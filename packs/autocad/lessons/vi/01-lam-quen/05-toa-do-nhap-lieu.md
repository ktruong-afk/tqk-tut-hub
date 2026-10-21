---
id: ac-01-05
title: Hệ toạ độ và các phương pháp nhập toạ độ chính xác
category: Làm quen
tags: [toa-do, absolute, relative, polar, dynamic-input]
level: beginner
minutes: 20
needs: [ac-01-04]
appVersions: ['2024', '2025']
edition: all
---
# Hệ toạ độ và các phương pháp nhập toạ độ chính xác

> **Mục tiêu:**
> - Phân biệt phương pháp nhập toạ độ tuyệt đối, toạ độ tương đối và toạ độ cực.
> - Sử dụng tính năng Dynamic Input (F12) để nhập kích thước trực tiếp tại con trỏ.
> - Áp dụng phương pháp nhập khoảng cách trực tiếp (Direct Distance Entry) kết hợp phương hướng.

## Lệnh này làm gì và khi nào dùng

Vẽ kỹ thuật đòi hỏi sự chính xác tuyệt đối từng phần trăm milimet. Không ai dùng chuột để ước lượng điểm rơi. Thay vào đó, AutoCAD dựa trên hệ toạ độ Descartes (X, Y) và cung cấp 4 phương pháp nhập liệu:
1. [[Hệ toạ độ tuyệt đối]] `X,Y`: Tính khoảng cách trực tiếp từ gốc toạ độ chuẩn (0,0).
2. [[Hệ toạ độ tương đối]] `@X,Y`: Tính độ dời delta X và delta Y từ điểm vừa chọn trước đó.
3. [[Toạ độ cực]] `@Khoảng_cách<Góc`: Nhập chiều dài đoạn thẳng và góc nghiêng quy ước (ví dụ `@100<45`).
4. Nhập khoảng cách trực tiếp: Rê chuột theo phương mong muốn rồi gõ thẳng chiều dài và nhấn [Enter].

Chế độ [[Dynamic Input]] (phím [F12]) đưa toàn bộ ô nhập này hiển thị nổi ngay đầu con trỏ chuột, giúp bạn tập trung tuyệt đối vào bản vẽ mà không cần liếc nhìn dòng lệnh.

## Cách dùng từng bước

1. **Bật Dynamic Input:** Nhấn phím [F12] trên bàn phím. Kiểm tra biểu tượng Dynamic Input trên thanh trạng thái đã sáng màu xanh.
2. **Nhập toạ độ tuyệt đối điểm đầu:** Gõ lệnh `LINE`, khi dòng lệnh hỏi `Specify first point:`, gõ `0,0` rồi nhấn [Enter] để bắt đầu đoạn thẳng đúng tại gốc toạ độ.
3. **Nhập toạ độ tương đối:** Khi dòng lệnh hỏi `Specify next point:`, gõ `@80,0` rồi nhấn [Enter]. Một đoạn thẳng dài 80mm nằm ngang sang phải sẽ được vẽ.
4. **Nhập toạ độ cực theo góc:** Tiếp tục gõ `@60<45` rồi nhấn [Enter]. Bạn sẽ có đoạn thẳng dài 60mm nghiêng một góc 45 độ ngược chiều kim đồng hồ.
5. **Dùng phím [Tab] chuyển ô Dynamic Input:** Khi Dynamic Input đang bật, gõ chiều dài `100`, nhấn phím [Tab] để chuyển sang ô khoá góc, gõ góc `30` rồi nhấn [Enter].
6. **Kết thúc lệnh:** Nhấn [Enter] hoặc [Esc] để hoàn thành.

## Tuỳ chọn và mẹo

> [!TIP]
> Khi bật Dynamic Input (F12), AutoCAD sẽ mặc định hiểu toạ độ bạn gõ là toạ độ tương đối, không cần phải gõ thủ công ký tự `@` phía trước.

> [!TIP]
> Nhập khoảng cách trực tiếp (Direct Distance Entry) kết hợp với phím [F8] (chế độ khoá phương vuông góc) là cách vẽ các cạnh ngang và dọc nhanh nhất mà không cần tính toạ độ.

## Thử tính toạ độ cực bằng code

Để hiểu rõ cách máy tính chuyển đổi toạ độ cực `@d<a` thành độ dời ngang `dx` và đứng `dy`, bạn hãy hoàn thiện hàm `polarToCartesian(d, angleDeg)` dưới đây rồi bấm **Chạy**.

