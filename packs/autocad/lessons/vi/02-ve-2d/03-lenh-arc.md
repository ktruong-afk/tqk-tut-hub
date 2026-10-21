---
id: ac-02-03
title: Vẽ cung tròn với lệnh ARC
category: Vẽ 2D
tags: [arc, ve-2d, cung-tron, ban-kinh]
level: beginner
minutes: 15
needs: [ac-02-02]
appVersions: ['2024', '2025']
edition: all
---
# Vẽ cung tròn với lệnh ARC

> **Mục tiêu:**
> - Sử dụng lệnh ARC để dựng cung tròn qua 3 điểm (3-Point Arc) nhanh chóng.
> - Áp dụng các phương thức dựng cung tròn có điều kiện: Start-Center-End và Start-End-Radius.
> - Kiểm soát chiều cong của cung tròn theo quy tắc ngược chiều kim đồng hồ của AutoCAD.

## Lệnh này làm gì và khi nào dùng

Lệnh `ARC` (phím tắt `A`) dùng để tạo một phân đoạn [[Cung tròn]] mở. Trong thiết kế kiến trúc và cơ khí, cung tròn là yếu tố không thể thiếu khi vẽ cửa mở trên mặt bằng, vòm cuốn kiến trúc, góc lượn chuyển tiếp hoặc đường dẫn cam cơ cấu máy.

Mặc định, lệnh ARC vẽ cung tròn đi qua 3 điểm. Tuy nhiên trên thanh công cụ Ribbon (mục Draw > Arc), AutoCAD hỗ trợ tới 11 cách phối hợp khác nhau giữa: Điểm đầu (Start), Tâm (Center), Điểm cuối (End), Bán kính (Radius), Góc ở tâm (Angle) và Chiều dài dây cung (Length).

Một nguyên tắc vàng bạn bắt buộc phải ghi nhớ: AutoCAD luôn vẽ cung tròn theo chiều **ngược chiều kim đồng hồ** từ điểm bắt đầu đến điểm kết thúc.

## Cách dùng từng bước

1. **Vẽ cung tròn qua 3 điểm (3-Point):**
   - Gõ `ARC` hoặc `A` rồi nhấn [Enter].
   - Nhấp chọn điểm bắt đầu (Start point).
   - Nhấp chọn điểm thứ hai nằm trên thân cung tròn (Second point).
   - Nhấp chọn điểm kết thúc (End point).
2. **Vẽ cung tròn theo Start, Center, End:**
   - Gõ `A` rồi nhấn [Enter].
   - Bấm điểm đầu tiên (Start point).
   - Gõ chữ `C` (Center) rồi bấm chọn điểm tâm cung tròn.
   - Bấm điểm kết thúc (End point).
3. **Vẽ cung tròn theo Start, End, Radius:**
   - Trên Ribbon, chọn *Home > Draw > Arc flyout > Start, End, Radius*.
   - Nhấp điểm đầu (Start).
   - Nhấp điểm cuối (End).
   - Nhập giá trị [[Bán kính]] mong muốn (ví dụ `50`) rồi nhấn [Enter].
4. **Vẽ tiếp tuyến nối tiếp đối tượng trước:**
   - Gõ `ARC` rồi nhấn [Enter] ngay hai lần liên tiếp (không bấm điểm nào). AutoCAD sẽ tự động tạo cung tròn tiếp tuyến nối mượt vào điểm mút cuối cùng của đường thẳng hoặc cung tròn bạn vừa vẽ.

## Tuỳ chọn và mẹo

> [!TIP]
> Nếu cung tròn bị uốn cong ngược hướng so với ý muốn (cong lõm thay vì cong lồi), hãy đè giữ phím [Ctrl] trên bàn phím trong lúc rê chuột để đảo ngược chiều quay của cung tròn.

> [!TIP]
> Khi vẽ cánh cửa mở trên mặt bằng kiến trúc, phương pháp *Start, Center, End* kết hợp phím [F8] là cách dựng chuẩn xác và nhanh nhất.

## Tự kiểm tra

