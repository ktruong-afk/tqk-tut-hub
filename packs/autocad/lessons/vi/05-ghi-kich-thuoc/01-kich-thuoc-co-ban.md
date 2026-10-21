---
id: ac-05-01
title: Đo kích thước cơ bản với DIMLINEAR và DIMALIGNED
category: Ghi kích thước
tags: [dimension, dimlinear, dimaligned, dimradius, dimdiameter, co-ban]
level: beginner
minutes: 20
needs: [ac-04-07]
appVersions: ['2024', '2025']
edition: all
---
# Đo kích thước cơ bản với DIMLINEAR và DIMALIGNED

> **Mục tiêu:**
> - Sử dụng thành thạo lệnh `DIMLINEAR` để đo đoạn thẳng theo phương ngang và đứng.
> - Áp dụng `DIMALIGNED` để đo đoạn thẳng xiên nghiêng song song với đối tượng.
> - Phân biệt cách đo bán kính (`DIMRADIUS`), đường kính (`DIMDIAMETER`) và góc (`DIMANGULAR`).

## Các loại kích thước cơ bản trong AutoCAD

Trong bản vẽ kỹ thuật, kích thước ([[Dimension]]) là thông tin sống còn để gia công chế tạo hoặc thi công xây dựng. Nếu vẽ đúng hình mà thiếu hoặc sai kích thước thì thợ không thể sản xuất sản phẩm.

AutoCAD cung cấp bộ lệnh ghi kích thước chuyên dụng cho từng dạng hình học:
- **Đo kích thước thẳng (Linear Dimension):** Lệnh `DIMLINEAR` (lệnh tắt `DLI`) đo khoảng cách chiếu theo phương ngang hoặc thẳng đứng giữa hai điểm.
- **Đo kích thước xiên (Aligned Dimension):** Lệnh `DIMALIGNED` (lệnh tắt `DAL`) đo khoảng cách thực song song với đoạn thẳng nghiêng.
- **Đo bán kính cung/tròn (Radius Dimension):** Lệnh `DIMRADIUS` (lệnh tắt `DRA`) đo bán kính, tự động chèn ký hiệu `R`.
- **Đo đường kính hình tròn (Diameter Dimension):** Lệnh `DIMDIAMETER` (lệnh tắt `DDI`) đo đường kính, tự động chèn ký hiệu `Ø`.
- **Đo góc (Angular Dimension):** Lệnh `DIMANGULAR` (lệnh tắt `DAN`) đo góc giữa hai đoạn thẳng hoặc góc của một cung tròn.

![Các loại kích thước cơ bản trong AutoCAD](media/ac-05-01-dimension-types.svg)

```hotspots
image: media/ac-05-01-dimension-types.svg
alt: Cấu tạo và các dạng đường kích thước tiêu chuẩn
layout: central
points:
  - id: spot-1
    x: 26
    y: 43
    title: Đo thẳng ngang (DIMLINEAR)
    text: Đo khoảng cách chiếu theo trục X giữa hai điểm đo (kết quả 120mm).
  - id: spot-2
    x: 44
    y: 43
    title: Đo đoạn xiên (DIMALIGNED)
    text: Đường kích thước chạy song song chính xác với cạnh xiên (kết quả 100mm).
  - id: spot-3
    x: 74
    y: 35
    title: Đo bán kính R (DIMRADIUS)
    text: Chỉ tâm và cung cong, hiển thị ký hiệu R (kết quả R35).
  - id: spot-4
    x: 74
    y: 70
    title: Đo đường kính Ø (DIMDIAMETER)
    text: Bấm chọn đường tròn, hiển thị ký hiệu phi Ø (kết quả Ø40).
```

## Cách dùng từng bước

