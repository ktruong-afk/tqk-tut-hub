---
id: ac-06-08
title: Tổ chức và chuẩn hoá kho thư viện Block cho doanh nghiệp
category: Khối và Tham chiếu
tags: [thu-vien, purge, audit, chuan-hoa, quy-trinh]
level: intermediate
minutes: 25
needs: [ac-06-04, ac-06-05]
appVersions: ['2024', '2025']
edition: all
---
# Tổ chức và chuẩn hoá kho thư viện Block cho doanh nghiệp

> **Mục tiêu:**
> - Xây dựng hệ thống cấu trúc thư mục và quy tắc đặt tên Block chuẩn hóa cho doanh nghiệp.
> - Sử dụng lệnh `PURGE` để dọn dẹp triệt để các định nghĩa khối và thuộc tính rác không dùng tới.
> - Kiểm tra và sửa lỗi cơ sở dữ liệu bản vẽ với lệnh `AUDIT`.

## Tầm quan trọng của chuẩn hóa thư viện Block

Một trong những vấn đề nhức nhối nhất tại các phòng thiết kế là tình trạng "thư viện rác":
- Kỹ sư A tải một cái ghế sofa từ trên mạng về, dán vào bản vẽ mang theo 20 layer lạ hoắc màu mè.
- Kỹ sư B đặt tên block là `cua1`, kỹ sư C đặt tên là `Door_go`, kỹ sư D đặt tên là `D900_final_v2`.
- Bản vẽ phình to từ 1MB lên 50MB, mở máy mất 3 phút, in ấn bị lỗi nét và không thể nào bóc tách khối lượng tự động được.

Để làm việc chuyên nghiệp, mọi công ty tư vấn thiết kế và doanh nghiệp sản xuất đều phải thiết lập một **Quy chuẩn thư viện Block (CAD Standards)** thống nhất.

## 4 quy tắc vàng khi tạo thư viện Block chuẩn

1. **Quy tắc Layer 0:** Toàn bộ nét vẽ tạo Block phải vẽ trên `Layer 0`, thuộc tính màu sắc (`Color`), kiểu đường (`Linetype`) và độ dày nét (`Lineweight`) phải để **ByLayer** (hoặc **ByBlock** nếu cần kiểm soát linh động).
2. **Quy tắc Điểm đặt (Base Point):** Luôn chọn điểm đặt có ý nghĩa thực tế (ví dụ: góc bản lề cho cửa, tâm cho bu lông/cột, trung điểm cạnh dưới cho thiết bị vệ sinh). Không bao giờ để điểm đặt tùy tiện.
3. **Quy tắc Đơn vị (Block Units):** Khi tạo Block trong hộp thoại `BLOCK`, ô **Block unit** phải luôn chọn đúng đơn vị thực tế vẽ (ví dụ: `Millimeters`). Nếu để `Unitless` hoặc `Inches`, khi chèn vào bản vẽ hệ mét block có thể bị phóng to 25.4 lần!
4. **Quy tắc Đặt tên (Naming Convention):** Đặt tên theo cú pháp phân cấp có tiền tố chuyên ngành:
   - `KT_CUA_DI_D900` (Kiến trúc - Cửa đi - Rộng 900)
   - `KC_COT_VUONG_C400x400` (Kết cấu - Cột vuông - 400x400)
   - `CK_BULONG_M16x60` (Cơ khí - Bu lông M16 dài 60)
   - `MEP_DEN_DOWNLIGHT_D110` (Cơ điện - Đèn âm trần D110)

## Dọn dẹp tệp bản vẽ với lệnh PURGE

Khi bạn xóa một khối block khỏi màn hình bằng lệnh `ERASE`, định nghĩa ngầm của khối đó vẫn tồn tại trong cơ sở dữ liệu của file DWG. Càng vẽ lâu, file càng tích tụ hàng trăm khối "ma" khiến dung lượng nặng nề.

Lệnh **`PURGE` (Lệnh tắt `PU`)** là công cụ thanh lọc rác tối thượng:
1. Gõ `PU` hoặc `PURGE` rồi nhấn [Enter].
2. Bấm vào nút **Purge All** ở dưới cùng.
3. Nếu hộp thoại xác nhận hiện ra, chọn **Purge all items**.
4. Lặp lại thao tác cho đến khi nút *Purge All* mờ đi (không còn đối tượng rác nào).
5. Dung lượng tệp DWG có thể giảm ngay từ 50% đến 80%!

## Sửa lỗi cơ sở dữ liệu với lệnh AUDIT

Khi bản vẽ thường xuyên bị văng lỗi (Crash), giật lag hoặc thông báo cảnh báo file bị hỏng, hãy chạy lệnh **`AUDIT`**:
1. Gõ `AUDIT` rồi nhấn [Enter].
2. AutoCAD hỏi: `Fix any errors detected? [Yes/No] <N>:`.
3. Gõ `Y` rồi nhấn [Enter].
4. AutoCAD sẽ tự động quét toàn bộ cây cơ sở dữ liệu hình học, phát hiện và sửa chữa ngay lập tức tất cả các bản ghi lỗi hoặc con trỏ rỗng.
5. Dòng lệnh sẽ thông báo kết quả: `Total errors found 0, fixed 0` (hoặc đã sửa bao nhiêu lỗi).

