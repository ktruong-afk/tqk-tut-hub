---
id: ac-01-04
title: Thiết lập đơn vị đo và Template mẫu bản vẽ
category: Làm quen
tags: [units, template, dwt, metric, acadiso]
level: beginner
minutes: 15
needs: [ac-01-02]
appVersions: ['2024', '2025']
edition: all
---
# Thiết lập đơn vị đo và Template mẫu bản vẽ

> **Mục tiêu:**
> - Thiết lập đơn vị đo độ dài và góc chính xác cho bản vẽ kỹ thuật bằng lệnh UNITS.
> - Phân biệt giữa template hệ mét (acadiso.dwt) và hệ inch (acad.dwt).
> - Kiểm soát độ chính xác thập phân và đơn vị chèn khối (Insertion scale).

## Lệnh này làm gì và khi nào dùng

Trong bản vẽ kỹ thuật, mọi kích thước đều phải gắn liền với một [[Đơn vị đo]] xác định (milimet, mét hoặc inch). Nếu bạn bắt đầu vẽ mà không kiểm tra đơn vị, một đường thẳng dài 100 có thể bị hiểu là 100 milimet hoặc 100 inch, dẫn đến sai lệch nghiêm trọng khi in ấn hoặc lắp ghép mô hình.

AutoCAD cung cấp sẵn các [[Mẫu bản vẽ]] tiêu chuẩn:
- **`acadiso.dwt`:** Template chuẩn quốc tế theo hệ mét (Metric - milimet), phù hợp với tiêu chuẩn Việt Nam (TCVN) và ISO.
- **`acad.dwt`:** Template theo hệ inch (Imperial - feet, inch), dùng cho tiêu chuẩn Mỹ.

Lệnh `UNITS` cho phép bạn kiểm tra và thay đổi định dạng hiển thị toạ độ, số chữ số sau dấu phẩy và đơn vị tỷ lệ khi chèn thư viện.

## Cách dùng từng bước

1. **Khởi tạo đúng template hệ mét:** Gõ lệnh `NEW`, trong danh sách file mẫu chọn tệp `acadiso.dwt` rồi bấm Open.
2. **Mở hộp thoại thiết lập đơn vị:** Gõ `UNITS` (hoặc phím tắt `UN`) rồi nhấn [Enter]. Hộp thoại *Drawing Units* sẽ xuất hiện.
3. **Cài đặt độ dài (Length):**
   - *Type:* Chọn `Decimal` (số thập phân thông thường).
   - *Precision:* Chọn `0.00` (độ chính xác đến 2 chữ số thập phân).
4. **Cài đặt góc (Angle):**
   - *Type:* Chọn `Decimal Degrees` (độ thập phân).
   - *Precision:* Chọn `0` hoặc `0.0`.
   - *Clockwise:* Mặc định để trống (chiều quay góc ngược chiều kim đồng hồ là chiều dương).
5. **Đơn vị chèn khối (Insertion Scale):**
   - *Units to scale inserted content:* Chọn `Millimeters`.
6. **Lưu cài đặt:** Bấm **OK** để áp dụng cho bản vẽ hiện hành.

## Tuỳ chọn và mẹo

> [!TIP]
> Hãy luôn bắt đầu bản vẽ cơ khí hoặc xây dựng tại Việt Nam bằng mẫu `acadiso.dwt` thay vì `acad.dwt`. Bản `acadiso.dwt` đã cấu hình sẵn linetype và hatch theo hệ mét chuẩn xác.

> [!TIP]
> Lệnh `UNITS` chỉ quy định cách hiển thị và đơn vị tương thích khi chèn khối; nó không tự động phóng to hay thu nhỏ các hình học bạn đã vẽ trước đó.

## Tự kiểm tra

