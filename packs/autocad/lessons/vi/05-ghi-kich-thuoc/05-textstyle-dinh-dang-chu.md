---
id: ac-05-05
title: Định dạng kiểu chữ kỹ thuật với Text Style (STYLE)
category: Ghi kích thước
tags: [style, textstyle, mtext, font, tieng-viet]
level: beginner
minutes: 20
needs: [ac-05-04]
appVersions: ['2024', '2025']
edition: all
---
# Định dạng kiểu chữ kỹ thuật với Text Style (STYLE)

> **Mục tiêu:**
> - Sử dụng lệnh `STYLE` để tạo và quản lý các kiểu chữ kỹ thuật trong bản vẽ.
> - Phân biệt ưu nhược điểm giữa font đơn nét AutoCAD (`.shx`) và font hệ thống Windows (`TrueType / .ttf`).
> - Cài đặt bộ gõ tiếng Việt Unicode và quy tắc vàng đặt chiều cao chữ (`Height = 0`) trong Text Style.

## Vai trò của Text Style trong bản vẽ kỹ thuật

Chữ viết trên bản vẽ kỹ thuật (ghi chú kết cấu, tên phòng, bảng kê vật liệu, chữ số kích thước) phải rõ ràng, đồng nhất và tuân thủ tiêu chuẩn trình bày. Không được dùng các font chữ hoa mỹ, uốn lượn gây khó đọc khi thi công.

Trong AutoCAD, toàn bộ chữ viết được kiểm soát qua **Kiểu chữ ([[TextStyle]])**. Lệnh `STYLE` (lệnh tắt `ST`) mở hộp thoại thiết lập kiểu chữ.

Có 2 họ phông chữ chính trong AutoCAD:
- **Font SHX (AutoCAD Compiled Shape):** Font vector đơn nét cổ điển do Autodesk phát triển (ví dụ: `romans.shx`, `txt.shx`, `vn_vni.shx`). Ưu điểm: Dung lượng bản vẽ cực nhẹ, tốc độ zoom mượt mà, in ấn không bao giờ bị lỗi nhòe nét. Nhược điểm: Cần kèm theo file `.shx` khi gửi file cho người khác.
- **Font TrueType (TTF):** Font hệ điều hành Windows quen thuộc (ví dụ: `Arial`, `Times New Roman`, `Tahoma`). Ưu điểm: Hỗ trợ tiếng Việt Unicode 100% không bao giờ lỗi font, máy tính nào cũng có sẵn. Nhược điểm: Tệp bản vẽ nặng hơn một chút khi có quá nhiều chữ.

## Quy tắc vàng: Luôn để Text Height = 0 trong Text Style

Một trong những sai lầm phổ biến nhất của người mới học AutoCAD là nhập một giá trị cụ thể (như `2.5` hay `3.0`) vào ô **Height** trong hộp thoại `STYLE`.

Khi bạn đặt `Height = 0`:
- Kiểu chữ trở thành **linh hoạt (flexible)**.
- Khi dùng trong `DIMSTYLE`, chiều cao chữ sẽ tự điều chỉnh theo thiết lập của Dimstyle.
- Khi gõ `TEXT` hoặc `MTEXT`, AutoCAD sẽ cho phép bạn tự do nhập chiều cao chữ phù hợp với từng vị trí ghi chú khác nhau.

Nếu bạn đặt `Height` khác 0 (ví dụ `3.0`), AutoCAD sẽ "đóng đinh" chiều cao chữ này vĩnh viễn, bạn không thể thay đổi chiều cao chữ khi đo kích thước hoặc viết chữ được nữa!

## Cách dùng từng bước

### 1. Tạo kiểu chữ Unicode chuẩn (Khuyên dùng)
1. Gõ `ST` hoặc `STYLE` rồi nhấn [Enter].
2. Bấm nút **New** và đặt tên cho kiểu chữ: ví dụ `TCVN-TEXT` hoặc `CHU-GHI-CHU`.
3. Tại ô **Font Name**, chọn font `Arial` hoặc `Tahoma`.
4. Giữ nguyên ô **Height** là `0.0000`.
5. Tại ô **Width Factor** (hệ số co hẹp chiều ngang chữ), bạn có thể đặt `0.85` để chữ thon gọn hơn, tiết kiệm diện tích trên bản vẽ kỹ thuật.
6. Bấm **Apply** rồi bấm **Close**.

### 2. Thiết lập gõ tiếng Việt trong AutoCAD
- Mở Unikey hoặc EVKey trên máy tính.
- Chọn bảng mã: **Unicode** (dành cho font TTF như Arial, Time New Roman).
- Kiểu gõ: **Telex** hoặc **VNI** tùy thói quen.
- Khi gõ chữ bằng lệnh `MTEXT`, tiếng Việt sẽ hiển thị chuẩn xác không bị mất dấu hay biến thành hình ô vuông.

