---
id: ac-02-07
title: Vẽ đường cong trơn mượt với lệnh SPLINE
category: Vẽ 2D
tags: [spline, ve-2d, duong-cong, fit-points, cv]
level: beginner
minutes: 15
needs: [ac-02-06]
appVersions: ['2024', '2025']
edition: all
---
# Vẽ đường cong trơn mượt với lệnh SPLINE

> **Mục tiêu:**
> - Sử dụng lệnh SPLINE để vẽ đường cong tham số mượt mà (NURBS curve).
> - Phân biệt hai phương pháp tạo và chỉnh sửa Spline: Fit Points và Control Vertices (CV).
> - Kiểm soát hướng tiếp tuyến (Tangency) và độ uốn lượn tại hai đầu mút đường cong.

## Lệnh này làm gì và khi nào dùng

Khi cần vẽ các hình học hữu cơ phi tròn không theo quy luật bán kính cố định (đường đồng mức bản đồ địa hình, dáng vỏ tàu thuỷ, thân xe ô tô, mặt cắt cánh quạt hoặc đường cắt gãy tôn sóng), các cung tròn của lệnh ARC hay PLINE không thể mô tả chân thực. Lúc này bạn cần đến [[Đường cong Spline]].

Lệnh `SPLINE` (phím tắt `SPL`) tạo ra đường cong toán học B-spline hữu tỷ không đồng nhất (NURBS). Đường cong này có đặc tính mượt mà liên tục ở mọi đạo hàm bậc cao.

AutoCAD cung cấp hai cách kiểm soát hình dáng Spline:
- **Fit Points (Điểm nội suy):** Đường cong bắt buộc phải đi xuyên qua chính xác các điểm bạn đã bấm chuột.
- **Control Vertices - CV (Đỉnh điều khiển):** Đường cong được uốn nắn theo khung lưới đa giác kiểm soát bên ngoài mà không nhất thiết phải chạm qua các đỉnh.

## Cách dùng từng bước

1. **Vẽ Spline theo Fit Points (Mặc định):**
   - Gõ lệnh `SPLINE` hoặc `SPL` rồi nhấn [Enter].
   - Nhấp chọn điểm thứ nhất, điểm thứ hai, điểm thứ ba... Đường cong sẽ uốn lượn mềm mại đi xuyên qua từng điểm.
   - Nhấn [Enter] để xác nhận kết thúc.
2. **Chuyển đổi phương thức Fit / CV:**
   - Gõ `SPL` [Enter], gõ chữ `M` (Method) rồi [Enter].
   - Gõ `F` nếu muốn vẽ theo Fit Points, hoặc gõ `C` nếu muốn vẽ theo Control Vertices.
3. **Khép kín đường cong Spline:**
   - Trong quá trình nhấp các điểm uốn, gõ chữ `C` (Close) rồi nhấn [Enter] để tự động khép kín đầu và đuôi thành một vòng cong trơn tru.
4. **Hiệu chỉnh hình dáng sau khi vẽ:**
   - Nhấp chuột chọn đường Spline.
   - Bấm vào mũi tên nhỏ màu xanh hình tam giác xuất hiện gần điểm đầu: Bạn có thể chuyển đổi tức thời giữa hiển thị kẹp kiểu *Fit* hoặc kiểu *Control Vertices*.
   - Kéo các điểm kẹp (Grip) để nắn chỉnh độ cong theo ý muốn.

## Tuỳ chọn và mẹo

> [!TIP]
> Không nên nhấp quá nhiều điểm Fit san sát nhau khi vẽ Spline. Càng ít điểm kiểm soát, đường cong của bạn sẽ càng mượt mà và bản vẽ càng nhẹ nhàng, tránh bị hiện tượng "lượn sóng gồ ghề".

> [!TIP]
> Muốn biến một đường Polyline gấp khúc thành đường Spline mượt, bạn có thể dùng lệnh `PEDIT` rồi chọn tuỳ chọn `Spline`.

## Tự kiểm tra

