---
id: ac-06-07
title: Trích xuất khối lượng và bóc tách dữ liệu với DATAEXTRACTION
category: Khối và Tham chiếu
tags: [dataextraction, thong-ke, xuat-du-lieu, excel, bom]
level: advanced
minutes: 25
needs: [ac-06-02, ac-05-07]
appVersions: ['2024', '2025']
edition: all
---
# Trích xuất khối lượng và bóc tách dữ liệu với DATAEXTRACTION

> **Mục tiêu:**
> - Sử dụng trình thuật sĩ `DATAEXTRACTION` để tự động bóc tách số lượng và thuộc tính của toàn bộ Block trong bản vẽ.
> - Lọc, sắp xếp và kết xuất dữ liệu thẳng vào bảng AutoCAD Table hoặc tệp Microsoft Excel ngoài.
> - Cập nhật bảng thống kê tự động khi thêm, bớt hoặc chỉnh sửa đối tượng trong thiết kế.

## Bóc tách khối lượng tự động: Từ thủ công đến 1 cú click

Sau khi vẽ xong mặt bằng một công trình có 50 cánh cửa, 120 bóng đèn và 80 cái bàn ghế, công việc kinh khủng nhất của người kỹ sư trước đây là gì?
Đó là ngồi đếm thủ công từng cái một: "Một cái cửa... hai cái cửa... ba cái cửa...". Việc này không chỉ tốn hàng giờ đồng hồ mệt mỏi mà còn tiềm ẩn nguy cơ đếm sót hoặc đếm trùng, dẫn đến dự toán kinh phí sai lệch hàng trăm triệu đồng!

Lệnh **`DATAEXTRACTION` (Lệnh tắt `DX`)** là công cụ tối thượng của AutoCAD:
Nó quét toàn bộ bản vẽ chỉ trong 1 giây, tự động đếm chính xác từng loại Block, lọc ra toàn bộ các nhãn thuộc tính ([[Attribute]]) như kích thước, vật liệu, mã hiệu, diện tích, sau đó:
- Xuất thành một bảng **AutoCAD Table** gắn trực tiếp vào bản vẽ.
- Hoặc xuất thẳng ra tệp bảng tính **Microsoft Excel (`.xlsx` hoặc `.csv`)** để chuyển cho phòng kinh doanh làm báo giá!

## Quy trình 8 bước của trình thuật sĩ Data Extraction

Gõ lệnh `DX` hoặc `DATAEXTRACTION` rồi nhấn [Enter]. Một cửa sổ thuật sĩ (Wizard) gồm 8 bước rõ ràng sẽ mở ra:

### Bước 1: Khởi tạo tệp mẫu trích xuất
- Chọn `Create a new data extraction` (tạo một mẫu trích xuất mới).
- Bấm **Next**, đặt tên cho file cấu hình (ví dụ: `BOC-TACH-CUA.dxe`) và lưu lại. Tệp `.dxe` này cho phép bạn tái sử dụng cấu hình cho các dự án sau mà không cần cài đặt lại từ đầu.

### Bước 2: Nguồn dữ liệu (Data Source)
- Chọn `Drawings/Sheet set` để quét toàn bộ file hiện tại, hoặc bấm `Add Drawings` để quét cùng lúc hàng chục file bản vẽ khác nhau trong toàn bộ dự án!

### Bước 3: Chọn đối tượng cần trích xuất (Select Objects)
- Danh sách tất cả các loại đối tượng trong bản vẽ sẽ hiện ra (Lines, Circles, Blocks...).
- Bỏ chọn các nét vẽ rác, chỉ đánh dấu tick vào các khối Block bạn cần thống kê (ví dụ: tick vào Block `CUA-DI-D900`, `CUA-SO-S1200`).

### Bước 4: Chọn thuộc tính cần lấy (Select Properties)
- Tại cột lọc bên phải *Category filter*, bỏ tick các thông tin hình học không cần (3D Visualization, General...).
- Chỉ giữ lại mục **Attribute** (các nhãn biến do bạn tạo) và mục **Drawing info**.
- Đánh dấu tick vào các trường bạn muốn hiển thị trong bảng: `Tên cửa`, `Kích thước`, `Vật liệu`, `Hãng sản xuất`...

### Bước 5: Tinh chỉnh bảng biểu (Refine Data)
- Cột **Count** (Số lượng) tự động đếm tổng số từng loại chi tiết.
- Bạn có thể kéo thả để đổi thứ tự các cột (ví dụ đưa cột Tên ra đầu, cột Số lượng ra cuối).
- Nhấp chuột phải vào tiêu đề cột để ẩn bớt cột thừa hoặc sắp xếp tăng/giảm dần theo bảng chữ cái.

### Bước 6: Lựa chọn đầu ra (Output Options)
- **Insert data extraction table into drawing:** Chèn bảng kết quả trực tiếp thành đối tượng `Table` vào bản vẽ CAD.
- **Output data to external file (.xls, .csv, .txt):** Xuất ra tệp bảng tính Excel độc lập. Bạn có thể tick chọn cả hai mục cùng lúc!

### Bước 7: Định dạng kiểu bảng (Table Style)
- Chọn kiểu bảng (ví dụ `TABLESTYLE` đã tạo ở chặng 5), đặt tiêu đề cho bảng: "BẢNG THỐNG KÊ CHI TIẾT CỬA".

