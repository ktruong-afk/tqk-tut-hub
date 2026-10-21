---
id: ac-02-10
title: Tạo chữ ghi chú với lệnh TEXT và MTEXT
category: Vẽ 2D
tags: [text, mtext, ve-2d, ghi-chu, font, chu-viet]
level: beginner
minutes: 15
needs: [ac-02-01]
appVersions: ['2024', '2025']
edition: all
---
# Tạo chữ ghi chú với lệnh TEXT và MTEXT

> **Mục tiêu:**
> - Phân biệt mục đích sử dụng của chữ đơn dòng (TEXT / DTEXT) và chữ đa dòng (MTEXT).
> - Thiết lập chiều cao chữ (Text Height), điểm căn lề (Justification) và góc xoay (Rotation).
> - Chèn các ký hiệu kỹ thuật đặc thù như đường kính phi (%%c hoặc Ø) và độ (%%d hoặc °).

## Lệnh này làm gì và khi nào dùng

Một bản vẽ kỹ thuật hoàn chỉnh không thể chỉ có đường nét hình học mà bắt buộc phải có câu chữ ghi chú: tên bản vẽ, vật liệu chi tiết, yêu cầu kỹ thuật và bảng kê khung tên.

AutoCAD cung cấp hai công cụ tạo chữ chính:
- `TEXT` (hoặc `DTEXT`, phím tắt `DT`): Tạo [[Chữ đơn dòng]] (Single-line Text). Thích hợp cho các nhãn ngắn gọn, số phòng, tên trục toạ độ hoặc các ô điền thông tin trong khung tên. Mỗi lần nhấn Enter xuống dòng, AutoCAD sẽ tạo ra một thực thể chữ độc lập.
- `MTEXT` (phím tắt `MT` hoặc `T`): Tạo [[Chữ đa dòng]] (Multiline Text). Hoạt động tương tự như một phần mềm soạn thảo văn bản Word thu nhỏ với khung viền, chia cột, đánh số thứ tự đầu dòng tự động, căn lề hai bên và chèn ký hiệu kỹ thuật phong phú.

## Cách dùng từng bước

1. **Tạo chữ đa dòng (MTEXT - Khuyến nghị cho đoạn văn):**
   - Gõ `MTEXT` hoặc phím tắt `T` rồi nhấn [Enter].
   - Nhấp chuột kéo một khung chữ nhật để xác định chiều rộng đoạn văn bản.
   - Trình soạn thảo *Text Editor* hiện ra trên Ribbon. Gõ nội dung văn bản kỹ thuật.
   - Bôi đen chữ và chỉnh chiều cao chữ trong ô **Text Height** (ví dụ `2.5`mm hoặc `3.5`mm).
   - Nhấp nút **Close Text Editor** hoặc bấm chuột ra ngoài vùng vẽ để lưu.
2. **Chèn ký hiệu kỹ thuật trong MTEXT:**
   - Trong lúc đang gõ, bấm nút **Symbol** (ký hiệu @) trên thanh Ribbon hoặc gõ mã tắt:
     - Gõ `%%c` để sinh ra ký hiệu đường kính phi `Ø` (ví dụ `%%c50` thành `Ø50`).
     - Gõ `%%d` để sinh ra ký hiệu độ `°` (ví dụ `45%%d` thành `45°`).
     - Gõ `%%p` để sinh ra dung sai cộng trừ `±` (ví dụ `%%p0.05` thành `±0.05`).
3. **Tạo chữ đơn dòng nhanh (TEXT):**
   - Gõ `TEXT` hoặc `DT` rồi nhấn [Enter].
   - Bấm điểm đặt chữ (Start point).
   - Nhập chiều cao chữ (Specify height, ví dụ `3.0`) rồi [Enter].
   - Nhập góc nghiêng chữ (Specify rotation angle, mặc định `0`) rồi [Enter].
   - Gõ nội dung chữ, nhấn [Enter] để xuống dòng tiếp theo hoặc nhấn [Enter] hai lần để kết thúc.

## Tuỳ chọn và mẹo

> [!TIP]
> Trong bản vẽ kỹ thuật theo tiêu chuẩn TCVN, chiều cao chữ thường dùng các cỡ chuẩn: `2.5`mm (ghi chú thứ cấp, kích thước), `3.5`mm (chữ tiêu chuẩn chung), `5.0`mm (tiêu đề mục) và `7.0`mm (tên bản vẽ chính).

> [!TIP]
> Luôn dùng mã phím tắt nhanh `%%c` cho đường kính và `%%d` cho độ khi gõ chữ trong AutoCAD; mã này hoạt động chuẩn xác trên cả lệnh TEXT lẫn MTEXT.

## Tự kiểm tra

