---
id: ac-08-03
title: Tra cứu thông số hình học siêu tốc với bộ công cụ Inquiry
category: Nâng cao năng suất
tags: [measuregeom, dist, area, id, list, do-dac, nang-suat]
level: beginner
minutes: 20
needs: [ac-08-01]
appVersions: ['2024', '2025']
edition: all
---
# Tra cứu thông số hình học siêu tốc với bộ công cụ Inquiry

> **Mục tiêu:**
> - Sử dụng công cụ đo nhanh trực quan `MEASUREGEOM` (Quick Measure) để xem tức thì kích thước chỉ bằng thao tác rê chuột.
> - Đo khoảng cách, toạ độ tương đối và góc với `DIST`, lấy toạ độ điểm tuyệt đối với `ID`.
> - Tính toán diện tích phức tạp (cộng/trừ diện tích lỗ khoét) với lệnh `AREA` và tra cứu thuộc tính với `LIST`.

## Nhu cầu đo kiểm tra tạm thời mà không vẽ thêm nét rác

Trong quá trình thiết kế, bạn liên tục cần kiểm tra:
- Khoảng cách lọt lòng giữa hai bức tường là bao nhiêu mét?
- Cột bê tông này đang nằm ở toạ độ X, Y nào trong hệ toạ độ công trình?
- Diện tích khu đất sau khi trừ đi diện tích sân vườn và hồ bơi còn lại bao nhiêu $m^2$?

Nhiều người mới học thường dùng lệnh `DIMLINEAR` đo thử để nhìn con số, sau đó lại phải bấm chuột xóa đường kích thước đó đi. Cách làm này vừa chậm chạp vừa rất dễ quên xóa, để lại các đường kích thước rác nằm đè lên bản vẽ!

AutoCAD cung cấp cụm công cụ **Tra cứu thông số hình học (Inquiry & Measurement)** chuyên biệt: Cho phép bạn kiểm tra toàn bộ kích thước, bán kính, chu vi, diện tích và tọa độ trong nháy mắt mà **hoàn toàn không tạo ra bất kỳ đối tượng nào trên bản vẽ**!

![Bộ công cụ đo đạc hình học nhanh](media/ac-08-03-measuregeom.svg)

```hotspots
image: media/ac-08-03-measuregeom.svg
alt: Các công cụ đo đạc tra cứu hình học nhanh trong AutoCAD
layout: central
points:
  - id: spot-1
    x: 23
    y: 35
    title: Quick Measure (MEASUREGEOM)
    text: "Rê chuột vào khoảng trống: Kích thước ngang dọc và bán kính tự động hiện lên màn hình."
  - id: spot-2
    x: 23
    y: 75
    title: Kích thước trực quan
    text: "Hiển thị màu cam nổi bật và biến mất ngay khi di chuyển chuột đi nơi khác."
  - id: spot-3
    x: 75
    y: 30
    title: Lệnh DIST (DI)
    text: "Đo khoảng cách thực giữa 2 điểm kèm góc nghiêng và độ chênh lệch dX, dY."
  - id: spot-4
    x: 75
    y: 70
    title: Lệnh AREA (AA)
    text: "Tính toán diện tích và chu vi vùng khép kín với chế độ cộng/trừ diện tích thông minh."
```

## Các công cụ tra cứu cốt lõi từng bước

### 1. Tính năng đo thông minh Quick Measure (MEASUREGEOM)
Lệnh tắt: `MEA` hoặc `MEASUREGEOM`:
1. Gõ `MEA` rồi nhấn [Enter] (hoặc bấm nút **Quick** trong cụm công cụ *Utilities* trên thẻ Home).
2. Di chuột nhẹ nhàng vào bên trong bất kỳ căn phòng hay chi tiết cơ khí nào:
   - Các đường kích thước màu cam sẽ lập tức phóng ra đo tự động khoảng cách giữa các mép tường lân cận.
   - Các góc vuông 90° sẽ hiển thị biểu tượng góc vuông nhỏ màu xanh.
   - Các cung tròn và lỗ khoan sẽ tự động hiển thị bán kính `R`.
