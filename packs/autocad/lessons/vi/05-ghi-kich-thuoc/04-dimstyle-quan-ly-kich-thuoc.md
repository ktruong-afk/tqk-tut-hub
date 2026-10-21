---
id: ac-05-04
title: Quản lý kiểu kích thước chuyên nghiệp với DIMSTYLE
category: Ghi kích thước
tags: [dimstyle, dimension, style, tieu-chuan]
level: intermediate
minutes: 25
needs: [ac-05-01]
appVersions: ['2024', '2025']
edition: all
---
# Quản lý kiểu kích thước chuyên nghiệp với DIMSTYLE

> **Mục tiêu:**
> - Sử dụng hộp thoại `DIMSTYLE` để tạo và hiệu chỉnh các kiểu kích thước theo tiêu chuẩn kỹ thuật (TCVN / ISO).
> - Làm chủ các thông số cốt lõi trong các thẻ Lines, Symbols and Arrows, Text, Fit và Primary Units.
> - Thiết lập số chữ số thập phân, phần nghìn và tỷ lệ thu phóng tổng thể `DIMSCALE`.

## Trung tâm điều khiển kích thước: Dimension Style Manager

Nếu bản vẽ của bạn có mũi tên quá to, chữ quá bé, hoặc số đo bị thừa đuôi `.0000`, bạn không thể đi sửa thủ công từng đường kích thước một. Thay vào đó, AutoCAD quản lý toàn bộ hình dáng, cỡ chữ, khoảng cách và đơn vị đo thông qua **Kiểu kích thước ([[Dimstyle]])**.

Chỉ cần thay đổi một thông số trong Dimstyle hiện hành, tất cả hàng nghìn đường kích thước thuộc kiểu đó trên toàn bộ bản vẽ sẽ tự động cập nhật ngay tức khắc.

Để mở trình quản lý kiểu kích thước, bạn gõ lệnh `DIMSTYLE` (lệnh tắt chỉ 1 chữ cái duy nhất: `D`) rồi nhấn [Enter].

![Hộp thoại DIMSTYLE và các thẻ thông số](media/ac-05-04-dimstyle-dialog.svg)

```hotspots
image: media/ac-05-04-dimstyle-dialog.svg
alt: Các thẻ thiết lập chính trong hộp thoại Dimension Style Manager
layout: central
points:
  - id: spot-1
    x: 12
    y: 22
    title: Thẻ Lines (Đường nét)
    text: Quản lý màu sắc, độ dày, khoảng nhô và thụt lề của Dimension Line và Extension Line.
  - id: spot-2
    x: 28
    y: 22
    title: Thẻ Symbols and Arrows
    text: Chọn hình dạng đầu mũi tên (Closed filled, Architectural tick, Dot...) và kích thước mũi tên.
  - id: spot-3
    x: 44
    y: 22
    title: Thẻ Text (Chữ số)
    text: Chọn TextStyle, màu sắc, chiều cao chữ số (Text height) và vị trí nằm trên đường gióng.
  - id: spot-4
    x: 60
    y: 22
    title: Thẻ Fit (Thu phóng & Bố trí)
    text: Xử lý khi chữ quá hẹp, và chứa hệ số phóng to tổng thể 'Use overall scale of' (DIMSCALE).
  - id: spot-5
    x: 76
    y: 22
    title: Thẻ Primary Units (Đơn vị đo)
    text: Chọn số chữ số sau dấu phẩy (Precision), đơn vị Decimal, và khử số 0 vô nghĩa (Zero suppression).
```

## Cách dùng từng bước

### 1. Tạo một kiểu kích thước mới
1. Gõ `D` hoặc `DIMSTYLE` rồi nhấn [Enter] để mở hộp thoại.
2. Tại danh sách bên trái, chọn kiểu chuẩn `ISO-25` (hệ mét).
3. Bấm nút **New...** bên phải.
4. Nhập tên kiểu mới (ví dụ: `KT-CO-KHI-1-1` hoặc `KT-KIEN-TRUC-1-100`). Bấm **Continue**.

