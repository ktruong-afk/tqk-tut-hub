---
id: ac-08-02
title: Kiểm soát chất lượng bản vẽ với tiêu chuẩn CAD Standards (DWS)
category: Nâng cao năng suất
tags: [standards, checkstandards, dws, quan-ly-chat-luong, quy-chuan]
level: advanced
minutes: 25
needs: [ac-08-01]
appVersions: ['2024', '2025']
edition: all
---
# Kiểm soát chất lượng bản vẽ với tiêu chuẩn CAD Standards (DWS)

> **Mục tiêu:**
> - Khởi tạo tệp tiêu chuẩn kiểm tra bản vẽ [[CAD Standards]] (đuôi `.dws`).
> - Sử dụng lệnh `STANDARDS` để cấu hình bộ tiêu chuẩn kiểm tra cho tệp dự án.
> - Quét phát hiện và tự động khắc phục các lỗi sai lệch tiêu chuẩn layer, font chữ, dimstyle với `CHECKSTANDARDS`.

## Nỗi lo "lệch chuẩn" trong các dự án làm việc nhóm

Trong một văn phòng thiết kế có 10 kỹ sư cùng làm việc:
- Kỹ sư A vẽ layer tường màu đỏ, kỹ sư B vẽ layer tường màu vàng.
- Kỹ sư C tự tiện tạo kiểu chữ `VNI-Helve` trong khi quy chuẩn công ty bắt buộc dùng `Arial Unicode`.
- Kỹ sư D tự ý sửa mũi tên kích thước thành chấm tròn.

Trước khi bàn giao hồ sơ cho khách hàng, người trưởng nhóm (BIM/CAD Manager) phải mở từng bản vẽ ra kiểm tra xem có ai vẽ sai quy định hay không. Việc kiểm tra thủ công bằng mắt trên hàng trăm bản vẽ vừa mất thời gian vừa dễ bỏ sót lỗi.

**[[CAD Standards]] (Bộ tiêu chuẩn CAD)** là công cụ cảnh sát tự động của AutoCAD:
Nó cho phép bạn tạo một file tiêu chuẩn làm "thước đo chân lý" (đuôi `.dws`). Bất cứ khi nào có ai vẽ sai tên layer, sai mã màu, hoặc dùng font chữ lạ, AutoCAD sẽ **bật còi báo động ngay lập tức** và đưa ra phương án sửa lỗi chỉ bằng 1 nút bấm!

## 4 đối tượng được CAD Standards giám sát chặt chẽ

1. **Layers:** Kiểm tra tên layer, màu sắc, kiểu đường `Linetype`, độ dày nét `Lineweight`.
2. **Text Styles:** Kiểm tra tên kiểu chữ, phông chữ, chiều cao và hệ số `Width Factor`.
3. **Dimension Styles:** Kiểm tra toàn bộ các thông số kích thước, mũi tên, khoảng nhô đường gióng.
4. **Linetypes:** Kiểm tra định nghĩa các loại nét vẽ đứt khúc.

## Cách dùng từng bước

### 1. Tạo tệp tiêu chuẩn chuẩn mực (.dws)
1. Mở file template chuẩn `TCVN-MAU-CHUAN.dwt` (hoặc một bản vẽ đã được chuẩn hóa 100%).
2. Chọn **Save As** > tại mục *Files of type*, chọn định dạng **`AutoCAD Drawing Standards (*.dws)`**.
3. Lưu tệp với tên: **`CONG-TY-CHUAN.dws`**. Tệp này đóng vai trò là "luật chuẩn" của công ty.

### 2. Cấu hình kiểm tra cho bản vẽ với lệnh STANDARDS
1. Mở bản vẽ cần kiểm tra (ví dụ một bản vẽ do cộng tác viên mới gửi tới).
2. Gõ `STANDARDS` rồi nhấn [Enter] (hoặc vào menu *Manage* > cụm *CAD Standards* > chọn **Configure**).
3. Hộp thoại **Configure Standards** mở ra:
   - Thẻ **Standards**: Bấm nút dấu cộng `[+]` màu xanh (*Add Standards File*).
   - Duyệt tìm và chọn file `CONG-TY-CHUAN.dws` vừa tạo ở bước 1.
   - Thẻ **Plug-ins**: Đánh dấu tick vào cả 4 mục (Dimension Styles, Layers, Linetypes, Text Styles).
4. Bấm nút **Check Standards...** ngay trong hộp thoại (hoặc bấm OK đóng lại).

### 3. Quét lỗi và sửa tự động với CHECKSTANDARDS
1. Gõ lệnh `CHECKSTANDARDS` rồi nhấn [Enter].
2. Hộp thoại **Check Standards** xuất hiện và bắt đầu quét toàn bộ bản vẽ:
   - Nếu phát hiện vi phạm, phần mềm sẽ dừng lại và hiển thị chi tiết:
     *"Problem: Layer 'Net_Tuong' is non-standard"* (Layer này không có trong quy chuẩn công ty).
   - Tại khung bên dưới **Replace with**: AutoCAD gợi ý danh sách các layer chuẩn trong file DWS. Bạn bấm chọn layer chuẩn `TUONG_XAY`.
   - Bấm nút **Fix**: Toàn bộ các đối tượng đang nằm ở layer sai `Net_Tuong` sẽ lập tức được chuyển sang layer chuẩn `TUONG_XAY`, đồng thời layer sai sẽ bị xóa sạch!
   - Nếu lỗi là font chữ sai: Bấm chọn font chuẩn `Arial` rồi bấm **Fix**.
