---
id: ac-06-02
title: Gán nhãn thông tin động với thuộc tính Block Attribute (ATTDEF)
category: Khối và Tham chiếu
tags: [attdef, attribute, eattedit, battman, block]
level: intermediate
minutes: 25
needs: [ac-06-01]
appVersions: ['2024', '2025']
edition: all
---
# Gán nhãn thông tin động với thuộc tính Block Attribute (ATTDEF)

> **Mục tiêu:**
> - Khai báo các trường thuộc tính văn bản thông minh bằng lệnh `ATTDEF`.
> - Đóng gói thuộc tính vào khối Block và nhập liệu trực tiếp khi chèn (`INSERT`).
> - Quản lý và đồng bộ hàng loạt thuộc tính với `EATTEDIT` và `BATTMAN`.

## Thuộc tính Block Attribute là gì?

Ở bài trước, bạn đã biết Block tĩnh giúp tái sử dụng hình vẽ. Nhưng hãy tưởng tượng:
- Bạn có khung tên bản vẽ kỹ thuật: Tên người vẽ, ngày vẽ, số hiệu bản vẽ ở mỗi tờ giấy là khác nhau.
- Bạn có ký hiệu trục cột: Vòng tròn giống hệt nhau nhưng bên trong lúc thì ghi chữ `A`, lúc thì ghi số `1`, `2`, `3`.
- Bạn có ký hiệu phòng: Vòng elip giống nhau nhưng bên trong ghi "Phòng Khách", "Phòng Ngủ", "Bếp".

Nếu dùng Block thông thường, bạn không thể đổi được chữ bên trong mà không làm đổi theo toàn bộ các block khác. Để giải quyết việc này, AutoCAD cung cấp **Thuộc tính Block ([[Attribute]])**.

Thuộc tính là một biến văn bản thông minh được tích hợp sẵn vào Block. Khi chèn Block vào bản vẽ, AutoCAD sẽ mở bảng hỏi để bạn điền giá trị riêng cho vị trí đó, đồng thời các dữ liệu này có thể tự động trích xuất ra bảng biểu sau này!

![Nguyên lý hoạt động của Block Attribute](media/ac-06-02-block-attributes.svg)

```hotspots
image: media/ac-06-02-block-attributes.svg
alt: Cấu tạo biến thuộc tính ATTDEF và các thể hiện khi chèn
layout: central
points:
  - id: spot-1
    x: 23
    y: 35
    title: Khai báo thuộc tính (ATTDEF)
    text: Tạo nhãn biến Tag 'PHONG_TEN' với giá trị mặc định 'Phòng Khách'.
  - id: spot-2
    x: 23
    y: 65
    title: Chế độ thuộc tính (Mode Flags)
    text: Tùy biến Invisible (ẩn chữ), Constant (cố định), Preset (điền tự động).
  - id: spot-3
    x: 67
    y: 35
    title: Thể hiện Block P101
    text: "Chèn vào bản vẽ và gán giá trị: Phòng Khách, diện tích 28.5 m²."
  - id: spot-4
    x: 67
    y: 60
    title: Thể hiện Block P102
    text: "Cùng 1 khối block nhưng mang giá trị riêng: Phòng Ngủ Master, 19.2 m²."
```

## 3 thông số cốt lõi trong ATTDEF

Khi gõ lệnh `ATTDEF` (Attribute Definition), hộp thoại xuất hiện với 3 ô nhập bắt buộc:
1. **Tag (Thẻ biến):** Tên định danh của thuộc tính, viết liền không dấu, không chứa khoảng trắng (ví dụ: `SO_HIEU`, `TEN_PHONG`, `DIEN_TICH`).
2. **Prompt (Lời nhắc):** Câu hỏi hiển thị khi người vẽ chèn Block (ví dụ: `Nhập số hiệu bản vẽ:`, `Nhập tên phòng:`).
3. **Default (Giá trị mặc định):** Giá trị tự động điền sẵn nếu người vẽ nhấn [Enter] bỏ qua (ví dụ: `P101` hoặc `01/10`).

