---
id: ac-09-08
title: Trích xuất hình chiếu 2D từ mô hình 3D với SECTIONPLANE và FLATSHOT
category: Mô hình hoá 3D
tags: [sectionplane, flatshot, trich-xuat-2d, hinh-chieu, mat-cat-3d]
level: advanced
minutes: 25
needs: [ac-09-05]
appVersions: ['2024', '2025']
edition: full-only
---
# Trích xuất hình chiếu 2D từ mô hình 3D với SECTIONPLANE và FLATSHOT

> **Mục tiêu:**
> - Sử dụng lệnh `SECTIONPLANE` để tạo mặt phẳng cắt bổ đôi mô hình 3D quan sát trực quan cấu tạo bên trong.
> - Kích hoạt chế độ `Live Section` và tự động sinh bản vẽ mặt cắt 2D/3D có hoa văn gạch Hatch.
> - Sử dụng lệnh `FLATSHOT` để "chụp ảnh" góc nhìn 3D thành một khối Block 2D phẳng phục vụ đóng gói hồ sơ kỹ thuật.

## Cây cầu nối hoàn hảo giữa không gian 3D và bản vẽ 2D

Nhiều người e ngại vẽ 3D vì nghĩ rằng: "Đằng nào khi nộp cho thợ chế tạo hay nộp hồ sơ xin phép xây dựng cũng phải in ra bản vẽ 2D (hình chiếu đứng, hình chiếu bằng, mặt cắt), vẽ 3D xong lại phải ngồi vẽ lại 2D từ đầu thì mất công gấp đôi!".

Thực tế hoàn toàn ngược lại:
Trong quy trình thiết kế hiện đại, mô hình 3D là **nguồn dữ liệu gốc duy nhất (Single Source of Truth)**. Khi bạn đã dựng xong mô hình 3D:
- Bạn không cần vẽ tay bất kỳ hình chiếu 2D nào cả!
- AutoCAD cung cấp hai cỗ máy trích xuất tự động: **`SECTIONPLANE`** (Cắt bổ mặt cắt) và **`FLATSHOT`** (Chiếu phẳng 2D).
- Chỉ với 1 cú nhấp chuột, phần mềm tự động chụp lại các góc nhìn và xuất ra các khối Block 2D phẳng lì với đầy đủ nét thấy, nét khuất và ký hiệu mặt cắt hoa văn!

![Mặt phẳng cắt SECTIONPLANE và trích xuất FLATSHOT](media/ac-09-08-section-flatshot.svg)

```hotspots
image: media/ac-09-08-section-flatshot.svg
alt: Cơ chế mặt phẳng cắt SECTIONPLANE và trích xuất 2D với FLATSHOT
layout: central
points:
  - id: spot-1
    x: 23
    y: 35
    title: 1. Mặt phẳng cắt (SECTIONPLANE)
    text: "Đặt một mặt phẳng dao cắt xuyên qua chi tiết 3D để quan sát ruột bên trong."
  - id: spot-2
    x: 23
    y: 75
    title: Mặt cắt động (Live Section)
    text: "Tự động gọt bỏ nửa ngoài và tô vật liệu mặt cắt Hatch theo thời gian thực."
  - id: spot-3
    x: 75
    y: 35
    title: 2. Trích xuất phẳng (FLATSHOT)
    text: "Chụp góc nhìn hiện tại và ép phẳng thành một khối Block 2D hoàn chỉnh."
  - id: spot-4
    x: 75
    y: 75
    title: Phân biệt nét thấy và nét khuất
    text: "Tách nét thấy (Foreground) nét liền và nét khuất (Obscured) nét đứt màu đỏ."
```

## 1. Tạo mặt phẳng cắt động với SECTIONPLANE

### Cách dùng từng bước:
1. Gõ `SECTIONPLANE` rồi nhấn [Enter].
2. Dòng lệnh hỏi mặt phẳng cắt:
   - Gõ `O` (Orthographic) > chọn `Front` (Mặt cắt đứng nhìn từ phía trước).
   - Hoặc bấm 2 điểm bất kỳ để tự kẻ một đường dao cắt xuyên qua mô hình 3D.