## Quy trình đóng gói và chia sẻ kho thư viện

Để toàn bộ phòng ban có thể cùng sử dụng chung kho block:
1. Gom các khối theo từng chủ đề vào các file DWG tổng (ví dụ: `THU-VIEN-CUA.dwg`, `THU-VIEN-NOI-THAT.dwg`).
2. Đặt các tệp này trên ổ đĩa mạng nội bộ chung của công ty (Read-Only để tránh người dùng vô tình ghi đè làm hỏng).
3. Sử dụng **Tool Palettes** kết nối tới các tệp này để toàn bộ kỹ sư chỉ việc kéo thả sử dụng hàng ngày.

> [!TIP]
> Hãy kết hợp bộ ba lệnh: `AUDIT` $\to$ `PURGE` $\to$ `SAVE` như một nghi thức bắt buộc trước khi bàn giao bất kỳ tệp bản vẽ nào cho khách hàng hoặc đối tác!

## Tự kiểm tra

```quiz
id: q-ac-06-08-1
type: single
question: "Lệnh nào trong AutoCAD chuyên dùng để quét và dọn sạch các định nghĩa Block, Layer, Dimstyle rác không còn sử dụng để giảm dung lượng file?"
options:
  - text: "PURGE (PU)"
    correct: true
    why: "PURGE xóa sạch các định nghĩa đối tượng không còn đối tượng thực thể nào tham chiếu."
  - text: "ERASE (E)"
    correct: false
    why: "ERASE chỉ xóa đối tượng hiển thị trên màn hình, không xóa định nghĩa ngầm."
  - text: "EXPLODE (X)"
    correct: false
    why: "EXPLODE làm nổ đối tượng, càng làm tăng thêm số lượng nét rời."
  - text: "REGEN (RE)"
    correct: false
    why: "REGEN chỉ làm mới bộ nhớ hiển thị đồ họa."
explain: "Lệnh PURGE là công cụ tiêu chuẩn giúp thanh lọc tệp bản vẽ sạch sẽ và giảm thiểu tối đa dung lượng bộ nhớ."
```

```quiz
id: q-ac-06-08-2
type: single
question: "Khi bản vẽ bị lỗi giật lag, xuất hiện cảnh báo hỏng hóc hoặc tự động thoát phần mềm, lệnh đầu tiên bạn nên chạy để sửa lỗi cơ sở dữ liệu là gì?"
options:
  - text: "AUDIT"
    correct: true
    why: "AUDIT kiểm tra tính toàn vẹn cấu trúc dữ liệu và tự động sửa các lỗi bản ghi bị hỏng."
  - text: "SCALE"
    correct: false
    why: "SCALE dùng để phóng to thu nhỏ hình học."
  - text: "ARRAY"
    correct: false
    why: "ARRAY dùng để sao chép mảng hàng cột."
  - text: "TRIM"
    correct: false
    why: "TRIM dùng để cắt tỉa đối tượng."
explain: "Chạy AUDIT với tùy chọn Fix Errors = Yes là phương pháp phục hồi dữ liệu bản vẽ CAD hiệu quả và nhanh chóng nhất."
```

```quiz
id: q-ac-06-08-3
type: truefalse
question: "Toàn bộ các nét vẽ bên trong một khối Block thư viện chuẩn nên được vẽ trên Layer 0 với thuộc tính màu sắc ByLayer."
answer: false
explain: "Tuân thủ quy tắc Layer 0 giúp bản vẽ luôn sạch sẽ, tránh sinh ra các layer rác ngoài ý muốn khi chèn thư viện vào tệp dự án."
```

## Lỗi thường gặp

- **Chèn Block vào bị sinh ra hàng chục layer lạ:** Do người tạo Block vẽ nét trên các layer lung tung (như Defpoints, Dim, Nét thấy) thay vì vẽ trên Layer 0. Khắc phục: Dùng `BEDIT` mở khối ra, quét toàn bộ hình và đổi sang `Layer 0` với màu `ByLayer`.
- **Kích thước Block bị méo hoặc quá to:** Do không đồng bộ đơn vị Block Units khi tạo khối (ví dụ để Inches chèn vào tệp Millimeters).

## Bài tập thực hành

- [ ] Gõ `PURGE` (hoặc `PU`), bấm nút **Purge All** để dọn sạch toàn bộ các đối tượng rác trong bản vẽ hiện tại. <!-- expect: PURGE -->
- [ ] Gõ lệnh `AUDIT`, chọn `Y` (Yes) để kiểm tra và sửa lỗi cơ sở dữ liệu. <!-- expect: AUDIT -->
- [ ] Quan sát dòng lệnh hiển thị số lượng lỗi đã được phát hiện và khắc phục.
- [ ] Lưu lại bản vẽ để nhận thấy dung lượng tệp tin đã được tối ưu tinh gọn.

## Nguồn tham khảo

```links
- title: "Dọn dẹp bản vẽ với lệnh PURGE từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=PURGE"
  kind: official
- title: "Sửa lỗi tệp DWG bằng lệnh AUDIT từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=AUDIT"
  kind: official
```