```code-live
lang: js
title: Tính toạ độ Descartes từ toạ độ cực
starter: |
  function polarToCartesian(d, angleDeg) {
    const rad = angleDeg * Math.PI / 180;
    // Trả về { dx: d * cos, dy: d * sin }
    const dx = 0;
    const dy = 0;
    return { dx: Math.round(dx * 100) / 100, dy: Math.round(dy * 100) / 100 };
  }
  console.log(polarToCartesian(100, 45));
tests: |
  const p1 = polarToCartesian(100, 0);
  assert(Math.abs(p1.dx - 100) < 0.1 && Math.abs(p1.dy - 0) < 0.1, 'd=100 góc 0 độ thì dx=100, dy=0');
  const p2 = polarToCartesian(100, 90);
  assert(Math.abs(p2.dx - 0) < 0.1 && Math.abs(p2.dy - 100) < 0.1, 'd=100 góc 90 độ thì dx=0, dy=100');
  const p3 = polarToCartesian(100, 45);
  assert(Math.abs(p3.dx - 70.71) < 0.2 && Math.abs(p3.dy - 70.71) < 0.2, 'd=100 góc 45 độ thì dx=70.71, dy=70.71');
hints:
  - Dùng Math.cos(rad) cho trục X và Math.sin(rad) cho trục Y.
  - rad đã được đổi từ độ sang radian bằng công thức: angleDeg * Math.PI / 180.
solution: |
  function polarToCartesian(d, angleDeg) {
    const rad = angleDeg * Math.PI / 180;
    const dx = d * Math.cos(rad);
    const dy = d * Math.sin(rad);
    return { dx: Math.round(dx * 100) / 100, dy: Math.round(dy * 100) / 100 };
  }
  console.log(polarToCartesian(100, 45));
```

## Tự kiểm tra

```quiz
id: q-ac-01-05-1
type: single
question: Ký hiệu nào đứng trước toạ độ thể hiện điểm tiếp theo được tính tương đối từ điểm trước đó?
options:
  - text: "@"
    correct: true
    why: "Ký tự @ biểu thị toạ độ tương đối (Relative)"
  - text: "#"
    why: "Ký tự # dùng để cưỡng bức nhập toạ độ tuyệt đối khi Dynamic Input đang bật"
  - text: "$"
    why: "Ký tự $ không có ý nghĩa trong cú pháp toạ độ AutoCAD"
  - text: "<"
    why: "Ký tự < dùng để ngăn cách giữa khoảng cách và góc"
explain: "Cú pháp @X,Y hoặc @d<a cho AutoCAD biết điểm mới được xác định dựa trên gốc chuẩn là điểm bạn vừa bấm chọn trước đó."
tags: [toa-do, relative]
```

```quiz
id: q-ac-01-05-2
type: single
question: Phím tắt nào dùng để bật hoặc tắt chế độ nhập liệu động tại con trỏ (Dynamic Input)?
options:
  - { text: F12, correct: true, why: Phím F12 bật tắt Dynamic Input }
  - { text: F8, why: F8 dùng cho chế độ Ortho }
  - { text: F3, why: F3 dùng cho chế độ Osnap }
  - { text: F10, why: F10 dùng cho chế độ Polar Tracking }
explain: Phím chức năng [F12] điều khiển chế độ Dynamic Input, hiển thị kích thước và góc trực tiếp bên cạnh con trỏ chuột.
tags: [toa-do, dynamic-input, phim-tat]
```

```quiz
id: q-ac-01-05-3
type: short
question: Khi vẽ một đoạn thẳng dài 120mm nghiêng một góc 60 độ bằng toạ độ cực tương đối, bạn nhập cú pháp nào vào dòng lệnh?
answer: ["@120<60", "@120<60.0"]
explain: Cú pháp toạ độ cực tương đối là @khoảng_cách<góc, cụ thể ở đây là @120<60.
tags: [toa-do, polar]
```

## Lỗi thường gặp

- **Triệu chứng:** Gõ toạ độ `0,0` nhưng điểm lại không rơi vào gốc toạ độ mà rơi ngay tại vị trí con trỏ chuột.
  - *Nguyên nhân:* Chế độ Dynamic Input đang bật và ngầm hiểu bạn đang nhập toạ độ tương đối từ vị trí trước.
  - *Cách sửa:* Gõ thêm dấu thăng `#0,0` để cưỡng bức nhập toạ độ tuyệt đối khi Dynamic Input đang mở, hoặc tắt [F12].
- **Triệu chứng:** Đoạn thẳng vẽ theo góc nghiêng bị ngược hướng so với mong muốn.
  - *Nguyên nhân:* Nhập sai quy ước góc (AutoCAD tính góc tăng dần ngược chiều kim đồng hồ, nếu muốn quay xuống dưới phải nhập góc âm hoặc góc lớn hơn 180°).
  - *Cách sửa:* Nhập góc âm, ví dụ `@100<-30` thay vì `@100<30` nếu muốn đoạn thẳng nghiêng xuống dưới.

## Bài tập thực hành

- [ ] Nhấn [F12] để kích hoạt chế độ Dynamic Input trên bản vẽ.
- [ ] Gõ `LINE` và nhập điểm bắt đầu là `#0,0`. <!-- expect: LINE -->
- [ ] Nhập toạ độ tương đối `@100,0` để vẽ đoạn thẳng ngang dài 100mm.
- [ ] Nhập toạ độ cực `@80<45` để vẽ đoạn thẳng tiếp theo dài 80mm nghiêng 45 độ.
- [ ] Nhập toạ độ tương đối `@0,60` để đi thẳng lên trên 60mm.
- [ ] Gõ chữ `C` (Close) và nhấn [Enter] để khép kín hình về điểm xuất phát.

## Nguồn tham khảo

```links
- title: Hệ toạ độ và phương pháp nhập điểm (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Coordinate+Entry
  kind: official
  lang: en
  note: Toàn bộ quy tắc nhập toạ độ Descartes tuyệt đối, tương đối và toạ độ cực
- title: Sử dụng Dynamic Input (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Dynamic+Input
  kind: official
  lang: en
  note: Hướng dẫn tuỳ biến con trỏ chuột và các ô nhập toạ độ động
```
