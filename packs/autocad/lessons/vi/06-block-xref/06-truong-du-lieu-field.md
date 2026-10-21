---
id: ac-06-06
title: Tự động hoá thông tin bản vẽ với trường dữ liệu FIELD
category: Khối và Tham chiếu
tags: [field, updatefield, tu-dong-hoa, dien-tich, nang-suat]
level: intermediate
minutes: 20
needs: [ac-06-02]
appVersions: ['2024', '2025']
edition: all
---
# Tự động hoá thông tin bản vẽ với trường dữ liệu FIELD

> **Mục tiêu:**
> - Sử dụng lệnh `FIELD` để chèn các trường dữ liệu động như diện tích hình học, ngày tháng, tên file.
> - Liên kết trường Field vào văn bản hoặc thuộc tính Block khung tên bản vẽ.
> - Cập nhật dữ liệu tự động khi hình học bị chỉnh sửa bằng lệnh `UPDATEFIELD`.

## Khái niệm trường dữ liệu động FIELD

Trong thực tế thiết kế, có những thông số văn bản luôn thay đổi theo đối tượng:
- Diện tích một căn phòng: Nếu kiến trúc sư kéo rộng bức tường ra thêm 500mm, con số ghi diện tích trên sàn nhà phải tự động tăng lên!
- Ngày in ấn bản vẽ: Khi bạn mở file ra in lại vào ngày mai, ngày tháng trên khung tên phải tự động cập nhật ngày hiện tại.
- Tên tệp tin hoặc đường dẫn bản vẽ: Để thợ công trường biết bản vẽ được xuất từ file nào trên máy chủ công ty.

Nếu bạn gõ các con số này bằng chữ tĩnh (`TEXT` hoặc `MTEXT`), mỗi khi thay đổi thiết kế bạn sẽ phải dùng máy tính bỏ túi tính lại diện tích rồi sửa từng con số một.

**[[Field]] (Trường dữ liệu động)** là một đoạn văn bản có khả năng "lắng nghe" và liên kết chặt chẽ với các thuộc tính hình học của bản vẽ. Bất cứ khi nào hình vẽ thay đổi kích thước, con số Field sẽ **tự động tính toán lại** mà bạn không cần phải làm gì!

Một trường Field trong AutoCAD luôn được hiển thị với một ô nền màu xám nhạt (nền này chỉ để báo hiệu trên màn hình, khi in ra giấy hoàn toàn là chữ bình thường, không có vệt xám).

## Cách dùng từng bước

### 1. Tạo trường Field tự động tính diện tích sàn
1. Vẽ một đường viền phòng khép kín bằng lệnh `PLINE` (ví dụ phòng có diện tích 30m²).
2. Gõ lệnh `FIELD` rồi nhấn [Enter] (hoặc khi đang viết `MTEXT`, nhấp chuột phải chọn **Insert Field...** hay nhấn [Ctrl + F]).
3. Hộp thoại **Field** xuất hiện:
   - **Field category:** Chọn `Objects`.
   - **Field names:** Chọn `Object`.
   - Tại cột giữa mục *Object type*, bấm vào biểu tượng bàn tay nhỏ có con trỏ chuột (**Select object**).
   - Bấm chuột chọn vào đường Polyline vừa vẽ trên màn hình.
   - Danh sách thuộc tính của đường Polyline sẽ hiện ra ở cột giữa: Bấm chọn dòng **Area** (Diện tích).
   - Tại cột bên phải **Format**: Chọn `Decimal`, điều chỉnh số chữ số thập phân `Precision` là `0.00`.
   - Bấm nút **Additional Format...**: Vì đơn vị vẽ là milimet, diện tích tính ra là $mm^2$. Để đổi ra $m^2$, tại ô `Conversion factor` nhập `0.000001` (chia cho 1.000.000); tại ô `Suffix` (hậu tố) gõ ` m²`. Bấm **OK**.
4. Bấm **OK** để chèn con số Field vào giữa phòng. Màn hình sẽ hiện: `30.00 m²`.

### 2. Thử nghiệm tính toán tự động
1. Dùng lệnh `STRETCH` kéo dãn một cạnh của căn phòng ra xa thêm 1 mét.
2. Bạn sẽ thấy con số diện tích chưa đổi ngay lập tức.
3. Gõ lệnh `REGEN` (hoặc `REA`), hoặc gõ `UPDATEFIELD` rồi bấm vào con số.
4. Con số lập tức nhảy thành `35.00 m²` một cách kỳ diệu!

### 3. Chèn ngày tháng và tên tệp tự động vào khung tên
- Khi sửa khung tên bản vẽ, mở hộp thoại `FIELD`:
  - Chọn danh mục **Date & Time** > chọn **CreateDate** hoặc **SaveDate** để ngày in tự nhảy đúng theo lịch hệ thống.
  - Chọn danh mục **Document** > chọn **FileName** để tên tệp DWG tự hiển thị trong ô tên bản vẽ.

## Tuỳ chọn và mẹo kiểm soát hiển thị

