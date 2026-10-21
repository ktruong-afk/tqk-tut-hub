---
id: ac-07-03
title: Làm chủ khung nhìn Viewport với MVIEW, MSPACE và PSPACE
category: Layout và In ấn
tags: [mview, mspace, pspace, viewport, ti-le, khoa-khung]
level: intermediate
minutes: 25
needs: [ac-07-02]
appVersions: ['2024', '2025']
edition: all
---
# Làm chủ khung nhìn Viewport với MVIEW, MSPACE và PSPACE

> **Mục tiêu:**
> - Sử dụng lệnh `MVIEW` để tạo các khung nhìn hình chữ nhật hoặc đa giác trên bản vẽ Layout.
> - Di chuyển linh hoạt giữa không gian giấy và mô hình bằng lệnh `MSPACE` và `PSPACE`.
> - Gán tỉ lệ bản vẽ chuẩn xác và khóa bảo vệ khung nhìn với tính năng `Display Locked`.

## Khái niệm khung nhìn Viewport: Ô cửa sổ nhìn vào mô hình

Hãy tưởng tượng bạn đang cầm trên tay một tờ bìa các-tông A3 màu trắng. Bạn lấy kéo khoét một ô cửa sổ hình chữ nhật ở giữa tờ bìa, rồi đưa lên mắt nhìn qua ô cửa đó vào căn phòng rộng lớn phía trước.

Ô cửa sổ đó chính là **[[Viewport]] (Khung nhìn)** trong AutoCAD!
- Trên một tờ giấy Layout A3, bạn có thể khoét bao nhiêu ô cửa sổ tùy thích.
- Ô thứ nhất nhìn vào phòng khách với tỉ lệ thu nhỏ 1:50.
- Ô thứ hai nhìn vào chi tiết khớp nối cơ khí với tỉ lệ phóng to 2:1.
- Toàn bộ hình ảnh nhìn thấy qua Viewport đều là hình ảnh sống động của không gian Model theo thời gian thực.

![Làm chủ khung nhìn Viewport](media/ac-07-03-mview-scale.svg)

```hotspots
image: media/ac-07-03-mview-scale.svg
alt: Cấu tạo khung nhìn Viewport và quy trình điều khiển khóa tỉ lệ
layout: central
points:
  - id: spot-1
    x: 23
    y: 35
    title: Viewport mặt bằng (Tỉ lệ 1:100)
    text: "Khung nhìn chính hiển thị tổng thể công trình với tỉ lệ 1:100 đã được khóa."
  - id: spot-2
    x: 48
    y: 15
    title: Biểu tượng Ổ khóa (Display Locked)
    text: "Khóa bảo vệ không cho phép thay đổi tỉ lệ khi vô tình lăn chuột."
  - id: spot-3
    x: 75
    y: 35
    title: Viewport trích đoạn (Tỉ lệ 1:25)
    text: "Khung nhìn phụ phóng to chi tiết cấu tạo ở tỉ lệ 1:25 trên cùng một tờ giấy."
  - id: spot-4
    x: 75
    y: 70
    title: Thoát về Paper Space (PSPACE)
    text: "Nhấp đúp chuột ra ngoài mặt giấy để vẽ khung tên và ghi chú tiêu đề bản vẽ."
```

## Bộ ba thao tác cốt lõi: MVIEW, MSPACE và PSPACE

### 1. Tạo khung nhìn với lệnh MVIEW (Lệnh tắt MV)
1. Đang ở trong không gian Layout.
2. Gõ `MV` hoặc `MVIEW` rồi nhấn [Enter].
3. Bấm chuột trái điểm thứ nhất và điểm thứ hai để quét mở một ô cửa sổ chữ nhật.
4. Ngay lập tức, toàn bộ công trình bạn đã vẽ ở Model sẽ xuất hiện thu nhỏ bên trong ô cửa sổ đó!
*(Mẹo: Gõ `MV` > chọn tuỳ chọn `Polygonal` để vẽ khung nhìn hình đa giác ziczac hoặc `Object` để biến một đường tròn thành khung nhìn).*