```quiz
id: q-ac-01-04-1
type: single
question: Mẫu bản vẽ (template) tiêu chuẩn nào trong AutoCAD được cấu hình sẵn theo hệ mét (Metric)?
options:
  - { text: acadiso.dwt, correct: true, why: acadiso.dwt là template chuẩn quốc tế hệ mét (milimet) }
  - { text: acad.dwt, why: acad.dwt là template theo hệ inch của Mỹ }
  - { text: tutorial-i.dwt, why: tutorial-i là mẫu hướng dẫn hệ inch }
  - { text: standard.dwt, why: AutoCAD không có file mẫu mặc định tên standard.dwt }
explain: File mẫu acadiso.dwt (ISO) được xây dựng riêng cho các nước sử dụng hệ đo lường mét (milimet), phù hợp với tiêu chuẩn kỹ thuật Việt Nam.
tags: [units, template, acadiso]
```

```quiz
id: q-ac-01-04-2
type: single
question: Lệnh nào dùng để mở hộp thoại cài đặt đơn vị đo và độ chính xác trong bản vẽ?
options:
  - { text: UNITS, correct: true, why: Lệnh UNITS (gõ tắt UN) mở hộp thoại Drawing Units }
  - { text: LIMITS, why: LIMITS dùng để đặt giới hạn vùng vẽ }
  - { text: SCALE, why: SCALE dùng để phóng to thu nhỏ đối tượng }
  - { text: DIMSTYLE, why: DIMSTYLE dùng để quản lý kiểu kích thước }
explain: Gõ lệnh UNITS (phím tắt UN) giúp bạn kiểm soát định dạng số đo chiều dài, góc và đơn vị chèn khối cho toàn bộ bản vẽ.
tags: [units, lenh]
```

```quiz
id: q-ac-01-04-3
type: truefalse
question: Trong AutoCAD, chiều quay góc mặc định được quy ước là cùng chiều kim đồng hồ.
answer: false
explain: Ngược lại, quy ước toán học chuẩn của AutoCAD là góc 0 độ nằm theo phương ngang hướng sang phải (hướng Đông) và tăng dần ngược chiều kim đồng hồ.
tags: [units, goc]
```

## Lỗi thường gặp

- **Triệu chứng:** Khi chèn block hoặc hình vẽ từ file khác vào, hình bị nhỏ đi 25.4 lần hoặc to lên 25.4 lần.
  - *Nguyên nhân:* Một file đang đặt đơn vị là *Inches* còn file kia đặt là *Millimeters*. Tỷ lệ chuyển đổi giữa inch và mm chính là 25.4.
  - *Cách sửa:* Dùng lệnh `UNITS` trên cả hai file và đồng nhất mục *Units to scale inserted content* về `Millimeters`.
- **Triệu chứng:** Nét đứt (Dashed, Hidden) hiển thị như nét liền khi vẽ theo hệ mét.
  - *Nguyên nhân:* Bản vẽ đang khởi tạo từ mẫu hệ inch `acad.dwt` nên tỷ lệ nét đứt quá nhỏ so với kích thước mm.
  - *Cách sửa:* Tạo bản vẽ mới từ mẫu `acadiso.dwt` hoặc dùng lệnh `MEASUREMENT` chuyển giá trị về `1`.

## Bài tập thực hành

- [ ] Gõ `NEW` và chọn template `acadiso.dwt` để bắt đầu bản vẽ mới. <!-- expect: NEW -->
- [ ] Gõ `UNITS` và nhấn [Enter] để mở hộp thoại Drawing Units. <!-- expect: UNITS -->
- [ ] Thiết lập mục *Length Type* thành `Decimal` và *Precision* thành `0.00`.
- [ ] Kiểm tra mục *Insertion scale* và xác nhận đơn vị đã là `Millimeters` rồi bấm OK.

## Nguồn tham khảo

```links
- title: Lệnh UNITS và quản lý đơn vị bản vẽ (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=UNITS+Command
  kind: official
  lang: en
  note: Hướng dẫn cấu hình hệ đo lường chiều dài, góc và đơn vị chèn khối chuẩn xác
- title: Mẫu bản vẽ DWT và chuẩn hệ mét (Autodesk Support)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Drawing+Templates
  kind: official
  lang: en
  note: Giải thích sự khác biệt giữa acad.dwt và acadiso.dwt
```