### Bước 8: Hoàn tất (Finish)
- Bấm **Finish** và bấm chuột trái để đặt bảng lên vị trí thông thoáng trên bản vẽ.

## Cập nhật bảng thống kê tự động khi thiết kế thay đổi

Sau khi đã chèn bảng thống kê ra bản vẽ, nếu chủ đầu tư yêu cầu thêm 5 cánh cửa nữa:
1. Bạn chỉ việc dùng lệnh `COPY` thêm 5 khối block cửa vào mặt bằng.
2. Bấm chuột phải vào bảng thống kê trên màn hình.
3. Chọn dòng **Update Table Data Links** (hoặc gõ lệnh `DATALINKUPDATE`).
4. Ngay lập tức, con số tại cột Số lượng (Count) sẽ tự động nhảy số chính xác mà bạn không phải đếm lại dù chỉ 1 giây!

> [!TIP]
> Tệp `.dxe` lưu lại toàn bộ cấu hình lọc cột. Khi triển khai các dự án mới, ở Bước 1 chỉ cần chọn *Use previous extraction as a template* để áp dụng ngay bộ lọc mà không mất công tick chọn lại từng thuộc tính.

## Tự kiểm tra

```quiz
id: q-ac-06-07-1
type: single
question: "Lệnh tắt ngắn nhất để khởi động trình thuật sĩ trích xuất dữ liệu Data Extraction trong AutoCAD là gì?"
options:
  - text: "DX"
    correct: true
    why: "DX là lệnh tắt tiêu chuẩn của lệnh DATAEXTRACTION."
  - text: "DE"
    correct: false
    why: "DE không phải lệnh Data Extraction."
  - text: "EX"
    correct: false
    why: "EX là lệnh EXTEND (kéo dài đối tượng)."
  - text: "DTE"
    correct: false
    why: "DTE không phải alias chuẩn của AutoCAD."
explain: "Sử dụng phím tắt DX để mở nhanh trình thuật sĩ 8 bước trích xuất dữ liệu khối lượng."
```

```quiz
id: q-ac-06-07-2
type: single
question: "Khi số lượng đối tượng trong bản vẽ thay đổi, bạn làm cách nào để bảng thống kê Data Extraction cập nhật số liệu mới?"
options:
  - text: "Nhấp chuột phải vào bảng và chọn Update Table Data Links (hoặc DATALINKUPDATE)"
    correct: true
    why: "Lệnh cập nhật liên kết dữ liệu sẽ quét lại bản vẽ và làm mới toàn bộ số lượng trong bảng."
  - text: "Phải xóa bảng cũ đi và chạy lại từ đầu toàn bộ 8 bước"
    correct: false
    why: "AutoCAD hỗ trợ cập nhật động thông minh, không cần làm lại từ đầu."
  - text: "Gõ lệnh ERASE"
    correct: false
    why: "ERASE sẽ xóa mất bảng thống kê."
  - text: "Khởi động lại máy tính"
    correct: false
    why: "Không cần khởi động lại máy tính."
explain: "Tính năng liên kết động Data Links cho phép bảng thống kê cập nhật số lượng chỉ bằng một cú nhấp chuột phải."
```

```quiz
id: q-ac-06-07-3
type: truefalse
question: "DATAEXTRACTION cho phép quét và trích xuất dữ liệu từ nhiều tệp bản vẽ DWG khác nhau cùng một lúc trong một dự án."
answer: false
explain: "Khả năng quét đa tệp giúp các kỹ sư tổng hợp khối lượng cho toàn bộ công trình gồm hàng chục bản vẽ mặt bằng chỉ trong vài phút."
```

## Lỗi thường gặp

- **Bảng thống kê bị hiển thị quá nhiều chi tiết rác:** Do ở Bước 3 và Bước 4 bạn không lọc đối tượng, khiến AutoCAD quét cả các nét thẳng, đường tròn và thuộc tính hình học vụn vặt. Khắc phục: Quay lại Wizard và chỉ tick chọn Block cùng mục Attribute.
- **File Excel xuất ra bị lỗi font tiếng Việt:** Do chọn định dạng file text cũ. Khắc phục: Khi xuất dữ liệu ở Bước 6, luôn chọn định dạng đuôi `.xlsx` hoặc `.csv (Unicode)`.

## Bài tập thực hành

- [ ] Gõ `DATAEXTRACTION` (hoặc `DX`) để mở cửa sổ thuật sĩ. <!-- expect: DATAEXTRACTION -->
- [ ] Tiến hành tạo một file cấu hình trích xuất mới đặt tên là `TEST-THONG-KE.dxe`.
- [ ] Chọn phạm vi bản vẽ hiện hành và quan sát danh sách các khối Block có trong bản vẽ.
- [ ] Chọn một vài thuộc tính như tên khối và số lượng, sau đó xem trước bảng dữ liệu ở Bước 5.
- [ ] Hủy hoặc hoàn tất tạo bảng để nắm vững quy trình 8 bước.

## Nguồn tham khảo

```links
- title: "Trích xuất dữ liệu thuộc tính DATAEXTRACTION từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=DATAEXTRACTION"
  kind: official
```