### 2. Thiết lập các thông số cơ bản chuẩn TCVN / ISO
1. **Thẻ Lines:**
   - Đặt màu sắc (`Color`) và nét vẽ (`Lineweight`) theo `ByBlock` hoặc `ByLayer`.
   - `Extend beyond dim lines`: Đặt `1.5` đến `2.0` mm (độ nhô của đường gióng quá đường kích thước).
   - `Offset from origin`: Đặt `1.5` đến `2.0` mm (khoảng hở chân đường gióng so với điểm đo trên vật thể).
   - `Baseline spacing`: Đặt `8.0` mm (khoảng cách khi đo song song).
2. **Thẻ Symbols and Arrows:**
   - `First` / `Second`: Chọn `Closed filled` (mũi tên tam giác đặc cho cơ khí) hoặc `Architectural tick` (gạch chéo cho kiến trúc xây dựng).
   - `Arrow size`: Đặt từ `2.5` đến `3.0` mm.
   - `Center marks`: Chọn `Mark` kích thước `2.0` mm.
3. **Thẻ Text:**
   - `Text style`: Chọn kiểu chữ kỹ thuật (đã tạo ở lệnh `STYLE`).
   - `Text height`: Đặt `2.5` mm (kích thước chữ khi in ra giấy).
   - `Text placement` > `Vertical`: Chọn `Above` (chữ nằm phía trên đường kích thước).
   - `Text alignment`: Chọn `Aligned with dimension line` (chữ luôn song song với đường kích thước).
4. **Thẻ Primary Units:**
   - `Unit format`: `Decimal`.
   - `Precision`: Chọn `0` (nếu không cần số thập phân) hoặc `0.0` (lấy 1 chữ số thập phân).
   - `Decimal separator`: Chọn dấu chấm `.` (Period) hoặc phẩy `,` (Comma).
   - `Zero suppression`: Đánh dấu tick vào ô `Trailing` để tự động giấu các số 0 thừa phía sau (ví dụ `100.0` sẽ hiển thị gọn thành `100`).
5. Bấm **OK**, sau đó bấm **Set Current** và **Close** để áp dụng.

## Tuỳ chọn và mẹo xử lý tỉ lệ với DIMSCALE

Trong thẻ **Fit**, ô **Use overall scale of** (tương ứng với biến hệ thống `DIMSCALE`) là bí quyết quan trọng nhất khi vẽ bản vẽ nhiều tỉ lệ:
- Nếu in bản vẽ tỉ lệ 1:1, đặt giá trị là `1`. Chiều cao chữ in ra giấy sẽ đúng chuẩn 2.5mm.
- Nếu in bản vẽ tỉ lệ 1:50, đặt giá trị là `50`. Chiều cao chữ trong không gian vẽ sẽ tự phóng to lên thành $2.5 \times 50 = 125$ mm, để khi in thu nhỏ 50 lần về giấy A3, con số đo lại đúng 2.5mm!

> [!TIP]
> Không bao giờ chỉnh sửa chiều cao chữ trực tiếp ở từng kích thước đơn lẻ qua bảng Properties. Luôn quy chuẩn trong Dimstyle để đảm bảo toàn bộ bản vẽ đồng nhất và chuyên nghiệp.

> [!TIP]
> Nút **Override** trong hộp thoại Dimstyle cho phép tạo các thông số ghi đè tạm thời cho các kích thước sắp vẽ mà không làm hỏng kiểu kích thước gốc.

## Tự kiểm tra

```quiz
id: q-ac-05-04-1
type: single
question: "Để mở hộp thoại Dimension Style Manager, lệnh tắt nhanh nhất trong AutoCAD là gì?"
options:
  - text: "Lệnh D"
    correct: true
    why: "Phím D là alias ngắn gọn và phổ biến nhất của DIMSTYLE."
  - text: "Lệnh DS"
    correct: false
    why: "DS là Drafting Settings (cài đặt Osnap, Grid)."
  - text: "Lệnh DI"
    correct: false
    why: "DI là DIST (đo khoảng cách tạm thời)."
  - text: "Lệnh ST"
    correct: false
    why: "ST là STYLE (quản lý kiểu chữ Text Style)."
explain: "Gõ D rồi nhấn Enter là cách mọi kỹ sư CAD truy cập hộp thoại quản lý kích thước."
```

