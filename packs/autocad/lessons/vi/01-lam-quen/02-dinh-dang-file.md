---
id: ac-01-02
title: Mở, lưu và các định dạng file trong AutoCAD
category: Làm quen
tags: [dwg, dxf, dwt, autosave, bak]
level: beginner
minutes: 15
needs: [ac-01-01]
appVersions: ['2024', '2025']
edition: all
---
# Mở, lưu và các định dạng file trong AutoCAD

> **Mục tiêu:**
> - Phân biệt mục đích sử dụng của các định dạng file DWG, DXF, DWT và file dự phòng .bak.
> - Thiết lập thời gian tự động lưu bản vẽ để phòng ngừa sự cố mất điện hoặc treo máy.
> - Sử dụng thành thạo các thao tác mở, lưu nhanh và lưu sang phiên bản CAD đời cũ hơn.

## Lệnh này làm gì và khi nào dùng

Quản lý tệp là kỹ năng sống còn trong thiết kế kỹ thuật. Khi làm việc với AutoCAD, bạn sẽ tiếp xúc với nhiều định dạng tệp khác nhau:
- [[Định dạng DWG]] (Drawing): Tệp nhị phân tiêu chuẩn lưu toàn bộ thực thể và thuộc tính bản vẽ.
- [[Định dạng DXF]] (Drawing Exchange Format): Định dạng mở chia sẻ dữ liệu hình học cho máy cắt CNC, laser hoặc phần mềm CAD khác.
- [[Mẫu bản vẽ]] (DWT): Bản vẽ mẫu chứa sẵn khung tên, layer, kiểu chữ để tạo file mới.
- [[Tự động lưu]] (.sv$) và [[File sao lưu]] (.bak): Cơ chế bảo vệ bản vẽ an toàn trước các sự cố bất ngờ.

Hiểu rõ các định dạng giúp bạn cộng tác thông suốt với đối tác dùng các phiên bản AutoCAD khác nhau và phục hồi bản vẽ kịp thời khi gặp sự cố.

## Cách dùng từng bước

1. **Lưu nhanh bản vẽ đang mở:** Gõ lệnh `QSAVE` hoặc nhấn tổ hợp phím [Ctrl + S]. Nếu là file mới chưa đặt tên, hộp thoại Save Drawing As sẽ hiện ra.
2. **Lưu sang file mới hoặc phiên bản cũ:** Gõ `SAVEAS` (hoặc [Ctrl + Shift + S]). Trong ô **Files of type**, chọn phiên bản như *AutoCAD 2018/LT 2018 Drawing (*.dwg)* để đối tác dùng máy đời thấp hơn vẫn mở được.
3. **Mở bản vẽ có sẵn:** Gõ `OPEN` hoặc nhấn [Ctrl + O], chọn đường dẫn tới file `.dwg` rồi bấm Open.
4. **Tạo bản vẽ mới từ template:** Gõ `NEW` hoặc [Ctrl + N], chọn file mẫu `acadiso.dwt` (chuẩn hệ mét) để bắt đầu.
5. **Cấu hình thời gian tự lưu:** Gõ `OPTIONS` (gõ tắt `OP`), chuyển đến thẻ **Open and Save**, tại mục *File Safety Precautions* tích chọn *Automatic save* và chỉnh số phút (khuyến nghị 5 - 10 phút).

## Tuỳ chọn và mẹo

> [!TIP]
> Khi gặp sự cố phần mềm đột ngột tắt mà chưa kịp lưu, bạn có thể tìm file có đuôi `.bak` nằm cùng thư mục với file gốc, đổi đuôi thành `.dwg` để cứu lại phiên bản vừa lưu trước đó.

> [!TIP]
> Luôn lưu bản vẽ ở định dạng thấp hơn phiên bản bạn đang dùng một bậc khi gửi cho đối tác (ví dụ lưu về bản 2018 khi đang dùng 2024) để đảm bảo tính tương thích.

## Tự kiểm tra

