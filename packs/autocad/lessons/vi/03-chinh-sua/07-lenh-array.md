---
id: ac-03-07
title: Sao chép mảng đối tượng với lệnh ARRAY
category: Chỉnh sửa
tags: [array, arrayrect, arraypolar, arraypath, sao-chep-mang, mang-tron, mang-luoi]
level: beginner
minutes: 20
needs: [ac-03-02]
appVersions: ['2024', '2025']
edition: all
---
# Sao chép mảng đối tượng với lệnh ARRAY

> **Mục tiêu:**
> - Phân biệt và ứng dụng thành thạo 3 loại mảng trong AutoCAD: Rectangular, Polar và Path Array.
> - Thiết lập số lượng phần tử (Items), số hàng/cột (Rows/Columns) và cự ly khoảng cách giữa các phần tử.
> - Quản lý tính năng mảng liên kết (Associative Array) và chỉnh sửa thông số linh hoạt sau khi vẽ.

## Lệnh này làm gì và khi nào dùng

Khi bản vẽ có hàng chục hoặc hàng trăm chi tiết giống hệt nhau được sắp xếp theo một trật tự toán học nghiêm ngặt (lưới bàn ghế trong hội trường, hàng cột nhà xưởng, bậc cầu thang xoắn ốc, nan hoa bánh xe hay hệ thống lỗ bu lông mặt bích), việc dùng lệnh COPY thông thường là bất khả thi.

Tính năng [[Sao chép mảng]] (Array) tự động nhân bản đối tượng theo 3 dạng hình học:
- **Rectangular Array (`ARRAYRECT`):** [[Mảng chữ nhật]] phân bố đối tượng theo ma trận hàng (Rows) và cột (Columns).
- **Polar Array (`ARRAYPOLAR`):** [[Mảng tròn xoay]] phân bố đều các đối tượng quay xung quanh một tâm tròn theo góc quét (thường là 360°).
- **Path Array (`ARRAYPATH`):** Phân bố các đối tượng chạy dọc theo một đường dẫn bất kỳ (đường cong Polyline, Spline hay cung tròn).

Đối tượng Array trong AutoCAD là mảng tham số liên kết (Associative). Sau khi tạo xong, bạn vẫn có thể nhấp chuột vào mảng để thay đổi số lượng hoặc khoảng cách bất kỳ lúc nào.

```hotspots
image: media/ac-03-07-array-types.svg
alt: Sơ đồ minh hoạ 3 loại mảng sao chép trong AutoCAD gồm Rectangular, Polar và Path Array
layout: central
points:
  - id: array-rect
    x: 18
    y: 35
    title: 1. Rectangular Array (Ma trận hàng cột)
    text: Sao chép theo các cột (Columns) và các hàng (Rows) với cự ly Between xác định.
    quiz: q-ac-03-07-1
  - id: array-polar
    x: 50
    y: 35
    title: 2. Polar Array (Mảng tròn xoay)
    text: Sao chép quay quanh một tâm mốc. Thiết lập số lượng Items và góc quét Fill Angle (ví dụ 6 lỗ tròn 360°).
    quiz: q-ac-03-07-2
  - id: array-path
    x: 82
    y: 35
    title: 3. Path Array (Theo đường dẫn cong)
    text: Rải đều các đối tượng bám dọc theo đường cong Polyline hoặc Spline.
```

## Cách dùng từng bước

1. **Tạo mảng chữ nhật (Rectangular Array):**
   - Vẽ một hình chữ nhật nhỏ làm phần tử mẫu.
   - Gõ `ARRAYRECT` (hoặc `ARRAY` > chọn `Rectangular`) rồi nhấn [Enter].
   - Nhấp chọn hình chữ nhật rồi nhấn [Enter].
   - Một thanh Ribbon theo ngữ cảnh *Array Creation* sẽ xuất hiện:
     - *Columns:* Nhập số cột (ví dụ `4`).
     - *Between (Columns):* Khoảng cách giữa các cột (ví dụ `50`).
     - *Rows:* Nhập số hàng (ví dụ `3`).
     - *Between (Rows):* Khoảng cách giữa các hàng (ví dụ `40`).
   - Bấm **Close Array** để xác nhận.
2. **Tạo mảng tròn xoay (Polar Array):**
   - Vẽ một đường tròn lớn tâm `0,0` và một đường tròn nhỏ tại góc trên để làm lỗ bu lông.
   - Gõ `ARRAYPOLAR` rồi nhấn [Enter].
   - Chọn đường tròn nhỏ rồi [Enter].
   - Chọn tâm xoay (Specify center point of array): Dùng Osnap Center bấm vào tâm `0,0`.
   - Trên Ribbon, ô *Items* nhập số lượng (ví dụ `8`).
   - Ô *Fill* mặc định `360` (quét đủ một vòng tròn khép kín).
   - Bấm **Close Array**.
3. **Hiệu chỉnh mảng sau khi tạo:**
   - Nhấp chuột trái vào bất kỳ phần tử nào của mảng: Toàn bộ mảng sẽ sáng lên và thanh Ribbon Array mở lại để bạn sửa thông số.
   - Kéo các mũi tên Grip để tăng thêm số hàng/cột một cách trực quan.

## Tuỳ chọn và mẹo

> [!TIP]
> Luôn giữ tính năng **Associative** bật khi tạo Array. Điều này giúp bạn có thể đổi từ 6 lỗ bu lông lên 8 lỗ bu lông chỉ bằng 1 giây gõ lại thông số trên Ribbon mà không cần xoá đi vẽ lại.