### 1. Đo đoạn thẳng ngang hoặc đứng với DIMLINEAR
1. Chuyển sang layer kích thước (vd layer `KICH_THUOC` đã học ở chặng trước).
2. Gõ `DLI` hoặc `DIMLINEAR` rồi nhấn [Enter].
3. Bấm chuột chọn điểm đo thứ nhất (`Origin 1`) bằng truy bắt điểm [[Osnap]].
4. Bấm chuột chọn điểm đo thứ hai (`Origin 2`).
5. Di chuột kéo đường kích thước ra xa đối tượng rồi bấm chuột trái định vị trí đặt đường gióng.
*(Mẹo: Khi lệnh hỏi điểm thứ nhất, nhấn [Enter] lần nữa để vào chế độ chọn trực tiếp đối tượng, sau đó chỉ cần bấm chọn một đoạn thẳng để đo ngay).*

### 2. Đo đoạn thẳng xiên với DIMALIGNED
1. Gõ `DAL` hoặc `DIMALIGNED` rồi nhấn [Enter].
2. Bấm chọn điểm đầu và điểm cuối của cạnh xiên.
3. Kéo đường kích thước vuông góc với cạnh xiên đến vị trí thông thoáng rồi bấm chuột.

### 3. Đo bán kính, đường kính và góc
- **Đo bán kính:** Gõ `DRA` [Enter], bấm chọn cung cong hoặc hình tròn, kéo đường dẫn ra vị trí thích hợp.
- **Đo đường kính:** Gõ `DDI` [Enter], bấm chọn đường tròn, kéo mũi tên đường kính hiển thị ký hiệu `Ø`.
- **Đo góc:** Gõ `DAN` [Enter], bấm chọn đoạn thẳng thứ nhất, bấm chọn đoạn thẳng thứ hai, di chuột trong góc mở cần đo và bấm định vị trí.

## Tuỳ chọn và mẹo ghi kích thước nhanh

Khi đang kéo vị trí đặt kích thước, thanh nhắc lệnh hiển thị các tùy chọn hữu ích:
- **`Mtext` (M):** Mở cửa sổ soạn thảo văn bản để nhập thêm dung sai, chữ ghi chú hoặc thay đổi tiền tố/hậu tố kích thước.
- **`Text` (T):** Nhập trực tiếp chuỗi ký tự hiển thị trên thanh dòng lệnh mà không mở hộp thoại.
- **`Angle` (A):** Xoay góc nghiêng của con số kích thước so với đường gióng.

> [!TIP]
> Luôn gán layer riêng cho kích thước (chẳng hạn nét mảnh 0.15mm hoặc 0.18mm) để khi in bản vẽ, đường kích thước không lấn át đường bao chính của chi tiết gia công.

> [!TIP]
> Nhấn [Enter] ngay khi bắt đầu lệnh `DIMLINEAR` hoặc `DIMALIGNED` để chuyển con trỏ sang hình ô vuông (Pickbox). Lúc này chỉ cần bấm trúng đoạn thẳng cần đo, AutoCAD tự tính toán hai đầu mút cực kỳ chính xác và nhanh gọn.

## Tự kiểm tra

```quiz
id: q-ac-05-01-1
type: single
question: "Khác biệt cơ bản giữa DIMLINEAR (DLI) và DIMALIGNED (DAL) khi đo đoạn thẳng xiên là gì?"
options:
  - text: "DLI đo khoảng cách chiếu ngang hoặc đứng, còn DAL đo khoảng cách song song với cạnh xiên"
    correct: true
    why: "DIMLINEAR chỉ chiếu theo trục X hoặc Y, trong khi DIMALIGNED đo theo hướng thực của đối tượng."
  - text: "DLI dùng cho hình tròn, còn DAL dùng cho hình chữ nhật"
    correct: false
    why: "Cả hai lệnh đều dùng để đo đoạn thẳng."
  - text: "DLI chỉ dùng được trên không gian 3D, DAL dùng trên 2D"
    correct: false
    why: "Cả hai lệnh đều hoạt động tốt trong không gian bản vẽ 2D."
  - text: "DLI cho phép đổi màu chữ, DAL thì không đổi màu được"
    correct: false
    why: "Màu sắc kích thước phụ thuộc vào Layer và Dimstyle, không phụ thuộc vào lệnh đo."
explain: "DIMLINEAR luôn gióng theo phương tọa độ thẳng đứng hoặc nằm ngang. Để lấy chiều dài thực của một cạnh nghiêng bất kỳ, bạn bắt buộc phải dùng DIMALIGNED."
```