3. Cứ như vậy, bấm **Next** để duyệt qua toàn bộ các lỗi cho đến khi màn hình thông báo: *"Check complete. 0 problems found"*. Bản vẽ đã hoàn toàn sạch sẽ và chuẩn hóa 100%!

## Bật tính năng cảnh báo thời gian thực (Real-time Notification)

Bạn có thể cấu hình để AutoCAD cảnh báo ngay khi kỹ sư đang vẽ:
- Trong hộp thoại `STANDARDS`, bấm nút **Settings...**.
- Tại mục *Notification settings*, chọn **Display alert upon standards violation**.
- Giờ đây, nếu bất kỳ ai tạo một layer mới lệch chuẩn, một biểu tượng cảnh báo nhỏ sẽ nhấp nháy ở khay hệ thống góc dưới màn hình để nhắc nhở họ tuân thủ quy chuẩn!

> [!TIP]
> Sử dụng công cụ độc lập `Batch Standards Checker` (đi kèm bộ cài AutoCAD trong Windows Start Menu) để quét và xuất báo cáo vi phạm HTML cho cùng lúc hàng trăm bản vẽ của toàn bộ dự án mà không cần mở từng file một!

## Tự kiểm tra

```quiz
id: q-ac-08-02-1
type: single
question: "Định dạng phần mở rộng (đuôi tệp) của file lưu trữ quy chuẩn kiểm tra bản vẽ CAD Standards là gì?"
options:
  - text: ".dws"
    correct: true
    why: "DWS viết tắt của Drawing Standards File."
  - text: ".dwg"
    why: "DWG là tệp bản vẽ thiết kế thông thường."
  - text: ".dwt"
    why: "DWT là file mẫu Drawing Template."
  - text: ".dxe"
    why: "DXE là file cấu hình trích xuất dữ liệu Data Extraction."
explain: "Tệp .dws là tệp khuôn mẫu quy chuẩn dùng để kiểm tra đối chiếu sai sót cho các tệp DWG trong dự án."
```

```quiz
id: q-ac-08-02-2
type: single
question: "Lệnh nào trong AutoCAD khởi chạy trình thuật sĩ quét và tự động thay thế (Fix) các đối tượng lệch chuẩn layer, text, dim trong bản vẽ?"
options:
  - text: "CHECKSTANDARDS"
    correct: true
    why: "CHECKSTANDARDS là lệnh quét và sửa chữa vi phạm tiêu chuẩn CAD Standards."
  - text: "SPELL"
    why: "SPELL dùng để kiểm tra chính tả tiếng Anh."
  - text: "AUDIT"
    why: "AUDIT sửa lỗi cấu trúc cơ sở dữ liệu tệp tin."
  - text: "PURGE"
    why: "PURGE xóa bỏ đối tượng rác không dùng."
explain: "Sử dụng lệnh CHECKSTANDARDS để quét lỗi vi phạm tiêu chuẩn và tự động thay thế bằng các thuộc tính chuẩn của công ty."
```

```quiz
id: q-ac-08-02-3
type: truefalse
question: "CAD Standards có khả năng phát hiện khi một layer có cùng tên nhưng bị đặt sai mã màu hoặc sai độ dày nét so với tiêu chuẩn công ty."
answer: true
explain: "CAD Standards kiểm tra toàn diện cả 4 thuộc tính của Layer: tên, màu sắc, linetype và lineweight để đảm bảo tính đồng bộ tuyệt đối."
```

## Lỗi thường gặp

- **Bấm Check Standards nhưng không thấy báo gì:** Do chưa liên kết tệp `.dws` trong lệnh `STANDARDS`. Khắc phục: Gõ `STANDARDS` và bấm nút `[+]` để chỉ định file DWS chuẩn.
- **Bị cảnh báo liên tục gây khó chịu khi đang vẽ phác thảo:** Do bật chế độ cảnh báo thời gian thực. Khắc phục: Trong Settings của Standards chọn *Automatically check standards: Off* và chỉ chạy kiểm tra tổng thể trước khi nộp bản vẽ.

## Bài tập thực hành

- [ ] Gõ lệnh `STANDARDS` để mở hộp thoại Configure Standards. <!-- expect: STANDARDS -->
- [ ] Quan sát các thẻ kiểm tra Plug-ins: `Dimension Styles`, `Layers`, `Linetypes`, `Text Styles`.
- [ ] Gõ lệnh `CHECKSTANDARDS` để khởi chạy trình kiểm tra tiêu chuẩn bản vẽ. <!-- expect: CHECKSTANDARDS -->
- [ ] Đóng hộp thoại kiểm tra.

## Nguồn tham khảo

```links
- title: "Tổng quan về CAD Standards từ Autodesk Knowledge Network"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+CAD+Standards"
  kind: official
- title: "Lệnh CHECKSTANDARDS kiểm tra tiêu chuẩn từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=CHECKSTANDARDS"
  kind: official
```
