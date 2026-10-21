---
id: ac-01-03
title: Điều hướng khung nhìn với Zoom, Pan và Regen
category: Làm quen
tags: [zoom, pan, regen, dieu-huong]
level: beginner
minutes: 15
needs: [ac-01-01]
appVersions: ['2024', '2025']
edition: all
---
# Điều hướng khung nhìn với Zoom, Pan và Regen

> **Mục tiêu:**
> - Sử dụng chuột giữa để phóng to, thu nhỏ và rê trượt vùng làm việc mượt mà.
> - Làm chủ các tuỳ chọn của lệnh ZOOM (All, Extents, Window, Previous).
> - Sử dụng lệnh REGEN để làm mịn các cung tròn và giải phóng giới hạn hiển thị.

## Lệnh này làm gì và khi nào dùng

Khi bản vẽ mở rộng với hàng nghìn chi tiết, khả năng [[Điều hướng khung nhìn]] nhanh chóng là yếu tố quyết định năng suất. Trong AutoCAD:
- **Pan (Rê trượt):** Di chuyển khung nhìn mà không làm thay đổi vị trí thực hay kích thước của đối tượng hình học.
- **Zoom (Phóng to / Thu nhỏ):** Thay đổi độ phóng đại để quan sát từ chi tiết nhỏ đến toàn bộ công trình.
- **Regen (Tái tạo màn hình):** Tính toán lại bộ nhớ đồ hoạ để làm mịn lại đường cong bị gãy và cho phép tiếp tục zoom khi bị kịch màn hình.

Hầu hết thao tác điều hướng thường ngày đều được thực hiện thông qua bánh xe chuột giữa (con lăn).

```hotspots
image: media/ac-01-03-dieu-huong.svg
alt: Minh hoạ khối ViewCube, thanh điều hướng Navigation Bar và các thao tác chuột giữa
layout: central
points:
  - id: viewcube-top
    x: 77
    y: 22
    title: Khối ViewCube
    text: Cho phép xoay góc nhìn 2D/3D nhanh chóng và định hướng trục toạ độ Bắc/Nam/Đông/Tây.
  - id: nav-bar
    x: 91
    y: 70
    title: Thanh Navigation Bar
    text: Chứa các công cụ rê trượt hình bàn tay (Pan) và công cụ phóng to khung nhìn (Zoom Extents).
    quiz: q-ac-01-03-1
  - id: mouse-wheel-tips
    x: 34
    y: 76
    title: Thao tác chuột giữa
    text: Lăn bánh xe để Zoom; đè giữ chuột giữa để Pan; nhấp đúp bánh xe để Zoom Extents toàn màn hình.
    quiz: q-ac-01-03-2
```

## Cách dùng từng bước

1. **Rê trượt bản vẽ (Pan):** Nhấn và giữ chặt bánh xe chuột giữa, con trỏ biến thành hình bàn tay, di chuyển chuột đến vị trí mong muốn rồi thả ra. Bạn cũng có thể gõ lệnh `PAN` (phím tắt `P`) rồi kéo chuột trái.
2. **Phóng to thu nhỏ (Zoom):** Lăn bánh xe chuột về phía trước để phóng to đối tượng dưới con trỏ, lăn về sau để thu nhỏ lại.
3. **Phóng to vừa khít toàn bộ đối tượng (Zoom Extents):** Nhấp nhanh đúp chuột giữa hai lần liên tiếp. Toàn bộ đối tượng có trong bản vẽ sẽ hiển thị vừa trọn vẹn màn hình.
4. **Phóng to một vùng cụ thể (Zoom Window):** Gõ lệnh `ZOOM` (phím tắt `Z`), nhấn [Enter], gõ `W` rồi bấm hai góc chéo của vùng chữ nhật muốn quan sát chi tiết.
5. **Khắc phục đường cong bị gãy (Regen):** Khi thấy đường tròn bị gãy khúc thành đa giác hoặc lăn chuột không phóng to được nữa, gõ `REGEN` (phím tắt `RE`) rồi nhấn [Enter].

## Tuỳ chọn và mẹo

> [!TIP]
> Nhấp đúp bánh xe chuột giữa (Zoom Extents) là cách nhanh nhất để tìm lại bản vẽ khi bạn vô tình phóng quá to hoặc zoom trôi ra ngoài khoảng không vô tận.

> [!TIP]
> Lệnh `ZOOM` kèm tuỳ chọn `Previous` (gõ `Z` [Enter] rồi `P` [Enter]) đưa bạn quay trở lại ngay lập tức khung nhìn trước đó.

## Tự kiểm tra