3. Một khung hình chữ nhật trong suốt màu xanh lá cây xuất hiện cắt đôi vật thể.
4. Bấm chuột chọn vào khung mặt phẳng cắt, bấm vào biểu tượng mũi tên định hướng để bật chế độ **Live Sectioning**:
   - Nửa phía trước của mô hình lập tức biến mất!
   - Bạn nhìn thấy rõ ràng toàn bộ cấu tạo rãnh then, lỗ trục, khoang rỗng bên trong chi tiết.
5. Khi bạn di chuyển hoặc kéo dãn mặt phẳng cắt, hình ảnh mặt cắt bên trong sẽ tự động cập nhật theo thời gian thực!

### Xuất mặt cắt ra bản vẽ 2D:
- Nhấp chuột phải vào đường viền mặt phẳng cắt `Section Plane`.
- Chọn dòng **Generate Section Block...**.
- Chọn `2D Section / Elevation Block`, bấm nút **Create**.
- Bấm chuột đặt khối ra màn hình: Bạn đã có ngay một bản vẽ mặt cắt 2D sắc sảo có sẵn hoa văn gạch Hatch!

## 2. Chiếu phẳng góc nhìn 3D thành Block 2D với FLATSHOT

Nếu như `SECTIONPLANE` chuyên dùng để làm mặt cắt, thì **`FLATSHOT`** là công cụ kinh điển để xuất các hình chiếu đứng, hình chiếu bằng, và hình chiếu trục đo 3D sang bản vẽ 2D thông thường.

### Cách dùng từng bước:
1. Xoay mô hình 3D về góc nhìn bạn muốn xuất bản vẽ (ví dụ bấm góc `SW Isometric` trên ViewCube để lấy hình chiếu trục đo, hoặc bấm `Front` để lấy hình chiếu đứng).
2. Gõ `FLATSHOT` rồi nhấn [Enter]. Hộp thoại **Flatshot** xuất hiện:
   - **Destination:** Chọn `Insert as new block` (Chèn trực tiếp thành một khối Block vào bản vẽ hiện tại) hoặc `Export to a file` (Xuất ra file DWG riêng biệt).
   - **Foreground lines (Nét thấy):** Chọn màu `ByLayer`, kiểu nét `Continuous` (nét liền).
   - **Obscured lines (Nét khuất):** Đánh dấu tick vào ô **Show** để hiển thị các cạnh bị che khuất bên trong; chọn màu `Color 1 (Red)` và linetype là `DASHED` (nét đứt).
3. Bấm nút **Create**.
4. Di chuột và bấm chuột trái để đặt khối hình chiếu 2D ra khoảng trống bản vẽ.
5. Nhấn [Enter] 3 lần để chấp nhận tỉ lệ và góc xoay.
6. Một hình vẽ 2D phẳng tuyệt mỹ xuất hiện: Bạn có thể đo kích thước, ghi chú và in ấn như một bản vẽ 2D thông thường!

> [!TIP]
> Sử dụng `FLATSHOT` là phương pháp nhanh nhất để tạo hình ảnh minh họa trục đo 3D đặt vào góc trên bên phải của khung tên bản vẽ kỹ thuật giúp thợ chế tạo dễ hình dung sản phẩm.

## Tự kiểm tra

