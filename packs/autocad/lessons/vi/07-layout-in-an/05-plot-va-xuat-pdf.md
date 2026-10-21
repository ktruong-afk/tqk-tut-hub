---
id: ac-07-05
title: Xuất bản vẽ và in ấn tệp PDF hoàn hảo với lệnh PLOT
category: Layout và In ấn
tags: [plot, exportpdf, pdf, in-an, preview]
level: intermediate
minutes: 20
needs: [ac-07-03, ac-07-04]
appVersions: ['2024', '2025']
edition: all
---
# Xuất bản vẽ và in ấn tệp PDF hoàn hảo với lệnh PLOT

> **Mục tiêu:**
> - Sử dụng lệnh `PLOT` ([Ctrl + P]) và `EXPORTPDF` để xuất hồ sơ bản vẽ kỹ thuật sang định dạng PDF vector.
> - Thao tác xem trước bản in với nút `Preview` để phát hiện và ngăn chặn triệt để mọi lỗi sai sót trước khi bấm in.
> - Kiểm soát các tuỳ chọn in nâng cao: độ dày nét in (Lineweights), độ trong suốt (Transparency) và nhúng phông chữ tiếng Việt.

## Xuất file PDF: Định dạng giao tiếp tiêu chuẩn của ngành thiết kế

Thời kỳ in hàng xấp giấy A0, A1 cồng kềnh mang đi họp đang dần nhường chỗ cho tài liệu điện tử. Ngày nay, hầu hết các chủ đầu tư, nhà thầu thi công và cơ quan thẩm duyệt đều yêu cầu nộp hồ sơ thiết kế dưới dạng tệp **PDF**.

Một tệp PDF chuẩn xuất từ AutoCAD phải thỏa mãn 3 tiêu chuẩn chất lượng cao:
1. **Định dạng Vector phóng to không vỡ hình:** Dù phóng to 5000% trên màn hình máy tính hay điện thoại, các đường nét vẫn mảnh mai sắc lẹm, không bao giờ bị nhòe hạt hình như file ảnh JPEG scan.
2. **Hỗ trợ tìm kiếm văn bản (Searchable Text):** Người đọc có thể nhấn [Ctrl + F] trong trình đọc PDF (Acrobat Reader, Foxit Reader, Google Chrome) để gõ tìm mã hiệu căn hộ, tên trục hoặc thông số kỹ thuật.
3. **Dung lượng tối ưu:** Một bộ hồ sơ hàng chục trang nhưng chỉ nặng vài Megabyte, dễ dàng gửi qua Zalo, Email hoặc tải lên hệ thống quản lý dự án đám mây.

## Cách dùng từng bước với lệnh PLOT ([Ctrl + P])

### 1. Mở hộp thoại Plot
- Đang ở tab Layout cần in, nhấn tổ hợp phím **[Ctrl + P]** hoặc gõ `PLOT` rồi nhấn [Enter].
- Nếu đã cấu hình Page Setup từ trước, bạn sẽ thấy toàn bộ thông số máy in, khổ giấy A3, bảng nét in CTB đã được điền sẵn hoàn hảo!

### 2. Kiểm tra các tuỳ chọn in quan trọng (Plot Options)
Tại cột bên phải hộp thoại Plot, kiểm tra các ô đánh dấu:
- **Plot object lineweights:** BẮT BUỘC TICK. Lệnh này báo cho máy in vẽ đúng độ đậm nhạt của nét vẽ (nét cắt dày, nét tim mỏng). Nếu bỏ tick ô này, tất cả các nét sẽ in ra mỏng như sợi chỉ!
- **Plot with plot styles:** BẮT BUỘC TICK. Áp dụng bảng nét in `.ctb` bạn đã cấu hình ở bài trước.
- **Plot transparency:** Chỉ tick khi bản vẽ của bạn có sử dụng đối tượng trong suốt (như bóng đổ hoặc vùng tô kính xuyên sáng).
- **Hide paperspace objects:** Bỏ tick (chỉ dùng cho bản vẽ 3D).

### 3. Quy tắc bắt buộc: LUÔN LUÔN BẤM PREVIEW TRƯỚC KHI IN!
Ở góc dưới bên trái của hộp thoại Plot, có nút bấm **Preview...** (Xem trước):
1. Bấm nút **Preview...**: Màn hình sẽ chuyển sang chế độ xem trước toàn trang giấy in với độ phân giải thực 100%.
2. Dùng chuột giữa phóng to để soi kỹ các chi tiết:
   - Các nét cắt cột có đậm và đen tuyền không?
   - Chữ số kích thước có bị đè lên nét vẽ nào không?
   - Khung tên có nằm trọn trong trang giấy mà không bị mất góc nào không?
3. Nếu phát hiện lỗi: Nhấn phím [Esc] để quay lại bản vẽ chỉnh sửa.
4. Nếu mọi thứ hoàn hảo: Nhấp chuột phải chọn **Plot** (hoặc bấm biểu tượng chiếc máy in ở góc trên).
5. Đặt tên tệp PDF cần lưu (ví dụ: `KT-01-MAT-BANG-TANG-1.pdf`), chọn thư mục lưu và bấm **Save**.

## Xuất nhanh một chạm với lệnh EXPORTPDF

Nếu bạn chỉ muốn xuất nhanh bản vẽ hiện tại ra PDF mà không cần mở hộp thoại Plot phức tạp:
1. Gõ lệnh `EXPORTPDF` rồi nhấn [Enter].
2. Chọn thư mục lưu tệp PDF và bấm **Save**.
3. AutoCAD sẽ tự động lấy cấu hình trang in của Layout hiện hành và xuất ra file PDF ngay lập tức.