```quiz
id: q-ac-05-04-2
type: single
question: "Trong thẻ Primary Units, tuỳ chọn 'Trailing' dưới mục Zero suppression có tác dụng gì?"
options:
  - text: "Khử các số 0 vô nghĩa ở phần đuôi thập phân (ví dụ 50.00 thành 50)"
    correct: true
    why: "Trailing loại bỏ các chữ số 0 dư thừa sau dấu thập phân giúp bản vẽ gọn gàng."
  - text: "Thêm dấu cộng trừ sai số vào sau kích thước"
    correct: false
    why: "Dung sai nằm trong thẻ Tolerances."
  - text: "Đổi đơn vị từ mm sang inch"
    correct: false
    why: "Đơn vị thay đổi ở Unit format hoặc Alternate Units."
  - text: "Tự động làm tròn số lên số nguyên chẵn gần nhất"
    correct: false
    why: "Làm tròn được quản lý bởi Round off."
explain: "Tick chọn Trailing giúp hiển thị 25.5 khi có số lẻ, nhưng hiển thị 25 thay vì 25.00 khi là số nguyên tròn."
```

```quiz
id: q-ac-05-04-3
type: multi
question: "Những thông số nào dưới đây nằm trong thẻ Lines của hộp thoại Modify Dimension Style? (Chọn 2 đáp án)"
options:
  - text: "Extend beyond dim lines (khoảng nhô của đường gióng)"
    correct: true
    why: "Quy định độ nhô vượt quá đường kích thước của 2 đường gióng."
  - text: "Offset from origin (khoảng cách hở chân đường gióng so với vật thể)"
    correct: true
    why: "Khoảng hở tránh để đường gióng kích thước dính liền vào nét vẽ của vật thể."
  - text: "Text height (chiều cao chữ số)"
    correct: false
    why: "Text height nằm trong thẻ Text."
  - text: "Arrow size (kích thước đầu mũi tên)"
    correct: false
    why: "Arrow size nằm trong thẻ Symbols and Arrows."
explain: "Thẻ Lines phụ trách hoàn toàn thuộc tính hình học của đường kích thước (Dimension lines) và đường gióng (Extension lines)."
```

## Lỗi thường gặp

- **Chân đường kích thước dính chặt vào nét vẽ chi tiết:** Giá trị `Offset from origin` bị đặt bằng 0. Khi in ra, đường gióng và nét chi tiết bị liền một cục. Khắc phục: Đặt `Offset from origin` tối thiểu `1.5mm`.
- **Mũi tên biến thành chấm tròn hoặc hình kỳ lạ:** Do vô tình đổi thiết lập `First` / `Second` trong thẻ Symbols and Arrows sang kiểu `Dot` hoặc `User Arrow`.
- **Kích thước bị nhân sai số đo:** Trong thẻ Primary Units > mục `Measurement scale` > ô `Scale factor` bị đặt khác 1 (ví dụ đặt là 2 khiến cạnh dài 100mm lại hiện số 200). Luôn kiểm tra `Scale factor` phải là `1.0`.

## Bài tập thực hành

- [ ] Gõ `DIMSTYLE` (hoặc `D`) để mở Dimension Style Manager. <!-- expect: DIMSTYLE -->
- [ ] Chọn kiểu `ISO-25`, bấm **New**, đặt tên kiểu là `TCVN-CO-KHI`.
- [ ] Trong thẻ `Lines`, đặt `Extend beyond dim lines` là 2 và `Offset from origin` là 2.
- [ ] Trong thẻ `Text`, chọn vị trí `Vertical` là `Above` và `Text height` là 2.5.
- [ ] Trong thẻ `Primary Units`, tick chọn `Trailing` ở mục `Zero suppression`. Bấm OK và chọn **Set Current**. <!-- expect: DIMSTYLE -->
- [ ] Dùng lệnh `DIMLINEAR` vẽ thử một kích thước để kiểm tra kiểu mới đã áp dụng đúng chưa. <!-- expect: DIMLINEAR -->

## Nguồn tham khảo

```links
- title: "Quản lý Dimension Styles chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=DIMSTYLE"
  kind: official
```