```quiz
id: q-ac-09-08-1
type: single
question: "Lệnh FLATSHOT trong AutoCAD dùng để làm gì?"
options:
  - text: "Chiếu phẳng góc nhìn 3D hiện tại thành một khối Block 2D có phân biệt nét thấy và nét khuất"
    correct: true
    why: "FLATSHOT chụp ảnh góc nhìn không gian và ép thành đối tượng phẳng 2D phục vụ in ấn bản vẽ."
  - text: "Làm nổ tung mô hình 3D thành từng mảnh vụn"
    correct: false
    why: "FLATSHOT không phá hủy hay làm hỏng mô hình 3D gốc."
  - text: "Xóa toàn bộ các khối 3D trên màn hình"
    correct: false
    why: "FLATSHOT chỉ tạo thêm một khối Block 2D mới."
  - text: "Đổi màu nền của AutoCAD sang màu trắng"
    correct: false
    why: "Màu nền do Options Display quản lý."
explain: "FLATSHOT là cây cầu kỳ diệu giúp chuyển hóa toàn bộ các góc nhìn phối cảnh 3D thành bản vẽ kỹ thuật 2D phẳng."
```

```quiz
id: q-ac-09-08-2
type: single
question: "Trong hộp thoại FLATSHOT, mục 'Obscured lines' phụ trách thiết lập hiển thị cho loại đường nét nào?"
options:
  - text: "Các nét khuất nằm ở phía sau bị che giấu bởi các mặt của vật thể"
    correct: true
    why: "Obscured lines quy định màu sắc và kiểu nét đứt cho các cạnh bị che khuất."
  - text: "Các đường kích thước đã bị xóa"
    correct: false
    why: "Không liên quan đến đường kích thước."
  - text: "Đường biên của khung tên bản vẽ"
    correct: false
    why: "Khung tên nằm ở không gian giấy Layout."
  - text: "Đường viền của con trỏ chuột"
    correct: false
    why: "Con trỏ chuột thuộc về phần cứng giao diện."
explain: "Thiết lập Obscured lines thành kiểu nét đứt DASHED giúp bản vẽ 2D thể hiện đầy đủ cấu tạo lỗ rỗng bên trong chi tiết."
```

```quiz
id: q-ac-09-08-3
type: truefalse
question: "Khi di chuyển mặt phẳng cắt SECTIONPLANE trên mô hình 3D, hình ảnh mặt cắt bên trong vật thể sẽ tự động thay đổi theo thời gian thực."
answer: true
explain: "Tính năng Live Sectioning của SECTIONPLANE cập nhật liên tục vị trí cắt theo thời gian thực rất trực quan."
```

## Lỗi thường gặp

- **Chèn khối FLATSHOT ra màn hình nhưng hình bị thu nhỏ li ti hoặc quá to:** Do góc nhìn khi chạy lệnh FLATSHOT đang bị méo tỉ lệ. Luôn đưa về góc nhìn chuẩn trục đo hoặc góc trực diện trước khi gõ lệnh.
- **Không thấy nét đứt của cạnh khuất xuất hiện:** Do trong hộp thoại FLATSHOT bạn quên không đánh dấu tick vào ô *Show* ở mục *Obscured lines*, hoặc do tỉ lệ nét đứt `LTSCALE` quá to.

## Bài tập thực hành

- [ ] Dùng `BOX` vẽ khối hộp 100 x 80 x 50 mm và dùng `CYLINDER` khoét một lỗ tròn xuyên giữa bằng `SUBTRACT`. <!-- expect: BOX -->
- [ ] Gõ lệnh `SECTIONPLANE`, kẻ một đường dao cắt đi qua tâm của lỗ tròn vừa khoét. <!-- expect: SECTIONPLANE -->
- [ ] Bấm vào đường viền mặt phẳng cắt để bật chế độ quan sát bổ đôi chi tiết.
- [ ] Xoay góc nhìn sang `SW Isometric`, gõ lệnh `FLATSHOT`. <!-- expect: FLATSHOT -->
- [ ] Trong hộp thoại FLATSHOT, tick chọn *Show* ở mục Obscured lines, chọn linetype là `DASHED`. Bấm Create và đặt hình chiếu 2D ra khoảng trống bản vẽ. <!-- expect: FLATSHOT -->

## Nguồn tham khảo

```links
- title: "Tạo mặt cắt với SECTIONPLANE từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=SECTIONPLANE"
  kind: official
- title: "Trích xuất hình chiếu 2D bằng FLATSHOT từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=FLATSHOT"
  kind: official
```
