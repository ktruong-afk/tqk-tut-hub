---
id: ac-03-05
title: Cắt tỉa với TRIM và kéo dài với EXTEND
category: Chỉnh sửa
tags: [trim, extend, cat-tia, keo-dai, xep-net, giao-cat]
level: beginner
minutes: 15
needs: [ac-03-02]
appVersions: ['2024', '2025']
edition: all
---
# Cắt tỉa với TRIM và kéo dài với EXTEND

> **Mục tiêu:**
> - Sử dụng lệnh TRIM để xén bỏ các đoạn thừa tại vị trí giao cắt giữa các nét vẽ.
> - Sử dụng lệnh EXTEND để kéo dài đường thẳng hoặc cung cong chạm tới đường biên giới hạn.
> - Chuyển đổi qua lại tức thời giữa TRIM và EXTEND bằng phím Shift mà không cần thoát lệnh.

## Lệnh này làm gì và khi nào dùng

Khi phác thảo bản vẽ kỹ thuật, thói quen của người thiết kế chuyên nghiệp là vẽ phóng khoáng các đường gióng dài đan chéo nhau, sau đó dùng lệnh cắt tỉa để làm sạch:
- `TRIM` (phím tắt `TR`): [[Cắt tỉa]] và xén bỏ các đoạn thừa nằm ngoài hoặc nằm giữa các đường giao cắt.
- `EXTEND` (phím tắt `EX`): [[Kéo dài]] đầu mút của một đường nét cho đến khi nó chạm chính xác vào một đường ranh giới phía trước.

Từ AutoCAD 2021 trở đi, hai lệnh này được nâng cấp lên chế độ **Quick Mode (Mặc định)**: Bạn không cần phải mất công chọn trước đường dao cắt (Cutting Edges) như thời CAD cũ, chỉ cần gõ lệnh và chạm chuột vào đoạn nào thì đoạn đó sẽ bị cắt hoặc phóng dài ngay lập tức!

Đặc biệt: TRIM và EXTEND là một cặp lệnh song sinh. Khi đang ở trong lệnh TRIM, bạn chỉ cần đè giữ phím [Shift] thì lệnh sẽ tự động biến thành EXTEND và ngược lại.

```hotspots
image: media/ac-03-05-trim-extend.svg
alt: Sơ đồ minh hoạ cơ chế cắt xén nét thừa của lệnh TRIM và phóng dài chạm biên của lệnh EXTEND
layout: central
points:
  - id: trim-cut
    x: 25
    y: 35
    title: Lệnh TRIM (Cắt tỉa nét thừa)
    text: Nhấp chuột hoặc quét qua các đoạn nét thừa thò ra ngoài ranh giới dao cắt.
    quiz: q-ac-03-05-1
  - id: extend-reach
    x: 75
    y: 35
    title: Lệnh EXTEND (Kéo dài chạm biên)
    text: Nhấp vào đầu mút đoạn thẳng để phóng dài nó chạm tới đường ranh giới tiếp theo.
    quiz: q-ac-03-05-2
```

## Cách dùng từng bước

1. **Cắt tỉa nét thừa bằng TRIM (Quick Mode):**
   - Gõ `TRIM` hoặc phím tắt `TR` rồi nhấn [Enter].
   - Di chuyển con trỏ chuột đến đoạn nét thừa: Đoạn đó sẽ mờ đi kèm dấu gạch chéo đỏ.
   - Nhấp chuột trái vào đoạn đó để xén bỏ.
   - Bạn cũng có thể nhấn giữ chuột trái và kéo một đường quét (Fence) cắt qua hàng loạt nét thừa để xén sạch cùng một lúc.
   - Nhấn [Enter] hoặc [Esc] để kết thúc.
2. **Kéo dài nét chạm biên bằng EXTEND:**
   - Gõ `EXTEND` hoặc phím tắt `EX` rồi nhấn [Enter].
   - Rê chuột vào gần đầu mút của đường thẳng cần kéo dài: Một đường gióng dự báo màu xám sẽ thò ra chạm vào biên trước mắt.
   - Nhấp chuột trái để xác nhận kéo dài chạm biên.
   - Nhấn [Enter] để kết thúc.
3. **Mẹo đổi lệnh bằng phím Shift:**
   - Đang trong lệnh `TRIM`: Đè giữ phím [Shift] và nhấp vào một đoạn thẳng, đoạn thẳng đó sẽ được **phóng dài** (EXTEND).
   - Đang trong lệnh `EXTEND`: Đè giữ phím [Shift] và nhấp vào nét thừa, nét đó sẽ bị **cắt tỉa** (TRIM).

## Tuỳ chọn và mẹo

> [!TIP]
> Sử dụng thao tác quét đường thẳng (Fence Selection) trong lệnh TRIM: Chỉ cần bấm chuột và lướt con trỏ qua 10 đường dóng thừa, toàn bộ 10 đoạn thừa sẽ bị cắt sạch trong 1 giây!

