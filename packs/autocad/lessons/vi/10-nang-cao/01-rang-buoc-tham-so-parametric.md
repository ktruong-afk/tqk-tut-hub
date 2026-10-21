---
id: ac-10-01
title: Thiết kế biến đổi thông minh với ràng buộc tham số Parametric
category: Nâng cao và Tự động hoá
tags: [parametric, geomconstraint, dimconstraint, parameters, rang-buoc]
level: advanced
minutes: 25
needs: [ac-09-10]
appVersions: ['2024', '2025']
edition: all
---
# Thiết kế biến đổi thông minh với ràng buộc tham số Parametric

> **Mục tiêu:**
> - Sử dụng lệnh `GEOMCONSTRAINT` để gán các ràng buộc hình học (song song, vuông góc, đồng tâm, tiếp xúc).
> - Sử dụng lệnh `DIMCONSTRAINT` để điều khiển kích thước đối tượng thông qua biến số và công thức toán học.
> - Quản lý bảng phương trình tham số trong `PARAMETERS` để thay đổi kích thước tổng thể mà không cần vẽ lại hình.

## Khái niệm thiết kế tham số Parametric trong AutoCAD

Trong cách vẽ truyền thống, hình vẽ của bạn là "hình tĩnh". Nếu bạn vẽ một hình chữ nhật có lỗ tròn ở giữa, khi dùng lệnh `STRETCH` kéo dài hình chữ nhật ra, lỗ tròn sẽ bị lệch sang một bên, bạn lại phải mất công dùng lệnh `MOVE` dời lỗ tròn về lại tâm.

**Thiết kế tham số ([[Parametric]])** đưa tư duy kỹ thuật lên một tầm cao mới:
Bạn không chỉ vẽ hình, bạn đang **thiết lập các mối quan hệ logic và toán học** giữa các đối tượng:
1. **Ràng buộc hình học (Geometric Constraints):** Ra lệnh cho hai đoạn thẳng luôn luôn song song, hoặc hai đường tròn luôn luôn đồng tâm. Khi bạn xoay một đoạn, đoạn kia tự động xoay theo!
2. **Ràng buộc kích thước (Dimensional Constraints):** Đặt chiều dài cạnh $d_1 = 120$, và chiều cao $d_2 = d_1 / 2$. Khi bạn đổi $d_1$ thành 200, toàn bộ hình chữ nhật tự động dãn to và chiều cao tự động nhảy thành 100 mà bạn không cần chạm vào lệnh `SCALE`!

![Ràng buộc tham số Parametric](media/ac-10-01-parametric-constraints.svg)

```hotspots
image: media/ac-10-01-parametric-constraints.svg
alt: Hệ thống ràng buộc hình học và ràng buộc kích thước trong AutoCAD Parametric
layout: central
points:
  - id: spot-1
    x: 23
    y: 35
    title: 1. Ràng buộc hình học (Geometric)
    text: "Cố định quan hệ: Song song, Vuông góc, Đồng tâm, Tiếp xúc, Trùng điểm."
  - id: spot-2
    x: 23
    y: 75
    title: Biểu tượng phù hiệu nhỏ
    text: "Các phù hiệu nhỏ // hoặc ⊥ xuất hiện bên cạnh cạnh để báo hiệu quan hệ logic."
  - id: spot-3
    x: 75
    y: 35
    title: 2. Ràng buộc kích thước (Dimensional)
    text: "Gán các biến d1, d2 điều khiển khoảng cách bằng biểu thức đại số."
  - id: spot-4
    x: 75
    y: 75
    title: Bảng Parameters Manager
    text: "Thay đổi giá trị biến số tại bảng tham số, hình vẽ tự động co giãn theo."
```

## 1. Gán ràng buộc hình học với GEOMCONSTRAINT

Chuyển sang thẻ **Parametric** trên thanh Ribbon, bạn sẽ thấy cụm công cụ **Geometric**:
- **Coincident (Trùng điểm):** Khóa hai đầu mút của hai đoạn thẳng luôn dính chặt vào nhau, kéo đoạn này đi đâu đoạn kia bám theo đó.
- **Parallel (Song song):** Buộc hai đường thẳng luôn song song tuyệt đối (biểu tượng `//`).
- **Perpendicular (Vuông góc):** Buộc hai cạnh luôn tạo thành góc 90 độ (biểu tượng `⊥`).
- **Concentric (Đồng tâm):** Khóa tâm của hai hình tròn hoặc cung cong luôn trùng nhau.
- **Tangent (Tiếp xúc):** Buộc đường thẳng luôn tiếp tuyến mượt mà với đường tròn.
- **Equal (Bằng nhau):** Buộc hai đoạn thẳng luôn có chiều dài bằng nhau, hoặc hai đường tròn luôn có cùng bán kính.

### Cách dùng:
1. Gõ `GEOMCONSTRAINT` rồi chọn loại ràng buộc (ví dụ `Parallel`).
2. Bấm chọn đoạn thẳng thứ nhất, bấm chọn đoạn thẳng thứ hai.
3. Đoạn thẳng thứ hai sẽ lập tức xoay song song với đoạn thứ nhất!

## 2. Gán ràng buộc kích thước với DIMCONSTRAINT

Khác với kích thước ghi chú thông thường (chỉ để đọc số đo), kích thước ràng buộc `Dimensional Constraint` là **kích thước chủ động điều khiển hình học**:
1. Gõ `DIMCONSTRAINT` rồi chọn kiểu đo (ví dụ `Linear`).
2. Đo chiều dài của cạnh hình chữ nhật:
   - Một nhãn kích thước xuất hiện có tên biến đại số: `d1 = 100`.
