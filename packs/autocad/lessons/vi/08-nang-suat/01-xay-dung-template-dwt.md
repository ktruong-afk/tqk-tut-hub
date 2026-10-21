---
id: ac-08-01
title: Xây dựng tệp mẫu bản vẽ chuẩn hoá Drawing Template (DWT)
category: Nâng cao năng suất
tags: [template, dwt, tieu-chuan, layer, dimstyle, quy-trinh]
level: intermediate
minutes: 25
needs: [ac-07-07]
appVersions: ['2024', '2025']
edition: all
---
# Xây dựng tệp mẫu bản vẽ chuẩn hoá Drawing Template (DWT)

> **Mục tiêu:**
> - Xây dựng tệp mẫu bản vẽ [[Template]] (`.dwt`) tích hợp đầy đủ hệ thống Layer, Dimstyle, Textstyle và Layout chuẩn công ty.
> - Thiết lập tệp mẫu thành file khởi động mặc định (Default Template) khi tạo bản vẽ mới với lệnh `QNEW`.
> - Chuẩn hóa các thiết lập đơn vị đo, tỉ lệ chú thích và bảng nét in để tránh trùng lặp thao tác.

## Tệp mẫu DWT: Nền móng vững chắc của mọi bản vẽ kỹ thuật

Mỗi sáng khi bắt đầu một ngày làm việc mới, bạn có muốn phải ngồi:
- Tạo lại 15 layer quen thuộc (`Tuong`, `Cot`, `KichThuoc`, `Text`...)?
- Cài đặt lại kiểu chữ Unicode `Arial` chiều cao `0.0`?
- Thiết lập lại kiểu đo kích thước TCVN mũi tên 2.5mm?
- Chuyển sang Layout cấu hình khổ giấy A3 và chèn lại khung tên?

Nếu làm như vậy, mỗi dự án bạn đã lãng phí ít nhất 30 phút chỉ để chuẩn bị những thứ lặp đi lặp lại. Hơn thế nữa, mỗi người trong công ty sẽ tạo ra một kiểu layer với mã màu khác nhau, khiến việc ghép nối bản vẽ thành một thảm họa!

**Tệp mẫu bản vẽ ([[Template]] - Đuôi file `.dwt`)** là chìa khóa chuẩn hóa:
Nó lưu trữ sẵn 100% tất cả các thiết lập chuẩn mực của công ty. Khi bạn bấm nút tạo bản vẽ mới, một không gian làm việc hoàn hảo đã được dọn sẵn tinh tươm, bạn chỉ việc bắt tay vào thiết kế ngay lập tức!

## 6 thành phần bắt buộc phải có trong một Template DWT chuẩn

1. **Hệ thống Layer quy chuẩn:** Đầy đủ các lớp chuyên ngành với màu sắc, kiểu đường `Linetype` và độ dày nét `Lineweight` cố định.
2. **Kiểu chữ (Text Style):** Tạo sẵn kiểu chữ Unicode chuẩn (ví dụ `TCVN-ARIAL`) với chiều cao `Height = 0`.
3. **Kiểu kích thước (Dimstyle):** Tạo sẵn các kiểu đo thẳng, đo xiên, đo bán kính và kiểu `Annotative` đã tinh chỉnh `Baseline spacing = 8mm`, `Zero suppression = Trailing`.
4. **Kiểu ghi chú (MLeader Style):** Tạo sẵn kiểu ghi chú dẫn hướng `TCVN-MLD` có đoạn ngang gác chữ 8mm.
5. **Hệ đơn vị (Units):** Lệnh `UNITS` cài đặt `Decimal`, độ chính xác `0` (hoặc `0.0`), đơn vị chèn `Millimeters`.
6. **Các trang Layout in ấn:** Cấu hình sẵn các tab `A3-NGANG`, `A3-DUNG`, `A1-NGANG` đã Page Setup sẵn máy in `AutoCAD PDF`, bảng nét in `.ctb` và khung tên gắn thuộc tính thông minh.

## Cách tạo và lưu tệp DWT từng bước

### 1. Chuẩn bị file sạch
1. Mở một bản vẽ trắng từ template `acadiso.dwt`.
2. Tạo mới toàn bộ hệ thống Layer, Textstyle, Dimstyle, TableStyle như đã học từ chặng 1 đến chặng 7.
3. Chuyển sang Layout, cấu hình Page Setup khổ A3 Full Bleed, chèn khung tên chuẩn vào toạ độ `0,0` và mở sẵn khung nhìn `MVIEW`.
4. Gõ lệnh `PURGE` để dọn sạch mọi đối tượng rác không dùng.

### 2. Lưu file dưới định dạng DWT
1. Bấm vào biểu tượng chữ **A** lớn (Application Menu) ở góc trên bên trái > chọn **Save As** > chọn **AutoCAD Drawing Template (*.dwt)**.
2. AutoCAD sẽ tự động nhảy đến thư mục template hệ thống:
   `...\AppData\Local\Autodesk\AutoCAD ...\Template`.
3. Đặt tên file: ví dụ **`TCVN-CO-KHI-A3.dwt`** hoặc **`CONG-TY-KIEN-TRUC-ISO.dwt`**. Bấm **Save**.
4. Hộp thoại **Template Options** xuất hiện:
   - *Description:* Nhập mô tả (ví dụ: `Mẫu bản vẽ chuẩn công ty hệ mét khổ A3`).
   - *Measurement:* Chọn **Metric** (Hệ mét).