3. Nhấn [Enter] hoặc [Esc] để thoát lệnh. Cực kỳ trực quan và tiết kiệm thời gian!

### 2. Đo khoảng cách và góc nghiêng với lệnh DIST (DI)
Khi bạn cần đo khoảng cách chính xác giữa 2 điểm bất kỳ trong không gian:
1. Gõ `DI` hoặc `DIST` rồi nhấn [Enter].
2. Bấm chọn điểm mốc thứ nhất bằng truy bắt điểm [[Osnap]].
3. Bấm chọn điểm mốc thứ hai.
4. Thanh dòng lệnh sẽ xuất ra toàn bộ báo cáo chi tiết:
   - `Distance`: Khoảng cách thực giữa 2 điểm (ví dụ: `2500.0`).
   - `Angle in XY Plane`: Góc nghiêng so với phương ngang (ví dụ: `45°`).
   - `Delta X`, `Delta Y`, `Delta Z`: Độ chênh lệch khoảng cách chiếu theo từng trục toạ độ.

### 3. Lấy toạ độ tuyệt đối định vị công trình với lệnh ID
1. Gõ `ID` rồi nhấn [Enter].
2. Bấm chọn một giao điểm tim trục hoặc góc ranh đất.
3. Thanh dòng lệnh hiển thị ngay toạ độ trắc địa tuyệt đối:
   `X = 15420.5000  Y = 28350.2000  Z = 0.0000`.

### 4. Tính toán diện tích phức tạp với lệnh AREA (AA)
1. Gõ `AA` hoặc `AREA` rồi nhấn [Enter].
- **Cách 1 (Vật thể có sẵn):** Gõ `O` (Object), bấm chọn đường bao khép kín `PLINE` hoặc `REGION`. Màn hình hiển thị ngay diện tích `Area` và chu vi `Perimeter`.
- **Cách 2 (Cộng/Trừ diện tích - Add / Subtract mode):**
  - Gõ `A` (Add area) > gõ `O` > bấm chọn khu đất tổng thể (diện tích được cộng vào bộ nhớ tạm, tô sáng màu xanh lá).
  - Gõ `S` (Subtract area) > gõ `O` > bấm chọn hình ngôi nhà và hồ bơi (diện tích bị trừ đi, tô sáng màu đỏ).
  - Nhấn [Enter]: AutoCAD tính ra ngay diện tích đất trống còn lại chính xác tuyệt đối!

### 5. Xuất hồ sơ lý lịch đối tượng với lệnh LIST (LI)
1. Gõ `LI` hoặc `LIST` rồi nhấn [Enter].
2. Bấm chọn bất kỳ đối tượng nào (đoạn thẳng, hình tròn, block, spline), nhấn [Enter].
3. Một cửa sổ văn bản xuất hiện hiển thị toàn bộ thuộc tính "chân tơ kẽ tóc": Layer, màu sắc, toạ độ tâm, bán kính, chu vi, diện tích, góc nghiêng...

> [!TIP]
> Nhấn phím chức năng [F2] để mở rộng cửa sổ lịch sử dòng lệnh (Command History) giúp đọc các thông số kết quả đo của lệnh `DIST` và `LIST` rõ ràng hơn mà không bị che khuất.

## Tự kiểm tra

```quiz
id: q-ac-08-03-1
type: single
question: "Lệnh tắt ngắn nhất và phổ biến nhất để đo khoảng cách và góc giữa hai điểm trong AutoCAD là gì?"
options:
  - text: "DI (lệnh DIST)"
    correct: true
    why: "DI là lệnh tắt tiêu chuẩn của lệnh DIST."
  - text: "DLI"
    why: "DLI là DIMLINEAR dùng để vẽ đường kích thước cố định."
  - text: "DO"
    why: "DO là lệnh DONUT vẽ hình vành khăn."
  - text: "DT"
    why: "DT là lệnh DTEXT viết chữ đơn dòng."
explain: "Sử dụng phím tắt DI để đo nhanh khoảng cách giữa hai mốc mà không tạo ra đường kích thước rác."
```

