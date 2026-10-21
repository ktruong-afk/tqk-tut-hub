---
id: ac-03-01
title: Xoá và phục hồi đối tượng với ERASE, OOPS và UNDO
category: Chỉnh sửa
tags: [erase, oops, undo, redo, xoa, khoi-phuc]
level: beginner
minutes: 15
needs: [ac-02-11]
appVersions: ['2024', '2025']
edition: all
---
# Xoá và phục hồi đối tượng với ERASE, OOPS và UNDO

> **Mục tiêu:**
> - Sử dụng lệnh ERASE và phím Delete để xoá bỏ đối tượng nhanh chóng và triệt để.
> - Phân biệt cơ chế khôi phục đối tượng của lệnh OOPS so với lệnh UNDO.
> - Quản lý lịch sử thao tác với lệnh UNDO và REDO trên thanh truy cập nhanh.

## Lệnh này làm gì và khi nào dùng

Trong quá trình chỉnh sửa bản vẽ, việc loại bỏ các nét thừa hoặc sửa sai là thao tác diễn ra liên tục. AutoCAD cung cấp bộ 4 công cụ hỗ trợ xoá và phục hồi:
- `ERASE` (phím tắt `E`): Xoá các đối tượng được chọn khỏi bản vẽ.
- `UNDO` (phím tắt `U` hoặc tổ hợp [Ctrl + Z]): [[Hoàn tác]] thao tác lệnh vừa thực hiện trước đó, đưa bản vẽ quay ngược về trạng thái cũ.
- `REDO` (tổ hợp [Ctrl + Y]): Phục hồi lại thao tác vừa bị Undo.
- `OOPS`: Lệnh cứu nguy đặc biệt! Khôi phục lại toàn bộ đối tượng vừa bị xoá bởi lệnh `ERASE` gần nhất mà **không làm mất** các nét vẽ bạn vừa vẽ thêm sau đó.

Hiểu rõ sự khác biệt giữa `OOPS` và `UNDO` sẽ giúp bạn tiết kiệm hàng giờ vẽ lại khi lỡ tay xoá nhầm đối tượng quan trọng.

## Cách dùng từng bước

1. **Xoá đối tượng bằng ERASE:**
   - Cách 1: Nhấp chọn các đối tượng cần xoá rồi nhấn phím [Delete] trên bàn phím.
   - Cách 2: Gõ `ERASE` hoặc phím tắt `E` rồi nhấn [Enter], quét chọn các đối tượng rồi nhấn [Enter] để xác nhận xoá.
2. **Xoá toàn bộ nét vừa vẽ (Select Last):**
   - Gõ `E` rồi nhấn [Enter].
   - Gõ chữ `L` (Last) rồi nhấn [Enter]. Đối tượng vừa tạo gần nhất sẽ tự động được chọn để xoá.
3. **Hoàn tác bằng UNDO:**
   - Gõ `U` hoặc nhấn [Ctrl + Z] trên bàn phím để lùi lại 1 bước lệnh.
   - Bấm vào mũi tên xổ xuống cạnh nút Undo trên Quick Access Toolbar để lùi lại hàng loạt 10 - 20 bước cùng lúc.
4. **Cứu lại đối tượng đã xoá bằng OOPS:**
   - Giả sử bạn vừa xoá một đường tròn bằng `ERASE`.
   - Sau đó bạn tiếp tục vẽ thêm 5 đoạn thẳng `LINE` mới.
   - Nếu bạn dùng `UNDO`, 5 đoạn thẳng mới vẽ sẽ bị biến mất.
   - Thay vào đó, hãy gõ `OOPS` rồi nhấn [Enter]. Đường tròn vừa bị xoá sẽ lập tức xuất hiện trở lại mà 5 đoạn thẳng mới vẫn được giữ nguyên vẹn!

## Tuỳ chọn và mẹo

> [!TIP]
> Lệnh `OOPS` có thể khôi phục lại các đối tượng bị biến mất sau khi bạn thực hiện lệnh tạo khối `BLOCK` (khi vô tình chọn tuỳ chọn Delete source objects).

> [!TIP]
> Phím [Delete] trên bàn phím tương đương với lệnh ERASE khi bạn đã chọn sẵn đối tượng (chế độ Noun/Verb selection).

## Tự kiểm tra