> [!TIP]
> Nếu bạn muốn chuyển về phong cách chọn dao cắt thủ công như AutoCAD cổ điển, trong lệnh TRIM hãy chọn tuỳ chọn `Mode` và chuyển từ *Quick* sang *Standard*.

## Tự kiểm tra

```quiz
id: q-ac-03-05-1
type: single
question: Khi đang thực hiện lệnh TRIM, bạn có thể thực hiện thao tác kéo dài (EXTEND) bằng cách kết hợp phím nào?
options:
  - text: Đè giữ phím Shift và nhấp vào đối tượng
    correct: true
    why: Phím Shift đảo ngược chức năng giữa Trim và Extend ngay tức thì
  - text: Đè giữ phím Ctrl
    why: Phím Ctrl dùng cho các thao tác khác
  - text: Đè giữ phím Alt
    why: Phím Alt kích hoạt phím tắt trên menu Ribbon
  - text: Nhấn phím Tab
    why: Phím Tab chuyển đổi qua lại giữa các ô nhập liệu
explain: "Trong AutoCAD, đè giữ phím [Shift] trong lệnh TRIM sẽ tạm thời kích hoạt lệnh EXTEND, và ngược lại đè [Shift] trong EXTEND sẽ biến thành TRIM."
tags: [trim, extend, shift, meo]
```

```quiz
id: q-ac-03-05-2
type: single
question: Phím tắt mặc định của lệnh EXTEND trong AutoCAD là gì?
options:
  - text: EX
    correct: true
    why: EX là phím tắt chính thức của lệnh EXTEND
  - text: E
    why: E là phím tắt của lệnh ERASE
  - text: ET
    why: ET không phải phím tắt lệnh chuẩn
  - text: X
    why: X là phím tắt của lệnh phá vỡ EXPLODE
explain: "Phím tắt của lệnh EXTEND là EX, trong khi phím tắt của lệnh TRIM là TR."
tags: [extend, phim-tat]
```

```quiz
id: q-ac-03-05-3
type: truefalse
question: Trong chế độ Quick Mode của lệnh TRIM, bạn phải tự tay nhấp chọn từng đường dao cắt trước thì mới được cắt nét thừa.
answer: false
explain: "Trong chế độ Quick Mode hiện đại của AutoCAD, mọi đối tượng trên màn hình đều tự động được xem là dao cắt, bạn chỉ việc bấm vào đoạn thừa để xén ngay lập tức."
tags: [trim, quick-mode]
```

```quiz
id: q-ac-03-05-4
type: hotspot
question: Bấm vào vị trí minh hoạ thao tác cắt tỉa nét thừa TRIM trên hình.
use: hotspots
answer: trim-cut
explain: "Thao tác TRIM nằm ở nửa bên trái của sơ đồ, minh hoạ đoạn nét đứt thừa bị xén bỏ tại đường biên dao cắt."
tags: [trim, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Dùng lệnh EXTEND bấm vào đường thẳng nhưng không thấy nó phóng dài ra.
  - *Nguyên nhân:* Phía trước hướng phóng dài không có bất kỳ đối tượng nào làm biên giới hạn, hoặc đường biên nằm song song không thể cắt nhau.
  - *Cách sửa:* Đảm bảo có một đường bao cắt ngang qua hướng phóng dài của đường thẳng đó.
- **Triệu chứng:** Bấm chuột vào đoạn thẳng để TRIM nhưng đối tượng bị xoá sạch toàn bộ từ đầu đến đuôi.
  - *Nguyên nhân:* Đoạn thẳng đó không hề giao cắt với bất kỳ đường nào khác nên AutoCAD hiểu là bạn muốn xoá nó (Erase).
  - *Cách sửa:* Kiểm tra lại xem hai đường có thật sự giao nhau hay không (phóng to để kiểm tra xem có bị hở chân không).

## Bài tập thực hành

- [ ] Gõ `LINE` vẽ 3 đường thẳng đứng song song cách nhau 50mm. <!-- expect: LINE -->
- [ ] Gõ `LINE` vẽ 2 đường ngang cắt xuyên qua cả 3 đường đứng tạo thành khung lưới. <!-- expect: LINE -->
- [ ] Gõ `TRIM` và nhấp vào các đoạn thừa thò ra ngoài khung lưới để xén sạch viền bao. <!-- expect: TRIM -->
- [ ] Gõ `LINE` vẽ thêm một đường thẳng đứng độc lập cách khung 60mm về bên phải. <!-- expect: LINE -->
- [ ] Gõ `EXTEND` và nhấp vào hai đầu mút của các đường ngang để phóng dài chạm vào đường đứng mới. <!-- expect: EXTEND -->

## Nguồn tham khảo

```links
- title: Lệnh TRIM và chế độ Quick Mode (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=TRIM+Command
  kind: official
  lang: en
  note: Hướng dẫn chi tiết chế độ Quick Trim, Cutting Edges và hàng rào Fence
- title: Lệnh EXTEND kéo dài đối tượng (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=EXTEND+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn Boundary edges, Project, Edge mode của EXTEND
```