### 2. "Chui vào trong" để xoay và căn chỉnh hình với MSPACE (MS)
Để di dời hoặc phóng to hình vẽ bên trong khung nhìn:
- **Cách 1:** Nhấp đúp chuột trái vào **bên trong** ô Viewport.
- **Cách 2:** Gõ lệnh `MS` hoặc `MSPACE` rồi nhấn [Enter].
- Đường viền của Viewport sẽ sáng đậm lên, con trỏ chuột biến thành dấu chữ thập nằm gọn bên trong khung. Lúc này bạn đang thao tác trực tiếp trên Model Space: bạn có thể nhấn giữ bánh xe chuột giữa để `PAN` hình vẽ vào vị trí trung tâm đẹp nhất.

### 3. Gán tỉ lệ xích chuẩn xác và KHÓA KHUNG
Đây là bước quan trọng nhất quyết định bản vẽ có đúng tiêu chuẩn kỹ thuật hay không:
1. Nhìn xuống thanh trạng thái góc dưới bên phải màn hình: Bạn sẽ thấy ô số thể hiện tỉ lệ khung nhìn (ví dụ `0.0125` hoặc `Custom`).
2. Bấm vào ô số đó: Danh sách các tỉ lệ chuẩn quốc tế sẽ hiện ra (`1:100`, `1:50`, `1:25`, `1:20`, `1:10`...).
3. Bấm chọn tỉ lệ mong muốn (ví dụ: `1:100`). Hình vẽ bên trong sẽ tự động nhảy đúng kích thước xích 1:100!
4. **BƯỚC SỐNG CÒN:** Bấm vào biểu tượng **Chiếc ổ khóa** màu xanh ngay bên cạnh (hoặc trong bảng Properties đặt `Display locked = Yes`). Sau khi khóa, dù bạn có vô tình lăn chuột phóng to thu nhỏ, tỉ lệ 1:100 vẫn được giữ nguyên vẹn 100%!

### 4. "Thoát ra ngoài" mặt giấy với PSPACE (PS)
Sau khi căn chỉnh xong hình ảnh bên trong:
- **Cách 1:** Nhấp đúp chuột trái vào **khoảng trống màu xám bên ngoài tờ giấy**.
- **Cách 2:** Gõ lệnh `PS` hoặc `PSPACE` rồi nhấn [Enter].
- Viền khung nhìn mỏng trở lại. Giờ đây bạn đã an toàn quay lại mặt giấy để ghi chú và vẽ khung tên.

## Tính năng đóng băng Layer theo từng khung nhìn (VP Freeze)

Bạn có một mặt bằng nhưng muốn:
- Viewport 1 (Kiến trúc): Hiện tường và cửa, ẩn nét thép.
- Viewport 2 (Kết cấu): Hiện dầm và thép, ẩn nét nội thất bàn ghế.

Nếu tắt bóng đèn Layer thông thường, layer đó sẽ biến mất trên toàn bộ bản vẽ.
AutoCAD cung cấp cột **VP Freeze (Viewport Freeze - Biểu tượng mặt trời có trang giấy nhỏ)** trong bảng Layer:
- Chui vào Viewport 1 gõ `LA`, bấm đóng băng cột `VP Freeze` của layer cốt thép.
- Lập tức cốt thép biến mất ở Viewport 1 nhưng vẫn hiển thị bình thường ở Viewport 2!

> [!TIP]
> Hãy luôn tạo một layer riêng có tên `DEFPOINTS` hoặc `KHUNG_NHIN` (đặt chế độ No Plot) để chứa đường bao của các Viewport. Khi in ra giấy, đường viền ô chữ nhật Viewport sẽ hoàn toàn vô hình, bản vẽ chỉ hiển thị các chi tiết kỹ thuật sạch đẹp.

## Tự kiểm tra

```quiz
id: q-ac-07-03-1
type: single
question: "Để thoát khỏi chế độ chỉnh sửa bên trong khung nhìn và quay trở lại mặt phẳng tờ giấy Layout, lệnh tắt chuẩn là gì?"
options:
  - text: "PSPACE (lệnh tắt PS)"
    correct: true
    why: "PSPACE (Paper Space) đưa người dùng quay lại mặt phẳng tờ giấy in."
  - text: "MSPACE (lệnh tắt MS)"
    correct: false
    why: "MSPACE đưa người dùng chui vào trong khung nhìn mô hình."
  - text: "ESC"
    correct: false
    why: "Nhấn Esc chỉ hủy lệnh hiện tại, không tự động thoát khỏi Model Space trong Viewport."
  - text: "QUIT"
    correct: false
    why: "QUIT sẽ đóng phần mềm AutoCAD."
explain: "Sử dụng cặp lệnh MS (MSPACE - chui vào trong) và PS (PSPACE - thoát ra ngoài giấy) để điều khiển linh hoạt không gian Layout."
```