- **Ẩn hiện vệt màu xám của Field (`FIELDDISPLAY`):**
  Nếu bạn thấy vệt xám nền của Field gây khó chịu khi nhìn màn hình, hãy gõ biến hệ thống `FIELDDISPLAY`:
  - `FIELDDISPLAY = 1`: Hiển thị vệt xám báo hiệu (Mặc định, khuyên dùng).
  - `FIELDDISPLAY = 0`: Tắt vệt xám, chữ Field trông giống hệt chữ thường.
- **Biến `FIELDEVAL` (Khi nào thì Field tự cập nhật?):**
  Mặc định AutoCAD sẽ tự động cập nhật Field khi: Mở file (Open), Lưu file (Save), In bản vẽ (Plot), hoặc gõ lệnh `REGEN`.

> [!TIP]
> Bạn có thể lồng trường Field vào trong giá trị thuộc tính Block Attribute của khung tên bản vẽ, giúp tạo ra những khung tên thông minh đẳng cấp quốc tế.

## Tự kiểm tra

```quiz
id: q-ac-06-06-1
type: single
question: "Dấu hiệu trực quan nào trên màn hình giúp bạn nhận biết một đoạn văn bản là trường dữ liệu động FIELD?"
options:
  - text: "Đoạn chữ có một khung nền vệt màu xám nhạt bao quanh"
    correct: true
    why: "Vệt xám nhạt (Field Display) là dấu hiệu cảnh báo thị giác của AutoCAD cho đối tượng Field."
  - text: "Chữ luôn luôn có màu đỏ rực"
    correct: false
    why: "Màu chữ của Field hoàn toàn do Layer hoặc TextStyle quy định."
  - text: "Chữ liên tục nhấp nháy phát sáng"
    correct: false
    why: "Chữ không nhấp nháy trên màn hình CAD."
  - text: "Chữ luôn nằm ngược từ phải sang trái"
    correct: false
    why: "Chữ Field hiển thị theo chiều đọc thông thường."
explain: "Vệt xám nền này chỉ xuất hiện khi làm việc trong AutoCAD để nhắc nhở người vẽ không gõ đè chữ tay, và khi in ra giấy vệt xám sẽ hoàn toàn vô hình."
```

```quiz
id: q-ac-06-06-2
type: single
question: "Để đổi giá trị diện tích từ đơn vị mm² sang m² trong hộp thoại Field, tại ô Conversion Factor của mục Additional Format bạn cần nhập giá trị nào?"
options:
  - text: "0.000001 (tức 1/1.000.000)"
    correct: true
    why: "1 m² = 1.000.000 mm², do đó cần nhân với 10⁻⁶ để đổi đơn vị."
  - text: "0.001"
    correct: false
    why: "0.001 chỉ là chia cho 1.000 (đổi từ mm sang mét dài)."
  - text: "1000"
    correct: false
    why: "Nhân 1000 sẽ làm giá trị phóng đại lên gấp nghìn lần."
  - text: "10"
    correct: false
    why: "10 không đúng với tỉ lệ diện tích."
explain: "Do bản vẽ CAD tiêu chuẩn vẽ theo đơn vị milimet, 1m² = 1.000mm x 1.000mm = 1.000.000mm². Vì vậy hệ số chuyển đổi là 0.000001."
```

```quiz
id: q-ac-06-06-3
type: truefalse
question: "Khi thay đổi kích thước hình học, bạn chỉ cần gõ lệnh REGEN (hoặc REA) là các trường FIELD liên kết diện tích sẽ tự động cập nhật số liệu mới."
answer: false
explain: "Gõ REGEN hoặc REA là thói quen chuẩn mực của kỹ sư để làm mới toàn bộ các số liệu tự động trên bản vẽ."
```

## Lỗi thường gặp

- **Chữ Field hiển thị dấu #### (bốn dấu thăng):** Xảy ra khi đối tượng hình học mà Field liên kết tới đã bị xóa mất khỏi bản vẽ, hoặc liên kết bị đứt đoạn. Khắc phục: Nhấp đúp vào chữ Field để bấm chọn lại đối tượng hình học còn tồn tại.
- **Vệt xám nền biến mất:** Do biến `FIELDDISPLAY` bị đổi thành `0`. Khắc phục: Gõ `FIELDDISPLAY` nhập `1`.

## Bài tập thực hành

- [ ] Dùng lệnh `RECTANG` vẽ một phòng hình chữ nhật kích thước 6000 x 4000 mm. <!-- expect: RECTANG -->
- [ ] Gõ lệnh `FIELD`, chọn Category `Objects` > Name `Object`, bấm chọn hình chữ nhật vừa vẽ. <!-- expect: FIELD -->
- [ ] Chọn thuộc tính `Area`, bấm `Additional Format` nhập `Conversion factor` là `0.000001` và `Suffix` là ` m2`. Bấm OK và đặt chữ ra màn hình. <!-- expect: FIELD -->
- [ ] Dùng lệnh `UPDATEFIELD`, bấm chọn con số diện tích vừa chèn. <!-- expect: UPDATEFIELD -->

## Nguồn tham khảo

```links
- title: "Tổng quan và cách sử dụng trường Fields từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=FIELD"
  kind: official
- title: "Lệnh UPDATEFIELD cập nhật dữ liệu tự động từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=UPDATEFIELD"
  kind: official
```