## Cách dùng từng bước

### 1. Tạo Block có thuộc tính
1. Vẽ ký hiệu hình học (ví dụ: Vẽ một hình tròn đường kính 10mm làm ký hiệu trục tọa độ).
2. Gõ `ATTDEF` rồi nhấn [Enter].
3. Nhập:
   - `Tag`: `TEN_TRUC`
   - `Prompt`: `Nhập tên trục:`
   - `Default`: `A`
   - `Justification`: Chọn `Middle Center` (căn chính giữa tâm).
   - `Text height`: Nhập `3.5` mm.
4. Bấm **OK**, bấm chuột vào chính giữa tâm hình tròn để đặt chữ nhãn.
5. Gõ lệnh `BLOCK`, đặt tên là `TRUC-TOA-DO`. Bấm **Pick Point** chọn tâm hình tròn. Bấm **Select Objects** quét chọn cả hình tròn VÀ dòng nhãn `TEN_TRUC`. Bấm **OK**.

### 2. Chèn và nhập giá trị
1. Gõ lệnh `INSERT` (hoặc `I`).
2. Chèn Block `TRUC-TOA-DO` vào điểm cần đánh dấu.
3. Một hộp thoại hiển thị lên hỏi: "Nhập tên trục:".
4. Bạn gõ `B` rồi nhấn **OK**. Block lập tức hiển thị chữ `B` gọn gàng ở chính giữa!
5. Lặp lại chèn tiếp theo và gõ `C`, `D`, `1`, `2`...

### 3. Hiệu chỉnh giá trị thuộc tính với EATTEDIT và BATTMAN
- **Sửa giá trị của 1 Block đơn lẻ (`EATTEDIT`):**
  Chỉ cần **nhấp đúp chuột** vào khối block có thuộc tính. Hộp thoại *Enhanced Attribute Editor* sẽ mở ra cho phép bạn sửa lại chữ, đổi màu sắc hoặc lớp layer của riêng block đó.
- **Quản lý và đồng bộ toàn bộ Block (`BATTMAN`):**
  Lệnh `BATTMAN` (Block Attribute Manager) cho phép bạn đổi thứ tự các câu hỏi nhắc, xóa bớt thuộc tính thừa hoặc bấm nút **Sync** để cập nhật lại cấu trúc thuộc tính cho toàn bộ các Block đã chèn trước đó trong bản vẽ.

## Tuỳ chọn và mẹo quan trọng

> [!TIP]
> Nếu khi chèn Block mà không thấy hộp thoại hỏi giá trị hiện lên mà chỉ hỏi dưới thanh dòng lệnh, hãy gõ biến hệ thống `ATTDIA = 1` rồi nhấn Enter. Giá trị 1 sẽ kích hoạt giao diện hộp thoại đồ họa trực quan.

> [!TIP]
> Chọn chế độ `Invisible` trong ATTDEF nếu bạn muốn lưu trữ thông tin ngầm (ví dụ: mã nhà cung cấp, giá thành linh kiện) để phục vụ xuất thống kê sau này mà không muốn hiển thị dòng chữ đó làm rối bản vẽ in ấn.

## Tự kiểm tra

```quiz
id: q-ac-06-02-1
type: single
question: "Trong hộp thoại ATTDEF, ô thông số nào đóng vai trò là câu hỏi hướng dẫn hiển thị khi người vẽ chèn Block?"
options:
  - text: "Prompt"
    correct: true
    why: "Prompt là dòng chữ nhắc nhở người dùng nhập thông tin gì khi chèn block."
  - text: "Tag"
    correct: false
    why: "Tag là tên định danh biến của thuộc tính."
  - text: "Default"
    correct: false
    why: "Default là giá trị điền sẵn mặc định."
  - text: "Mode"
    correct: false
    why: "Mode là các chế độ hiển thị như ẩn hoặc cố định."
explain: "Prompt đóng vai trò là lời nhắc giao tiếp thân thiện (ví dụ: 'Nhập diện tích sàn:') khi thực hiện lệnh INSERT."
```