```quiz
id: q-ac-07-03-2
type: single
question: "Tính năng 'Display Locked' (Biểu tượng chiếc ổ khóa) của khung nhìn Viewport có tác dụng gì quan trọng nhất?"
options:
  - text: "Cố định tỉ lệ bản vẽ, ngăn ngừa việc vô tình lăn chuột làm sai lệch tỉ lệ xích đã thiết lập"
    correct: true
    why: "Khi đã khóa, thao tác lăn chuột Zoom chỉ phóng to tờ giấy chứ không làm đổi tỉ lệ của hình bên trong."
  - text: "Không cho phép bất kỳ ai in bản vẽ ra giấy"
    correct: false
    why: "Display Locked không ngăn cản việc in ấn."
  - text: "Đổi màu toàn bộ hình vẽ thành màu xám"
    correct: false
    why: "Khóa khung nhìn không làm đổi màu sắc đối tượng."
  - text: "Tự động khóa máy tính khi người vẽ rời bàn"
    correct: false
    why: "Đây là tính năng bảo vệ khung nhìn trong AutoCAD."
explain: "Display Locked là nguyên tắc bắt buộc phải thực hiện ngay sau khi gán tỉ lệ cho Viewport để bảo vệ tính chính xác của bản vẽ."
```

```quiz
id: q-ac-07-03-3
type: truefalse
question: "Tính năng VP Freeze trong bảng Layer Properties cho phép ẩn layer ở riêng khung nhìn này mà không làm ảnh hưởng đến các khung nhìn khác trên cùng tờ giấy."
answer: true
explain: "VP Freeze (Viewport Freeze) là công cụ tối thượng giúp một bản vẽ mặt bằng có thể trình bày thành nhiều bộ môn khác nhau trên cùng trang Layout."
```

## Lỗi thường gặp

- **Chui vào Viewport phóng to quá mức bị kẹt chuột không thoát ra được:** Khi zoom quá to, Viewport choán hết 100% màn hình, không còn khoảng trống màu xám nào để nhấp đúp ra ngoài. Khắc phục: Bình tĩnh gõ lệnh `PS` (hoặc `PSPACE`) rồi nhấn [Enter], hoặc bấm vào nút chữ `MODEL` trên thanh trạng thái góc dưới để chuyển về `PAPER`.
- **Đường viền Viewport in đè lên bản vẽ:** Do để đường bao Viewport ở layer vẽ thông thường. Khắc phục: Chuyển đường bao Viewport sang layer `Defpoints` hoặc tắt biểu tượng máy in (Plotting icon) của layer chứa Viewport.

## Bài tập thực hành

- [ ] Trong tab `Layout`, gõ lệnh `MVIEW` (hoặc `MV`), quét 2 điểm để tạo một khung nhìn chữ nhật kích thước khoảng 250 x 180 mm. <!-- expect: MVIEW -->
- [ ] Gõ lệnh `MSPACE` (hoặc `MS`) để kích hoạt chế độ chỉnh sửa bên trong khung nhìn. <!-- expect: MSPACE -->
- [ ] Nhấn giữ bánh xe chuột giữa để PAN đối tượng vào vị trí trung tâm khung hình.
- [ ] Bấm vào ô tỉ lệ trên thanh trạng thái, chọn tỉ lệ `1:100`. Bấm vào biểu tượng chiếc ổ khóa để bật `Display Locked`.
- [ ] Gõ lệnh `PSPACE` (hoặc `PS`) để thoát ra ngoài không gian giấy Layout. <!-- expect: PSPACE -->

## Nguồn tham khảo

```links
- title: "Tạo và hiệu chỉnh Layout Viewports (MVIEW) từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=MVIEW"
  kind: official
- title: "Chuyển đổi MSPACE và PSPACE từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=MSPACE"
  kind: official
```