```quiz
id: q-ac-02-07-1
type: single
question: Phương pháp tạo Spline theo kiểu "Fit Points" có đặc điểm nổi bật nào?
options:
  - text: Đường cong bắt buộc phải đi xuyên qua chính xác các điểm người dùng bấm chọn
    correct: true
    why: Fit Points là các điểm nội suy mà đường cong đi qua trực tiếp
  - text: Đường cong chỉ đi gần và chịu lực hút của các điểm kiểm soát bên ngoài
    why: Đó là đặc điểm của Control Vertices (CV)
  - text: Chỉ vẽ được các đoạn thẳng gấp khúc
    why: Spline luôn là đường cong trơn mượt
  - text: Luôn tạo ra một đường tròn khép kín
    why: Spline có thể là đường cong hở hoặc kín tuỳ ý
explain: "Trong phương thức Fit Points, thuật toán nội suy của AutoCAD đảm bảo đường cong mềm mại sẽ đi chính xác qua từng điểm bấm chuột của bạn."
tags: [spline, fit-points]
```

```quiz
id: q-ac-02-07-2
type: single
question: Khi chọn một đường cong Spline đã vẽ, ký hiệu hình tam giác nhỏ màu xanh cạnh đầu mút dùng để làm gì?
options:
  - text: Chuyển đổi hiển thị điểm kẹp giữa chế độ Fit và Control Vertices
    correct: true
    why: Mũi tên tam giác cho phép chuyển đổi nhanh cách thức nắn chỉnh đường cong
  - text: Xoá bỏ đường Spline
    why: Xoá dùng lệnh ERASE hoặc phím Delete
  - text: Biến đường Spline thành đường thẳng
    why: Không thể biến Spline thành đường thẳng bằng nút này
  - text: Khoá đối tượng không cho chỉnh sửa
    why: Khoá đối tượng dùng tính năng khoá Layer
explain: "Ký hiệu tam giác Grip Menu trên Spline cho phép bạn chuyển đổi linh hoạt giữa giao diện chỉnh sửa bằng Fit Points hoặc Control Vertices (CV)."
tags: [spline, grips, fit-cv]
```

```quiz
id: q-ac-02-07-3
type: truefalse
question: Nhấp càng nhiều điểm Fit san sát nhau thì đường cong Spline càng trơn mượt và dễ nắn chỉnh.
answer: false
explain: "Ngược lại, đặt quá nhiều điểm nội suy sẽ làm đường cong dễ bị gãy khúc, gợn sóng cục bộ và rất khó nắn chỉnh đồng đều."
tags: [spline, meo, fit]
```

## Lỗi thường gặp

- **Triệu chứng:** Đường Spline bị gấp khúc cục bộ và méo mó kỳ lạ tại các điểm uốn.
  - *Nguyên nhân:* Nhấp quá nhiều điểm Fit sát nhau hoặc điểm cuối bị giật ngược tiếp tuyến.
  - *Cách sửa:* Chọn đường Spline, bấm vào các điểm kẹp thừa và chọn *Remove Fit Point* để giảm bớt số điểm kiểm soát.
- **Triệu chứng:** Không thể đo diện tích vùng kín bao bởi đường Spline.
  - *Nguyên nhân:* Hai đầu mút của Spline chỉ chạm vào nhau bằng mắt thường chứ chưa dùng tuỳ chọn Close của lệnh.
  - *Cách sửa:* Chọn đường Spline, trong bảng Properties ([Ctrl + 1]) tìm mục *Closed* và đổi từ `No` sang `Yes`.

## Bài tập thực hành

- [ ] Gõ `SPLINE` và bấm lần lượt 4 điểm ziczac trên màn hình để tạo đường cong uốn lượn tự do. <!-- expect: SPLINE -->
- [ ] Nhấn [Enter] để kết thúc lệnh.
- [ ] Nhấp chuột chọn đường Spline vừa vẽ để hiển thị các điểm kẹp Fit màu xanh.
- [ ] Bấm vào biểu tượng tam giác Grip Menu và chuyển sang chế độ `Control Vertices`.
- [ ] Kéo thử một đỉnh điều khiển CV để quan sát cách đường cong uốn lượn mượt mà theo khung lưới.

## Nguồn tham khảo

```links
- title: Lệnh SPLINE và đường cong NURBS (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=SPLINE+Command
  kind: official
  lang: en
  note: Hướng dẫn chi tiết phương thức Fit, Control Vertices, bậc đường cong và tiếp tuyến
- title: Chỉnh sửa Spline bằng SPLINEDIT (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=SPLINEDIT+Command
  kind: official
  lang: en
  note: Thêm bớt điểm Fit, làm mịn và chuyển đổi Polyline sang Spline
```