3. Nhấp đúp chuột vào chữ `d1 = 100`, sửa thành `d1 = 160`.
4. Hình chữ nhật tự động co giãn dài ra thành đúng 160mm ngay lập tức!

## 3. Quản lý phương trình toán học với PARAMETERS

Lệnh **`PARAMETERS`** mở bảng quản lý tham số **Parameters Manager**:
- Bạn có thể tạo thêm các biến số người dùng (User Parameters): ví dụ đặt biến `DoDayThép = 15`.
- Bạn có thể viết công thức liên kết giữa các kích thước:
  - Cạnh dài: `d1 = 200`
  - Cạnh rộng: `d2 = d1 * 0.6`
  - Khoảng cách lỗ khoan: `d3 = d1 / 4`
- Khi khách hàng yêu cầu đổi chiều dài $d_1$ từ 200 lên 300: Bạn chỉ cần gõ số `300` vào bảng Parameters. Toàn bộ chiều rộng và khoảng cách lỗ khoan trên bản vẽ tự động co giãn theo phương trình toán học chuẩn xác 100%!

> [!TIP]
> Sử dụng tính năng **Auto Constrain** trên Ribbon để AutoCAD tự động quét và phân tích gán toàn bộ các ràng buộc vuông góc, song song cho một hình vẽ phác thảo chỉ trong 1 giây.

## Tự kiểm tra

```quiz
id: q-ac-10-01-1
type: single
question: "Khác biệt bản chất giữa kích thước thông thường (DIMLINEAR) và kích thước ràng buộc tham số (DIMCONSTRAINT) là gì?"
options:
  - text: "Kích thước thông thường chỉ hiển thị số đo thụ động, còn kích thước tham số chủ động làm thay đổi hình dạng vật thể khi sửa giá trị"
    correct: true
    why: "DIMCONSTRAINT điều khiển trực tiếp kích thước hình học thông qua các biến số d1, d2."
  - text: "Kích thước tham số chỉ in ra được màu vàng"
    correct: false
    why: "Màu sắc do Layer quản lý."
  - text: "Kích thước thông thường chính xác hơn kích thước tham số"
    correct: false
    why: "Cả hai đều có độ chính xác toán học tuyệt đối như nhau."
  - text: "Kích thước tham số không cho phép nhập số thập phân"
    correct: false
    why: "DIMCONSTRAINT hỗ trợ số thực và công thức đại số phức tạp."
explain: "Trong thiết kế Parametric, khi bạn sửa con số kích thước tham số, đối tượng hình học sẽ tự động co giãn theo con số đó."
```

```quiz
id: q-ac-10-01-2
type: single
question: "Hộp thoại hoặc bảng điều khiển nào trong AutoCAD cho phép người kỹ sư nhập các công thức phương trình đại số (ví dụ d2 = d1 / 2) để điều khiển bản vẽ?"
options:
  - text: "Parameters Manager (lệnh PARAMETERS)"
    correct: true
    why: "Parameters Manager quản lý toàn bộ cây biến số và phương trình toán học của bản vẽ."
  - text: "Layer Properties Manager"
    why: "Layer Manager quản lý lớp vẽ, màu sắc."
  - text: "Dimension Style Manager"
    why: "Dimstyle quản lý kiểu dáng mũi tên, cỡ chữ."
  - text: "Sheet Set Manager"
    why: "Sheet Set Manager quản lý hồ sơ in ấn."
explain: "Parameters Manager là trung tâm điều khiển tham số hóa thông minh của AutoCAD."
```

```quiz
id: q-ac-10-01-3
type: truefalse
question: "Ràng buộc hình học Concentric trong GEOMCONSTRAINT buộc tâm của hai hình tròn hoặc cung cong luôn luôn trùng nhau khi di chuyển."
answer: true
explain: "Concentric khóa cứng vị trí tâm của các đường cong đồng tâm trong suốt quá trình biến đổi hình học."
```

## Lỗi thường gặp

- **Báo lỗi Over-constrained (Thừa ràng buộc):** Do bạn gán quá nhiều ràng buộc mâu thuẫn nhau (ví dụ: đã gán vuông góc nhưng lại gán thêm song song cho cùng 2 cạnh). Khắc phục: Xóa bớt các ràng buộc thừa.
- **Biểu tượng ràng buộc che kín màn hình:** Do các phù hiệu nhỏ // và ⊥ hiện quá nhiều. Khắc phục: Bấm nút **Hide All** trên thẻ Parametric để ẩn bớt các phù hiệu đi cho thoáng mắt.

## Bài tập thực hành

- [ ] Dùng `LINE` vẽ 4 đoạn thẳng tạo thành một tứ giác méo mó bất kỳ. <!-- expect: LINE -->
- [ ] Gõ lệnh `GEOMCONSTRAINT`, áp dụng ràng buộc `Parallel` cho 2 cặp cạnh đối diện để biến tứ giác thành hình bình hành. <!-- expect: GEOMCONSTRAINT -->
- [ ] Gán tiếp ràng buộc `Perpendicular` cho một góc để biến hình bình hành thành hình chữ nhật. <!-- expect: GEOMCONSTRAINT -->
- [ ] Gõ lệnh `DIMCONSTRAINT`, gán kích thước chiều dài `d1 = 100` cho cạnh đáy. <!-- expect: DIMCONSTRAINT -->
- [ ] Gõ lệnh `PARAMETERS` để mở bảng Parameters Manager, sửa giá trị `d1` thành `150` và quan sát hình chữ nhật tự động dãn dài theo. <!-- expect: PARAMETERS -->

## Nguồn tham khảo

```links
- title: "Ràng buộc hình học và kích thước Parametric từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Constraints"
  kind: official
- title: "Quản lý tham số với Parameters Manager từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=PARAMETERS"
  kind: official
```