```quiz
id: q-ac-08-03-2
type: single
question: "Để tính diện tích một khu đất khép kín và tự động trừ đi diện tích của hồ bơi bên trong, lệnh AREA cung cấp cặp tùy chọn nào?"
options:
  - text: "Add area (gõ A) và Subtract area (gõ S)"
    correct: true
    why: "Chế độ Add/Subtract area cho phép cộng dồn hoặc khấu trừ các vùng diện tích phức tạp."
  - text: "Plus và Minus"
    why: "AutoCAD không dùng từ khóa Plus/Minus cho lệnh AREA."
  - text: "TRIM và EXTEND"
    why: "TRIM/EXTEND là lệnh cắt xén hình học."
  - text: "UNION và SUBTRACT"
    why: "UNION/SUBTRACT là lệnh boolean cho khối 3D solid."
explain: "Dùng tùy chọn Add area để chọn vùng tổng và Subtract area để khoét trừ các lỗ thủng bên trong."
```

```quiz
id: q-ac-08-03-3
type: truefalse
question: "Tính năng Quick Measure trong lệnh MEASUREGEOM cho phép xem tức thì kích thước các đoạn thẳng lân cận chỉ bằng cách rê chuột mà không cần bấm click chuột."
answer: true
explain: "Quick Measure là tính năng hiện đại cực mạnh giúp người vẽ kiểm tra nhanh toàn bộ không gian phòng chỉ trong vài giây lướt chuột."
```

## Lỗi thường gặp

- **Tính lệnh AREA bấm từng điểm nhưng bị sai kết quả:** Do bấm bắt điểm không chuẩn hoặc đường bao bị hở. Khắc phục: Dùng lệnh `JOIN` hoặc `BOUNDARY` (BO) để biến đường bao thành một Polyline khép kín trước, sau đó dùng `AREA` với tùy chọn `Object` (gõ `O`).
- **Số diện tích quá to làm hoa mắt:** Ví dụ phòng $20 m^2$ nhưng màn hình hiện `20000000` (đơn vị $mm^2$). Hãy nhẩm tính lùi dấu phẩy 6 chữ số để đổi sang $m^2$.

## Bài tập thực hành

- [ ] Dùng `RECTANG` vẽ một hình chữ nhật kích thước 5000 x 3000 mm. <!-- expect: RECTANG -->
- [ ] Dùng `CIRCLE` vẽ một hình tròn bán kính 800mm ở giữa hình chữ nhật. <!-- expect: CIRCLE -->
- [ ] Gõ lệnh `DIST` (hoặc `DI`), đo khoảng cách giữa hai góc đối diện của hình chữ nhật. <!-- expect: DIST -->
- [ ] Gõ lệnh `ID`, bấm kiểm tra toạ độ tuyệt đối tâm của hình tròn. <!-- expect: ID -->
- [ ] Gõ lệnh `AREA` (hoặc `AA`), dùng tuỳ chọn `Object` đo diện tích hình chữ nhật và hình tròn. <!-- expect: AREA -->
- [ ] Gõ `MEASUREGEOM` (hoặc `MEA`), rê chuột qua khoảng trống giữa hình chữ nhật và đường tròn để quan sát kích thước tự động. <!-- expect: MEASUREGEOM -->

## Nguồn tham khảo

```links
- title: "Công cụ đo MEASUREGEOM từ Autodesk Knowledge Network"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=MEASUREGEOM"
  kind: official
- title: "Tính diện tích với lệnh AREA từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=AREA"
  kind: official
```