```quiz
id: q-ac-01-03-1
type: single
question: Thao tác nào dùng để phóng to toàn bộ đối tượng trong bản vẽ vừa vặn màn hình (Zoom Extents)?
options:
  - { text: Nhấp đúp nhanh chuột giữa hai lần, correct: true, why: Nhấp đúp chuột giữa là phím tắt nhanh nhất của Zoom Extents }
  - { text: Nhấp chuột phải chọn Zoom, why: Chuột phải mở menu ngữ cảnh }
  - { text: Đè giữ chuột trái và kéo, why: Đè chuột trái tạo vùng chọn đối tượng }
  - { text: Lăn chuột giữa về phía sau, why: Lăn về sau là thu nhỏ Zoom Out }
explain: Thao tác nhấp đúp bánh xe chuột giữa tương đương với việc thực hiện lệnh ZOOM rồi chọn tuỳ chọn Extents, giúp thu trọn toàn bộ bản vẽ vào màn hình.
tags: [dieu-huong, zoom-extents]
```

```quiz
id: q-ac-01-03-2
type: single
question: Khi đường tròn trên màn hình hiển thị gãy khúc thành nhiều đoạn thẳng do giới hạn bộ nhớ đồ hoạ, bạn dùng lệnh nào để làm mịn lại?
options:
  - { text: REGEN, correct: true, why: REGEN tái tạo lại đồ hoạ màn hình từ dữ liệu toán học gốc }
  - { text: REDO, why: REDO dùng để khôi phục thao tác vừa Undo }
  - { text: RECTANG, why: RECTANG dùng để vẽ hình chữ nhật }
  - { text: ERASE, why: ERASE dùng để xoá đối tượng }
explain: Lệnh REGEN (gõ tắt RE) tính toán lại toạ độ hiển thị vector trên màn hình, giúp các đường tròn và cung tròn trở lại trạng thái tròn mượt chuẩn xác.
tags: [dieu-huong, regen]
```

```quiz
id: q-ac-01-03-3
type: truefalse
question: Thao tác rê trượt bản vẽ (Pan) sẽ làm thay đổi giá trị toạ độ thực của các đối tượng hình học.
answer: false
explain: Thao tác Pan chỉ thay đổi góc quan sát của khung nhìn (camera), toạ độ hình học gốc của đối tượng trong không gian Model hoàn toàn không thay đổi.
tags: [dieu-huong, pan]
```

```quiz
id: q-ac-01-03-4
type: hotspot
question: Bấm vào thanh công cụ Navigation Bar trên sơ đồ điều hướng.
use: hotspots
answer: nav-bar
explain: Thanh Navigation Bar nằm ở cạnh phải màn hình, chứa các công cụ điều hướng trực quan như Pan và Zoom.
tags: [dieu-huong, nav-bar]
```

## Lỗi thường gặp

- **Triệu chứng:** Lăn bánh xe chuột không thể thu nhỏ hoặc phóng to thêm được nữa (*"Cannot zoom in/out any further"*).
  - *Nguyên nhân:* Bộ nhớ đệm đồ hoạ màn hình của AutoCAD đã chạm ngưỡng giới hạn tính toán hiện tại.
  - *Cách sửa:* Gõ lệnh `REGEN` rồi nhấn [Enter], sau đó bạn có thể tiếp tục lăn chuột bình thường.
- **Triệu chứng:** Màn hình trắng trơn, không thấy đối tượng đâu sau khi mở bản vẽ.
  - *Nguyên nhân:* Vùng nhìn đang nằm ở toạ độ quá xa so với vị trí đối tượng được vẽ.
  - *Cách sửa:* Nhấp đúp chuột giữa hai lần liên tiếp (Zoom Extents) để đưa toàn bộ hình vẽ về giữa màn hình.

## Bài tập thực hành

- [ ] Di chuyển con trỏ chuột vào vùng vẽ và lăn bánh xe chuột để quan sát hiệu ứng phóng to, thu nhỏ.
- [ ] Đè giữ bánh xe chuột giữa và rê chuột sang trái, phải để thực hiện thao tác Pan.
- [ ] Gõ lệnh `PAN` và rê chuột bằng phím chuột trái, sau đó nhấn phím [Esc] để thoát. <!-- expect: PAN -->
- [ ] Gõ `ZOOM` rồi nhập `E` (Extents) để bao quát toàn bộ vùng làm việc. <!-- expect: ZOOM -->
- [ ] Gõ `REGEN` và nhấn [Enter] để làm mới bộ nhớ đồ hoạ bản vẽ. <!-- expect: REGEN -->

## Nguồn tham khảo

```links
- title: Lệnh ZOOM và các phương pháp điều hướng (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=ZOOM+Command
  kind: official
  lang: en
  note: Hướng dẫn chi tiết các tuỳ chọn All, Extents, Window, Dynamic của lệnh ZOOM
- title: Lệnh REGEN và cơ chế tái tạo đồ hoạ (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=REGEN+Command
  kind: official
  lang: en
  note: Giải thích nguyên lý tính toán vector và làm mịn cung tròn trong AutoCAD
```