> [!TIP]
> Nếu bạn muốn biến một mảng Array thành các đối tượng độc lập riêng lẻ để xoá bớt một vài phần tử cá biệt, hãy dùng lệnh `EXPLODE` (phím tắt `X`) để rã mảng ra.

## Tự kiểm tra

```quiz
id: q-ac-03-07-1
type: single
question: Để rải đều 6 lỗ bu lông phân bố cách đều nhau quay quanh tâm một mặt bích tròn 360 độ, bạn sử dụng loại Array nào?
options:
  - text: Polar Array (ARRAYPOLAR)
    correct: true
    why: Polar Array chuyên dùng cho các đối tượng xoay đều quanh một điểm tâm
  - text: Rectangular Array (ARRAYRECT)
    why: Rectangular Array phân bố theo lưới hàng và cột vuông góc
  - text: Path Array (ARRAYPATH)
    why: Path Array dùng khi có đường dẫn cong tự do
  - text: Linear Array
    why: AutoCAD không có loại Linear Array riêng biệt
explain: "Polar Array (mảng tròn xoay) phân bố đều các phần tử xung quanh một điểm tâm với góc quét chỉ định (mặc định 360 độ), là công cụ hoàn hảo để vẽ các lỗ bu lông đối xứng."
tags: [array, polar, bu-long]
```

```quiz
id: q-ac-03-07-2
type: single
question: Khi tính năng "Associative" được bật trong lệnh ARRAY, mảng đối tượng tạo ra có đặc điểm gì?
options:
  - text: Toàn bộ các phần tử liên kết với nhau thành một khối tham số, có thể chỉnh sửa lại số lượng và cự ly bất kỳ lúc nào
    correct: true
    why: Associative Array lưu giữ các tham số toán học để chỉnh sửa linh hoạt sau này
  - text: Mảng sẽ bị khoá vĩnh viễn không thể chỉnh sửa
    why: Ngược lại, Associative giúp sửa đổi rất dễ dàng
  - text: Tự động biến thành các đoạn thẳng rời rạc
    why: Muốn biến thành các đoạn rời phải dùng lệnh EXPLODE
  - text: Tự động đổi sang layer khác
    why: Associative không đổi layer của đối tượng
explain: "Mảng liên kết (Associative Array) hoạt động như một khối tham số thông minh, cho phép bạn nhấp chọn để cập nhật lại số lượng Items, Rows, Columns trên Ribbon."
tags: [array, associative]
```

```quiz
id: q-ac-03-07-3
type: truefalse
question: Sau khi đã tạo một mảng liên kết (Associative Array), bạn có thể dùng lệnh EXPLODE để rã mảng thành từng đối tượng riêng lẻ.
answer: true
explain: "Lệnh EXPLODE (phím tắt X) sẽ phá vỡ liên kết tham số của khối Array, đưa toàn bộ các phần tử bên trong trở về trạng thái các đối tượng độc lập ban đầu."
tags: [array, explode]
```

```quiz
id: q-ac-03-07-4
type: hotspot
question: Bấm vào vị trí minh hoạ mảng tròn xoay Polar Array trên sơ đồ.
use: hotspots
answer: array-polar
explain: "Mảng tròn xoay Polar Array nằm ở cột giữa của sơ đồ, gồm các đường tròn nhỏ phân bố xoay quanh tâm mốc."
tags: [array, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Không thể xoá riêng một phần tử đơn lẻ trong mảng (bấm vào là chọn cả mảng).
  - *Nguyên nhân:* Mảng đang ở chế độ Associative nên toàn bộ mảng là một thực thể duy nhất.
  - *Cách sửa:* Đè giữ phím [Ctrl] rồi nhấp vào riêng phần tử đó để xoá/di chuyển, hoặc dùng lệnh `EXPLODE` để rã toàn bộ mảng ra.
- **Triệu chứng:** Polar Array xoay sai hướng hoặc các hình bị méo nghiêng theo góc quay.
  - *Nguyên nhân:* Tuỳ chọn *Rotate Items* trên Ribbon đang bị bật hoặc tắt ngược với ý muốn thiết kế.
  - *Cách sửa:* Bấm vào mảng và tích hoặc bỏ tích ô *Rotate Items* trên thanh Ribbon.

## Bài tập thực hành

- [ ] Gõ `CIRCLE` vẽ một đường tròn bán kính `80` tại gốc toạ độ `0,0`. <!-- expect: CIRCLE -->
- [ ] Gõ `CIRCLE` vẽ một lỗ tròn nhỏ bán kính `10` tại điểm góc phần tư đỉnh (0, 80). <!-- expect: CIRCLE -->
- [ ] Gõ `ARRAYPOLAR`, chọn lỗ tròn nhỏ và chọn tâm xoay tại `0,0`. <!-- expect: ARRAYPOLAR -->
- [ ] Đặt số lượng *Items* thành `6` và nhấn Enter để hoàn thành mảng 6 lỗ bu lông tròn xoay.
- [ ] Nhấp chọn mảng vừa tạo và thử đổi số lượng Items từ 6 lên `8` trực tiếp trên Ribbon.

## Nguồn tham khảo

```links
- title: Lệnh ARRAY và các kiểu mảng sao chép (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=ARRAY+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về Rectangular, Polar và Path Array trong AutoCAD
- title: Chỉnh sửa mảng liên kết Associative Array (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=ARRAYEDIT+Command
  kind: official
  lang: en
  note: Hướng dẫn thay thế phần tử, chỉnh khoảng cách và sửa mảng tham số
```