5. Bấm **OK**. Bạn đã có tệp mẫu của riêng mình!

### 3. Cài đặt thành file khởi động mặc định (Default Template)
Để mỗi lần bấm nút tạo file mới ([Ctrl + N] hoặc biểu tượng tờ giấy trắng `QNEW`), AutoCAD tự động mở ngay template của bạn mà không cần hỏi:
1. Gõ `OP` hoặc `OPTIONS` rồi nhấn [Enter].
2. Chuyển sang thẻ **Files**.
3. Bấm vào dấu `[+]` của mục **Template Settings** > bấm tiếp vào `[+]` của **Default Template File Name for QNEW**.
4. Bấm chọn dòng `None` hoặc tên file cũ, bấm nút **Browse...** bên phải.
5. Chọn đúng file `TCVN-CO-KHI-A3.dwt` vừa tạo. Bấm **Open**.
6. Bấm **Apply** và **OK**. Từ nay, mỗi trang vẽ mới mở ra đều là trang vẽ chuẩn mực của bạn!

> [!TIP]
> Bạn có thể sao chép file `.dwt` này sang máy tính của toàn bộ các đồng nghiệp trong phòng thiết kế để đảm bảo 100% nhân viên đều vẽ trên cùng một nền tảng tiêu chuẩn duy nhất.

## Tự kiểm tra

```quiz
id: q-ac-08-01-1
type: single
question: "Định dạng phần mở rộng (đuôi tệp) của file mẫu bản vẽ Drawing Template trong AutoCAD là gì?"
options:
  - text: ".dwt"
    correct: true
    why: "DWT viết tắt của Drawing Template."
  - text: ".dwg"
    why: "DWG là tệp bản vẽ đồ họa thông thường."
  - text: ".dxf"
    why: "DXF là tệp trao đổi dữ liệu bản vẽ (Drawing Exchange Format)."
  - text: ".ctb"
    why: "CTB là tệp bảng nét in Color-dependent Plot Style."
explain: "Tệp đuôi .dwt là định dạng khuôn mẫu lưu trữ cấu hình Layer, Style và Layout chuẩn của AutoCAD."
```

```quiz
id: q-ac-08-01-2
type: single
question: "Để cài đặt tệp template yêu thích tự động mở mỗi khi người dùng bấm lệnh tạo bản vẽ mới (QNEW), bạn thiết lập tại mục nào trong hộp thoại Options?"
options:
  - text: "Thẻ Files > mục Template Settings > Default Template File Name for QNEW"
    correct: true
    why: "Đây là đường dẫn quy định file mẫu tự động nạp cho lệnh QNEW."
  - text: "Thẻ Display > mục Colors"
    why: "Thẻ Display dùng để chỉnh màu nền giao diện."
  - text: "Thẻ Drafting > mục AutoSnap"
    why: "Thẻ Drafting dùng cài đặt truy bắt điểm Osnap."
  - text: "Thẻ 3D Modeling"
    why: "Thẻ 3D Modeling dùng cài đặt không gian 3D."
explain: "Cấu hình Default Template File Name for QNEW giúp người vẽ tiết kiệm thời gian chọn template mỗi khi mở bản vẽ mới."
```

```quiz
id: q-ac-08-01-3
type: truefalse
question: "Khi bạn mở một file mẫu .dwt và bắt đầu vẽ, phần mềm sẽ tự động yêu cầu lưu thành tệp .dwg mới, không làm ghi đè hay hỏng file mẫu gốc."
answer: true
explain: "Đây là cơ chế bảo vệ an toàn của template AutoCAD: nó luôn sinh ra một bản vẽ Drawing1.dwg độc lập dựa trên khuôn mẫu có sẵn."
```

## Lỗi thường gặp

- **Chọn nhầm Measurement là Imperial (Hệ Inch):** Khiến các lệnh Hatch và kích thước bị co kéo theo hệ inch thay vì milimet. Luôn chọn `Metric` khi lưu template.
- **Để quên các nét vẽ thử trong template:** Khiến mỗi lần mở file mới đều có sẵn các hình vẽ rác cũ. Khắc phục: Mở file `.dwt`, quét xóa sạch mọi hình vẽ trong Model, chạy lệnh `PURGE` dọn rác rồi lưu lại.

## Bài tập thực hành

- [ ] Mở bản vẽ hiện tại, kiểm tra danh sách các layer và kiểu kích thước chuẩn đã học.
- [ ] Bấm **Application Menu** > **Save As** > chọn định dạng **AutoCAD Drawing Template (*.dwt)**.
- [ ] Đặt tên tệp là `TCVN-MAU-CHUAN.dwt`, nhập mô tả `Mau ban ve thiet ke chuan TCVN`, chọn hệ `Metric` và bấm Save.
- [ ] Gõ `OPTIONS` (hoặc `OP`), duyệt đến mục `Default Template File Name for QNEW` trong thẻ Files để kiểm tra đường dẫn template. <!-- expect: OPTIONS -->

## Nguồn tham khảo

```links
- title: "Tạo và sử dụng Drawing Templates (DWT) từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Drawing+Templates"
  kind: official
```