```quiz
id: q-ac-01-02-1
type: single
question: Định dạng tệp nào là tệp mẫu (Template) chứa cài đặt sẵn layer, kiểu chữ trong AutoCAD?
options:
  - { text: .dwt, correct: true, why: .dwt viết tắt của Drawing Template, dùng làm mẫu khởi tạo bản vẽ }
  - { text: .dwg, why: .dwg là định dạng bản vẽ thông thường }
  - { text: .dxf, why: .dxf là định dạng trao đổi dữ liệu CAD }
  - { text: .bak, why: .bak là file sao lưu dự phòng }
explain: Tệp .dwt (Drawing Template) là tệp mẫu chứa sẵn các thiết lập chuẩn (layer, text style, dimension style, khung tên) để tạo nhanh bản vẽ mới.
tags: [dinh-dang, dwt]
```

```quiz
id: q-ac-01-02-2
type: truefalse
question: Muốn phục hồi dữ liệu từ file sao lưu có đuôi .bak, bạn chỉ cần đổi phần mở rộng thành .dwg rồi mở lại trong AutoCAD.
answer: true
explain: File .bak chính là bản sao nguyên vẹn của file .dwg ở lần lưu liền trước đó, do đó đổi đuôi thành .dwg sẽ mở lại bình thường.
tags: [sao-luu, bak]
```

```quiz
id: q-ac-01-02-3
type: single
question: Khi gửi bản vẽ cho đối tác sử dụng AutoCAD phiên bản cũ hơn phiên bản của bạn, bạn nên dùng lệnh nào?
options:
  - { text: SAVEAS và chọn phiên bản đời cũ phù hợp, correct: true, why: SAVEAS cho phép chọn lưu ngược về các đời CAD 2018, 2013, 2010... }
  - { text: QSAVE, why: QSAVE chỉ lưu đè theo phiên bản hiện hành của phần mềm }
  - { text: OPEN, why: OPEN là lệnh mở file chứ không dùng để lưu }
  - { text: NEW, why: NEW dùng để tạo bản vẽ mới }
explain: Lệnh SAVEAS mở hộp thoại lưu tệp, cho phép bạn chọn phiên bản DWG đời cũ hơn tại danh sách "Files of type" để đảm bảo khả năng tương thích ngược.
tags: [luu-file, saveas]
```

## Lỗi thường gặp

- **Triệu chứng:** Đối tác báo lỗi *"Drawing file is not valid"* khi mở file do bạn gửi.
  - *Nguyên nhân:* Đối tác dùng phiên bản AutoCAD đời thấp hơn phiên bản DWG bạn đã lưu (ví dụ máy bạn 2024 nhưng máy đối tác 2016).
  - *Cách sửa:* Dùng lệnh `SAVEAS`, chọn định dạng *AutoCAD 2013 Drawing (*.dwg)* hoặc *AutoCAD 2018* rồi gửi lại.
- **Triệu chứng:** Không tìm thấy file tự lưu `.sv$` sau khi máy tính sập nguồn.
  - *Nguyên nhân:* File `.sv$` được lưu trong thư mục tạm của hệ thống (`%TEMP%`) và bị ẩn phần mở rộng.
  - *Cách sửa:* Gõ lệnh `DRAWINGRECOVERY` trong AutoCAD để mở bảng Recovery Manager tự động liệt kê các file sao lưu gần nhất.

## Bài tập thực hành

- [ ] Gõ `NEW` để mở hộp thoại tạo bản vẽ mới và chọn mẫu `acadiso.dwt`. <!-- expect: NEW -->
- [ ] Gõ `QSAVE` để lưu bản vẽ lần đầu tiên với tên `Thuc-Hanh-01.dwg`. <!-- expect: QSAVE -->
- [ ] Gõ `SAVEAS` và lưu thêm một bản sao có tên `Thuc-Hanh-01-2018.dwg` với định dạng AutoCAD 2018 Drawing. <!-- expect: SAVEAS -->
- [ ] Mở trình duyệt tệp Windows Explorer kiểm tra thư mục lưu và quan sát file `.bak` được tạo ra.

## Nguồn tham khảo

```links
- title: Giới thiệu các định dạng tệp AutoCAD (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Drawing+File+Formats
  kind: official
  lang: en
  note: Tài liệu chính thức về cấu trúc file DWG, DXF và khả năng tương thích ngược giữa các phiên bản
- title: Phục hồi bản vẽ từ file sao lưu (Autodesk Support)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Recover+Drawings
  kind: official
  lang: en
  note: Hướng dẫn khôi phục tệp bị hỏng hoặc mất do sập nguồn
```