```quiz
id: q-ac-02-03-1
type: single
question: Quy ước mặc định của AutoCAD khi tạo cung tròn là cung được vẽ theo chiều nào?
options:
  - text: Ngược chiều kim đồng hồ (Counter-Clockwise)
    correct: true
    why: AutoCAD luôn tính chiều quay góc và vẽ cung tròn ngược chiều kim đồng hồ
  - text: Cùng chiều kim đồng hồ (Clockwise)
    why: Muốn cùng chiều kim đồng hồ phải đè phím Ctrl hoặc chọn điểm ngược lại
  - text: Tự do tuỳ vị trí con trỏ chuột
    why: AutoCAD có thuật toán góc quay xác định chứ không ngẫu nhiên
  - text: Luôn vẽ từ trái sang phải
    why: Chiều vẽ phụ thuộc vào toạ độ góc quay
explain: "Theo quy ước toán học chuẩn của AutoCAD, cung tròn luôn được sinh ra từ điểm đầu (Start) đến điểm cuối (End) theo chiều ngược chiều kim đồng hồ."
tags: [arc, chieu-quay]
```

```quiz
id: q-ac-02-03-2
type: single
question: Để vẽ cung tròn đi qua 3 điểm bất kỳ đã có sẵn trên bản vẽ, bạn dùng phương pháp nào?
options:
  - text: 3-Point Arc
    correct: true
    why: 3-Point là phương pháp mặc định của lệnh ARC
  - text: Start, Center, Length
    why: Phương pháp này cần biết tâm và chiều dài dây cung
  - text: Start, End, Angle
    why: Phương pháp này cần biết góc mở
  - text: Center, Radius
    why: Center Radius dùng cho đường tròn khép kín CIRCLE
explain: "Phương pháp 3-Point là cách dựng nhanh nhất của lệnh ARC, chỉ cần nhấp lần lượt 3 điểm mút mà không cần tính góc hay bán kính."
tags: [arc, 3-point]
```

```quiz
id: q-ac-02-03-3
type: truefalse
question: Khi đang vẽ cung tròn, đè giữ phím [Ctrl] sẽ giúp đảo ngược chiều cong của cung tròn ngay lập tức.
answer: true
explain: "Phím [Ctrl] hoạt động như một công tắc tạm thời giúp chuyển đổi giữa chiều quay ngược chiều kim đồng hồ và cùng chiều kim đồng hồ khi vẽ cung tròn."
tags: [arc, ctrl, meo]
```

## Lỗi thường gặp

- **Triệu chứng:** Cung tròn bị lộn ngược vào trong thay vì uốn vồng ra ngoài như mong muốn.
  - *Nguyên nhân:* Chọn điểm Start và End theo chiều cùng chiều kim đồng hồ.
  - *Cách sửa:* Đổi thứ tự chọn điểm (chọn điểm ngược lại) hoặc đè giữ phím [Ctrl] khi rê chuột để đảo chiều cong.
- **Triệu chứng:** Dùng phương thức *Start, End, Radius* nhưng AutoCAD không cho vẽ.
  - *Nguyên nhân:* Khoảng cách giữa điểm Start và End lớn hơn hai lần bán kính (khoảng cách lớn hơn đường kính đường tròn).
  - *Cách sửa:* Nhập bán kính lớn hơn một nửa khoảng cách giữa hai điểm mút.

## Bài tập thực hành

- [ ] Gõ `ARC` và bấm lần lượt 3 điểm bất kỳ trên màn hình để tạo một cung tròn 3-Point. <!-- expect: ARC -->
- [ ] Gõ `LINE` vẽ một đoạn thẳng nằm ngang dài 100mm. <!-- expect: LINE -->
- [ ] Dùng lệnh `ARC` để vẽ cung tròn nối từ đầu mút bên phải sang đầu mút bên trái với đỉnh cong uốn lên trên. <!-- expect: ARC -->
- [ ] Gõ lệnh `ARC` và nhấn [Enter] hai lần liên tiếp để vẽ một cung tròn tiếp tuyến nối mượt vào cung vừa vẽ. <!-- expect: ARC -->

## Nguồn tham khảo

```links
- title: Lệnh ARC và các phương thức vẽ cung tròn (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=ARC+Command
  kind: official
  lang: en
  note: Hướng dẫn chi tiết 11 tuỳ chọn phối hợp thông số của lệnh ARC
- title: Đảo chiều cung tròn bằng phím Ctrl (Autodesk Support)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Arc+Direction
  kind: official
  lang: en
  note: Cách thức kiểm soát hướng quay của cung tròn trong AutoCAD
```