## Tuỳ chọn và mẹo

> [!TIP]
> Nếu bắt buộc phải dùng font SHX tiếng Việt (được chuyển giao từ các công ty cũ), hãy nhớ chọn thêm ô tick **Use Big Font** trong hộp thoại Style để chọn file phụ trợ tiếng Việt tương ứng.

> [!TIP]
> Để đổi kiểu chữ của hàng loạt đối tượng text đang có trên bản vẽ: Chọn tất cả chữ cần đổi, mở bảng thuộc tính [[Properties]] ([Ctrl + 1]), tại dòng `Style` chọn sang kiểu chữ mới vừa tạo.

## Tự kiểm tra

```quiz
id: q-ac-05-05-1
type: single
question: "Tại sao nên để thông số Height bằng 0 (0.0000) khi tạo Text Style trong AutoCAD?"
options:
  - text: "Để có thể linh hoạt thay đổi chiều cao chữ khi viết MTEXT hoặc khi gán vào DIMSTYLE"
    correct: true
    why: "Height = 0 biến kiểu chữ thành động, không cố định kích thước cưỡng bức."
  - text: "Để chữ tàng hình trên màn hình khi không muốn xem"
    correct: false
    why: "Chiều cao bằng 0 không làm chữ tàng hình khi vẽ."
  - text: "Để bản vẽ tự động dịch sang tiếng Anh"
    correct: false
    why: "Height không liên quan đến ngôn ngữ dịch thuật."
  - text: "Để máy tính tự động chọn màu chữ ngẫu nhiên"
    correct: false
    why: "Màu chữ do Layer quản lý."
explain: "Đặt Height bằng 0 là nguyên tắc số 1 trong AutoCAD để Dimstyle và lệnh viết chữ có thể tự quyết định kích thước chữ phù hợp."
```

```quiz
id: q-ac-05-05-2
type: single
question: "Để gõ tiếng Việt có dấu chuẩn xác với font chữ Arial trong AutoCAD, bạn cần chọn bảng mã nào trong phần mềm Unikey?"
options:
  - text: "Bảng mã Unicode"
    correct: true
    why: "Arial, Tahoma, Times New Roman là các font hệ thống theo bảng mã Unicode chuẩn quốc tế."
  - text: "Bảng mã TCVN3 (ABC)"
    correct: false
    why: "TCVN3 dùng cho các font bắt đầu bằng dấu chấm như .VnTime."
  - text: "Bảng mã VNI Windows"
    correct: false
    why: "VNI Windows dùng cho font có tiền tố VNI- như VNI-Helve."
  - text: "Bảng mã VIQR"
    correct: false
    why: "VIQR dùng các ký tự quy ước như o^? ít khi dùng vẽ kỹ thuật."
explain: "Font Arial và Tahoma sử dụng chuẩn Unicode dựng sẵn, tương thích hoàn hảo và phổ biến nhất hiện nay."
```

```quiz
id: q-ac-05-05-3
type: truefalse
question: "Width Factor trong hộp thoại Text Style nếu đặt bằng 0.8 sẽ làm các ký tự co thon gọn lại theo phương ngang so với mặc định 1.0."
answer: false
explain: "Trong bản vẽ kỹ thuật cơ khí và kiến trúc, Width Factor 0.8 đến 0.85 thường được dùng để chữ gọn gàng và tiết kiệm không gian."
```

## Lỗi thường gặp

- **Chữ bị biến thành dấu chấm hỏi (???):** Mở bản vẽ người khác gửi bị lỗi font do máy tính bạn thiếu file `.shx` hoặc font đó dùng bảng mã cũ không tương thích. Khắc phục: Dùng lệnh `STYLE`, đổi font của kiểu chữ đó về font phổ thông như `Arial`.
- **Kích thước chữ trong Dimstyle bị khóa cứng không đổi được:** Do trong `STYLE`, ô Height bị nhập một số khác 0. Khắc phục: Mở `STYLE`, sửa ô `Height` về `0`.

## Bài tập thực hành

- [ ] Gõ lệnh `STYLE` (hoặc `ST`) để mở hộp thoại Text Style. <!-- expect: STYLE -->
- [ ] Bấm nút **New**, đặt tên kiểu là `TCVN-ARIAL`.
- [ ] Chọn phông chữ `Arial`, kiểm tra chắc chắn ô `Height` là `0.0000`, đặt `Width Factor` là `0.85`. Bấm Apply và Set Current. <!-- expect: STYLE -->
- [ ] Dùng lệnh `MTEXT` viết một đoạn văn bản ghi chú tiếng Việt có dấu: "Chi tiết gia công theo tiêu chuẩn TCVN". <!-- expect: MTEXT -->

## Nguồn tham khảo

```links
- title: "Quản lý Text Style chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=STYLE"
  kind: official
```