> [!TIP]
> Để chữ tiếng Việt trong file PDF luôn tìm kiếm được bằng [Ctrl + F] và không bị biến thành nét vẽ hình học vô hồn: Trong hộp thoại `Page Setup` > tại ô máy in *AutoCAD PDF*, bấm nút **Properties** > chọn *Custom Properties* > đánh dấu tick vào ô **Capture fonts used in the drawing**!

> [!WARNING]
> Không bao giờ in từ không gian Model bằng cách chọn vùng in `Window` rồi quét khung bằng mắt cho từng tờ giấy. Làm như vậy rất lâu, dễ bị lệch mép giấy và tỉ lệ in bị méo mó. Luôn in chuẩn từ không gian Layout!

## Tự kiểm tra

```quiz
id: q-ac-07-05-1
type: single
question: "Thao tác nào là BẮT BUỘC phải thực hiện trước khi bấm xuất file PDF hoặc in giấy trong AutoCAD để tránh lãng phí và sai sót?"
options:
  - text: "Bấm nút Preview để xem trước bản in với độ phân giải và nét in thực tế"
    correct: true
    why: "Preview giúp phát hiện ngay các lỗi mất nét, đè chữ hoặc lệch mép giấy trước khi in ra tệp thật."
  - text: "Xóa toàn bộ các layer chỉ chừa lại layer 0"
    correct: false
    why: "Xóa layer sẽ làm mất dữ liệu của toàn bộ dự án."
  - text: "Khởi động lại máy tính"
    correct: false
    why: "Không cần khởi động lại máy trước mỗi lần in."
  - text: "Đổi màu màn hình sang màu đỏ"
    correct: false
    why: "Màu màn hình không liên quan đến quy trình in ấn."
explain: "Nút Preview là chốt chặn an toàn số một của người làm đồ họa kỹ thuật để đảm bảo 100% chất lượng bản in trước khi xuất xưởng."
```

```quiz
id: q-ac-07-05-2
type: single
question: "Nếu bỏ dấu tick ở ô 'Plot object lineweights' trong hộp thoại Plot, hiện tượng gì sẽ xảy ra với bản in?"
options:
  - text: "Tất cả các nét vẽ in ra đều có độ dày mảnh như nhau, mất hoàn toàn sự phân cấp đậm nhạt"
    correct: true
    why: "Plot object lineweights ra lệnh cho máy in áp dụng độ dày Lineweight cho nét vẽ."
  - text: "Bản vẽ in ra bị đảo ngược màu từ đen sang trắng"
    correct: false
    why: "Độ dày nét không làm đảo màu nền."
  - text: "Toàn bộ chữ số kích thước biến thành tiếng Nhật"
    correct: false
    why: "Lineweight không can thiệp vào bộ gõ ngôn ngữ."
  - text: "Máy in từ chối nhận lệnh và báo kẹt giấy"
    correct: false
    why: "Máy in vẫn in bình thường nhưng nét vẽ ra sẽ bị mảnh."
explain: "Luôn kiểm tra ô Plot object lineweights được đánh dấu tick để bản in có độ tương phản nét đậm nét mảnh chuẩn kỹ thuật."
```

```quiz
id: q-ac-07-05-3
type: truefalse
question: "Lệnh EXPORTPDF cho phép người dùng xuất nhanh trang Layout hiện hành sang định dạng tài liệu PDF mà không cần trải qua nhiều bước hộp thoại in."
answer: true
explain: "EXPORTPDF là công cụ xuất file nhanh tiện lợi, tự động kế thừa toàn bộ cấu hình trang in của Layout hiện hành."
```

## Lỗi thường gặp

- **Chữ tiếng Việt khi mở file PDF bị lỗi font ô vuông:** Do bản vẽ sử dụng font lạ mà máy tính không nhúng được vào PDF. Khắc phục: Dùng các font Unicode hệ thống chuẩn như `Arial`, `Tahoma` hoặc tick chọn `Capture all fonts` trong phần cài đặt của driver in AutoCAD PDF.
- **File PDF quá nặng (hàng trăm MB):** Do chèn các bức ảnh raster vệ tinh có độ phân giải quá cao, hoặc do nét vẽ chứa hàng triệu đoạn thẳng vụn vặt. Khắc phục: Giảm bớt độ phân giải Vector Quality trong phần PDF Options về mức `600 dpi` thay vì `2400 dpi`.

## Bài tập thực hành

- [ ] Nhấn tổ hợp phím `Ctrl + P` hoặc gõ lệnh `PLOT` để mở hộp thoại in ấn. <!-- expect: PLOT -->
- [ ] Kiểm tra các ô chọn: `Plot object lineweights` và `Plot with plot styles` đều đã được đánh dấu tick.
- [ ] Bấm vào nút **Preview** để xem trước toàn cảnh bản in trang giấy A3.
- [ ] Thoát khỏi Preview và hoàn tất tạo lệnh in. <!-- expect: PLOT -->
- [ ] Thử gõ lệnh `EXPORTPDF` để trải nghiệm tính năng xuất nhanh tài liệu PDF. <!-- expect: EXPORTPDF -->

## Nguồn tham khảo

```links
- title: "Quy trình in và xuất bản vẽ PLOT từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=PLOT"
  kind: official
- title: "Xuất tệp PDF bằng lệnh EXPORTPDF từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=EXPORTPDF"
  kind: official
```