```quiz
id: q-ac-06-02-2
type: single
question: "Lệnh nào dùng để đồng bộ hóa (Sync) lại định nghĩa thuộc tính khi bạn vừa chỉnh sửa thêm/bớt tag trong Block gốc?"
options:
  - text: "BATTMAN"
    correct: true
    why: "BATTMAN (Block Attribute Manager) có nút Sync đồng bộ toàn diện các thay đổi thuộc tính."
  - text: "PURGE"
    correct: false
    why: "PURGE dùng để dọn dẹp đối tượng rác không dùng."
  - text: "EXPLODE"
    correct: false
    why: "EXPLODE sẽ phá vỡ khối block thành chữ thường, mất tính năng thuộc tính."
  - text: "REGEN"
    correct: false
    why: "REGEN chỉ làm mới lại bộ nhớ hiển thị đồ hoạ màn hình."
explain: "BATTMAN là công cụ đắc lực nhất để quản lý, sắp xếp và Sync toàn bộ thuộc tính của Block trong bản vẽ."
```

```quiz
id: q-ac-06-02-3
type: truefalse
question: "Biến hệ thống ATTDIA nếu đặt bằng 1 sẽ cho phép mở hộp thoại trực quan để nhập giá trị thuộc tính khi chèn Block."
answer: false
explain: "Khi không thấy hộp thoại nhập liệu xuất hiện, thiết lập ATTDIA = 1 sẽ khôi phục ngay cửa sổ nhập liệu đồ họa."
```

## Lỗi thường gặp

- **Thuộc tính không cập nhật sau khi sửa Block gốc trong BEDIT:** Bạn vào BEDIT sửa font hoặc di chuyển vị trí Tag, nhưng ra ngoài bản vẽ các block cũ vẫn không thay đổi. Khắc phục: Gõ lệnh `ATTSYNC` hoặc vào `BATTMAN` bấm nút **Sync**.
- **Tên Tag bị báo lỗi:** Nhập tên Tag có dấu cách hoặc tiếng Việt có dấu. Khắc phục: Tag phải viết liền không dấu (ví dụ: `SO_HIEU_BV`).
- **Phá nổ block làm thuộc tính biến thành tên Tag:** Dùng lệnh `EXPLODE` lên block thuộc tính khiến giá trị đã điền biến mất, chỉ còn trơ lại chữ Tag ban đầu. Khắc phục: Nếu muốn phá block mà giữ nguyên chữ đã điền, hãy dùng lệnh `BURST` trong bộ Express Tools thay vì `EXPLODE`.

## Bài tập thực hành

- [ ] Vẽ một hình tròn bán kính 5mm bằng lệnh `CIRCLE`. <!-- expect: CIRCLE -->
- [ ] Gõ `ATTDEF`, tạo thuộc tính có Tag là `TRUC_ID`, Prompt là `Nhap ky hieu truc:`, Default là `A`, căn giữa `Middle Center`. <!-- expect: ATTDEF -->
- [ ] Đặt chữ nhãn vào đúng tâm của hình tròn vừa vẽ.
- [ ] Gõ `BLOCK`, đặt tên là `BLOCK-TRUC`, chọn tâm hình tròn làm Base Point, quét chọn cả hình tròn và nhãn thuộc tính. <!-- expect: BLOCK -->
- [ ] Gõ `INSERT`, chèn 3 block liên tiếp và nhập giá trị lần lượt là `1`, `2`, `3`. <!-- expect: INSERT -->
- [ ] Nhấp đúp vào block số 2 để mở hộp thoại `EATTEDIT` và đổi giá trị thành `2A`. <!-- expect: EATTEDIT -->

## Nguồn tham khảo

```links
- title: "Định nghĩa thuộc tính ATTDEF chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=ATTDEF"
  kind: official
- title: "Quản lý thuộc tính với BATTMAN từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=BATTMAN"
  kind: official
```