```quiz
id: q-ac-03-01-1
type: single
question: Khi bạn vừa dùng lệnh ERASE xoá đối tượng, sau đó vẽ thêm nhiều hình mới, lệnh nào giúp lấy lại đối tượng đã xoá mà không làm mất các hình mới vẽ?
options:
  - text: OOPS
    correct: true
    why: OOPS chỉ phục hồi đối tượng bị xoá bởi lệnh ERASE gần nhất mà không lùi thời gian như UNDO
  - text: UNDO
    why: UNDO sẽ xoá sạch các hình bạn vừa vẽ thêm để lùi về thời điểm trước đó
  - text: REDO
    why: REDO chỉ có tác dụng ngay sau khi bạn vừa bấm UNDO
  - text: REGEN
    why: REGEN chỉ làm mới màn hình đồ hoạ
explain: "Lệnh OOPS là lệnh chuyên biệt để khôi phục các thực thể bị xoá bởi lệnh ERASE cuối cùng mà không làm ảnh hưởng đến các thao tác vẽ diễn ra sau đó."
tags: [erase, oops, undo]
```

```quiz
id: q-ac-03-01-2
type: single
question: Phím tắt tiêu chuẩn nào dùng để kích hoạt lệnh xoá ERASE trong AutoCAD?
options:
  - text: E
    correct: true
    why: E là chữ cái tắt chính thức của lệnh ERASE
  - text: X
    why: X là phím tắt của lệnh phá vỡ EXPLODE
  - text: D
    why: D là phím tắt của lệnh DIMSTYLE
  - text: C
    why: C là phím tắt của lệnh CIRCLE
explain: "Phím tắt E đại diện cho lệnh ERASE. Bạn có thể gõ E rồi nhấn Spacebar để xoá nhanh các đối tượng được chọn."
tags: [erase, phim-tat]
```

```quiz
id: q-ac-03-01-3
type: truefalse
question: Lệnh REDO có thể thực hiện vào bất kỳ lúc nào để khôi phục lại các lệnh bạn đã làm vào ngày hôm qua.
answer: false
explain: "Lệnh REDO chỉ có hiệu lực ngay lập tức sau khi bạn vừa thực hiện lệnh UNDO. Nếu bạn đã thực hiện bất kỳ lệnh vẽ nào khác, chuỗi REDO sẽ bị ngắt."
tags: [redo, undo]
```

## Lỗi thường gặp

- **Triệu chứng:** Chọn đối tượng rồi nhấn phím [Delete] nhưng đối tượng không chịu biến mất.
  - *Nguyên nhân:* Biến hệ thống `PICKFIRST` đang bị tắt về giá trị 0 (vô hiệu hoá chế độ chọn đối tượng trước khi gọi lệnh).
  - *Cách sửa:* Gõ lệnh `PICKFIRST` vào dòng lệnh và đặt giá trị lại thành `1`.
- **Triệu chứng:** Lỡ tay bấm UNDO quá nhiều lần làm mất bản vẽ.
  - *Nguyên nhân:* Bấm nhầm hoặc nhấn giữ phím [Ctrl + Z] liên tục.
  - *Cách sửa:* Nhấn ngay tổ hợp phím [Ctrl + Y] (lệnh `REDO`) để lấy lại các bước vừa hoàn tác.

## Bài tập thực hành

- [ ] Gõ `LINE` vẽ một hình tam giác gồm 3 cạnh. <!-- expect: LINE -->
- [ ] Nhấp chọn 1 cạnh và gõ `ERASE` để xoá cạnh đó. <!-- expect: ERASE -->
- [ ] Gõ `OOPS` và nhấn [Enter] để phục hồi lại cạnh vừa xoá. <!-- expect: OOPS -->
- [ ] Gõ `UNDO` (hoặc nhấn [Ctrl + Z]) để huỷ bỏ lệnh vừa làm. <!-- expect: UNDO -->
- [ ] Gõ `REDO` (hoặc [Ctrl + Y]) để phục hồi lại trạng thái trước khi Undo. <!-- expect: REDO -->

## Nguồn tham khảo

```links
- title: Lệnh ERASE và dọn dẹp đối tượng (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=ERASE+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về các chế độ chọn lọc và xoá đối tượng
- title: Lệnh OOPS và cơ chế phục hồi đối tượng (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=OOPS+Command
  kind: official
  lang: en
  note: Tài liệu giải thích sự khác biệt giữa OOPS và UNDO
```