```quiz
id: q-ac-02-10-1
type: single
question: Trong AutoCAD, khi gõ mã nào vào chuỗi văn bản thì phần mềm sẽ tự động chuyển thành ký hiệu đường kính phi (Ø)?
options:
  - text: "%%c"
    correct: true
    why: "Mã %%c sinh ra ký hiệu đường kính Ø"
  - text: "%%d"
    why: "Mã %%d sinh ra ký hiệu độ °"
  - text: "%%p"
    why: "Mã %%p sinh ra ký hiệu dung sai ±"
  - text: "%%u"
    why: "Mã %%u bật tắt gạch chân chữ"
explain: "Ký tự điều khiển %%c (viết tắt của circle/diameter) trong AutoCAD được dùng để hiển thị ký hiệu đường kính Ø trong mọi phông chữ kỹ thuật."
tags: [text, mtext, ky-hieu, phi]
```

```quiz
id: q-ac-02-10-2
type: single
question: Khi bạn gõ 3 dòng chữ bằng lệnh TEXT (Single-line Text) rồi kết thúc lệnh, AutoCAD sẽ tạo ra bao nhiêu đối tượng chữ trong bản vẽ?
options:
  - text: 3 đối tượng chữ độc lập riêng biệt
    correct: true
    why: Mỗi dòng của lệnh TEXT là một thực thể chữ riêng rẽ
  - text: 1 đối tượng chữ duy nhất dạng đoạn văn
    why: Đó là cách hoạt động của lệnh MTEXT
  - text: 1 đối tượng block
    why: Lệnh TEXT không tạo block
  - text: Không tạo ra đối tượng nào
    why: Chữ được lưu bình thường
explain: "Lệnh TEXT (DTEXT) xem mỗi lần xuống dòng là một thực thể chữ độc lập. Nếu bạn muốn toàn bộ các dòng liên kết trong một khối văn bản duy nhất, bạn phải dùng lệnh MTEXT."
tags: [text, dtext, so-sanh]
```

```quiz
id: q-ac-02-10-3
type: truefalse
question: Lệnh MTEXT cho phép bạn chia cột văn bản, chèn số thứ tự tự động và căn lề hai bên tương tự như phần mềm soạn thảo văn phòng.
answer: true
explain: "MTEXT (Multiline Text) tích hợp một bộ soạn thảo văn bản phong phú đầy đủ tính năng căn lề Justify, chia Columns và Bullets/Numbering."
tags: [mtext, tinh-nang]
```

## Lỗi thường gặp

- **Triệu chứng:** Chữ gõ tiếng Việt bị lỗi font biến thành dấu chấm hỏi `???` hoặc ký tự hình vuông kỳ lạ.
  - *Nguyên nhân:* Phông chữ bạn đang dùng (Text Style) không hỗ trợ bảng mã gõ tiếng Việt tương ứng (ví dụ dùng Unikey mã Unicode nhưng Style lại dùng font VNI hoặc TCVN3).
  - *Cách sửa:* Gõ lệnh `STYLE` (phím tắt `ST`), chuyển font của Style về các font Unicode phổ biến như `Arial`, `Times New Roman` hoặc `Tahoma`.
- **Triệu chứng:** Gõ chữ xong không nhìn thấy chữ đâu trên màn hình.
  - *Nguyên nhân:* Chiều cao chữ (Text Height) đang để quá nhỏ so với tỷ lệ bản vẽ (ví dụ bản vẽ dài 100 mét nhưng chữ chỉ cao 2.5 milimet).
  - *Cách sửa:* Chọn chữ, mở bảng Properties ([Ctrl + 1]) và tăng giá trị *Height* lên phù hợp với khung nhìn bản vẽ.

## Bài tập thực hành

- [ ] Gõ lệnh `TEXT` và bấm điểm đặt chữ tại toạ độ `50,50`. <!-- expect: TEXT -->
- [ ] Nhập chiều cao chữ là `5.0`, góc xoay là `0`.
- [ ] Gõ dòng chữ `Chi tiet truc %%c40` rồi nhấn [Enter] hai lần để kết thúc. Quan sát ký hiệu `Ø` xuất hiện.
- [ ] Gõ lệnh `MTEXT`, kéo một khung hình chữ nhật trên vùng vẽ. <!-- expect: MTEXT -->
- [ ] Gõ đoạn văn bản yêu cầu kỹ thuật gồm 2 dòng rồi đóng Text Editor.
- [ ] Nhấp đúp vào khối chữ MTEXT để mở lại trình soạn thảo và bôi đen đổi màu sắc chữ.

## Nguồn tham khảo

```links
- title: Lệnh MTEXT và trình soạn thảo Multiline Text (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=MTEXT+Command
  kind: official
  lang: en
  note: Hướng dẫn chi tiết định dạng văn bản, căn lề, chia cột và chèn ký hiệu Symbol
- title: Danh sách ký hiệu đặc biệt %% trong AutoCAD (Autodesk Support)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Control+Codes+and+Special+Characters
  kind: official
  lang: en
  note: Bảng tra cứu các mã %%c, %%d, %%p, %%u trong văn bản AutoCAD
```