```quiz
id: q-ac-05-01-2
type: single
question: "Khi dùng lệnh DIMDIAMETER để đo đường tròn, ký hiệu nào sẽ tự động được thêm trước con số?"
options:
  - text: "Ký hiệu R"
    correct: false
    why: "Ký hiệu R là bán kính, xuất hiện khi dùng lệnh DIMRADIUS."
  - text: "Ký hiệu đường kính Ø"
    correct: true
    why: "AutoCAD tự động gán mã %%c tương ứng với ký hiệu Ø cho đường kính."
  - text: "Ký hiệu dấu cộng trừ ±"
    correct: false
    why: "Dấu ± chỉ xuất hiện khi cài đặt dung sai (Tolerance)."
  - text: "Ký hiệu góc độ °"
    correct: false
    why: "Ký hiệu độ dùng cho lệnh DIMANGULAR."
explain: "AutoCAD quy chuẩn bán kính có tiền tố R (Radius) và đường kính có tiền tố Ø (Diameter)."
```

```quiz
id: q-ac-05-01-3
type: truefalse
question: "Nhấn Enter ngay khi bắt đầu lệnh DIMLINEAR cho phép bạn bấm chọn thẳng đoạn thẳng mà không cần bắt từng điểm đầu cuối."
answer: false
explain: "Khi có sẵn đoạn thẳng hoặc cung tròn độc lập, nhấn Enter để chọn đối tượng nhanh hơn nhiều so với việc bắt điểm Endpoint 2 lần."
```

## Lỗi thường gặp

- **Kích thước đo ra quá bé hoặc quá to:** Chữ số kích thước li ti như dấu chấm hoặc to che hết bản vẽ. Do tỉ lệ kích thước trong [[Dimstyle]] chưa khớp với tỉ lệ bản vẽ (khắc phục bằng biến `DIMSCALE` hoặc dùng `Annotative`).
- **Bắt nhầm điểm đo:** Bấm nhầm điểm gióng của đường kích thước cũ thay vì điểm thực tế của chi tiết. Cần phóng to vùng quan sát và kiểm tra chế độ bắt điểm `Endpoint` / `Intersection`.
- **Số kích thước hiển thị số lẻ quá nhiều:** Chẳng hạn `100.0000` làm rối mắt bản vẽ. Cần điều chỉnh số chữ số thập phân (`Precision`) trong hộp thoại quản lý kiểu kích thước.

## Bài tập thực hành

- [ ] Mở bản vẽ trống từ template `acadiso.dwt`. Vẽ một hình chữ nhật kích thước 120 x 80 mm bằng lệnh `RECTANG`. <!-- expect: RECTANG -->
- [ ] Dùng lệnh `DIMLINEAR`, đo chiều dài cạnh ngang 120mm và cạnh đứng 80mm. <!-- expect: DIMLINEAR -->
- [ ] Vẽ đường thẳng xiên nối góc từ toạ độ 0,0 đến @100<45 bằng `LINE`. <!-- expect: LINE -->
- [ ] Đo chiều dài thực của đường thẳng xiên vừa vẽ bằng lệnh `DIMALIGNED`. <!-- expect: DIMALIGNED -->
- [ ] Vẽ hình tròn bán kính 25mm bằng `CIRCLE`, đo bán kính bằng `DIMRADIUS` và đo đường kính bằng `DIMDIAMETER`. <!-- expect: DIMRADIUS -->

## Nguồn tham khảo

```links
- title: "Tài liệu lệnh DIMLINEAR chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=DIMLINEAR"
  kind: official
- title: "Tài liệu lệnh DIMALIGNED chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=DIMALIGNED"
  kind: official
```
