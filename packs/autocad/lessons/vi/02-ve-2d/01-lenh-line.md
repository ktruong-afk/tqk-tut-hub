---
id: ac-02-01
title: Vẽ đoạn thẳng với lệnh LINE
category: Vẽ 2D
tags: [line, ve-2d, doan-thang, co-ban]
level: beginner
minutes: 15
needs: [ac-01-07]
appVersions: ['2024', '2025']
edition: all
---
# Vẽ đoạn thẳng với lệnh LINE

> **Mục tiêu:**
> - Sử dụng lệnh LINE để vẽ chuỗi các đoạn thẳng liên tiếp với toạ độ và kích thước chính xác.
> - Áp dụng các tuỳ chọn Undo và Close trực tiếp trên dòng lệnh khi đang thao tác.
> - Phân biệt đặc tính độc lập của đối tượng đoạn thẳng (Line) với đường đa tuyến (Polyline).

## Lệnh này làm gì và khi nào dùng

Lệnh `LINE` (phím tắt `L`) là lệnh vẽ hình học cơ bản và được sử dụng với tần suất cao nhất trong AutoCAD. Mỗi lần thực hiện, lệnh LINE tạo ra một hoặc nhiều [[Đoạn thẳng]] nối tiếp nhau. 

Điểm đặc trưng của lệnh LINE là mỗi phân đoạn giữa hai điểm bấm chuột là một thực thể hình học hoàn toàn độc lập. Bạn có thể chọn, xoá, di chuyển hoặc đổi thuộc tính của từng đoạn đơn lẻ mà không làm ảnh hưởng đến các đoạn xung quanh. Lệnh LINE thích hợp nhất cho việc phác thảo nhanh đường bao, vẽ các đường gióng chuẩn hoặc các chi tiết cơ khí đơn giản.

```hotspots
image: media/ac-02-01-line-status.svg
alt: Minh hoạ quá trình vẽ đoạn thẳng với lệnh LINE, hiển thị con trỏ chữ thập và dòng nhắc toạ độ
layout: central
points:
  - id: start-pt
    x: 10
    y: 60
    title: Điểm xuất phát (First point)
    text: Điểm bắt đầu của chuỗi đoạn thẳng, có thể bấm chuột tự do hoặc gõ toạ độ chính xác (ví dụ 0,0).
  - id: next-pt
    x: 42
    y: 60
    title: Điểm kế tiếp (Next point)
    text: Điểm kết thúc phân đoạn thứ nhất và là điểm khởi đầu cho phân đoạn tiếp theo.
    quiz: q-ac-02-01-1
  - id: cmd-prompt
    x: 50
    y: 84
    title: Dòng nhắc lệnh LINE
    text: Hiển thị tuỳ chọn Undo (quay lại điểm trước) và Close (khép kín về điểm ban đầu).
    quiz: q-ac-02-01-2
```

## Cách dùng từng bước

1. **Gọi lệnh:** Gõ `LINE` hoặc phím tắt `L` rồi nhấn [Spacebar] hoặc [Enter].
2. **Xác định điểm đầu tiên:** Dòng lệnh hiển thị `Specify first point:`. Nhấp chuột trái vào vùng vẽ hoặc gõ toạ độ (ví dụ `50,50`) rồi nhấn [Enter].
3. **Xác định điểm kế tiếp:** Dòng lệnh chuyển sang `Specify next point or [Undo]:`. Di chuyển chuột theo hướng mong muốn, gõ độ dài (ví dụ `120`) rồi nhấn [Enter].
4. **Vẽ tiếp các phân đoạn khác:** Tiếp tục nhập chiều dài hoặc nhấp điểm mút mới.
5. **Khép kín hoặc quay lui:**
   - Muốn huỷ phân đoạn vừa vẽ sai: Gõ chữ `U` (Undo) rồi nhấn [Enter].
   - Muốn tự động vẽ đoạn thẳng nối về điểm đầu tiên và thoát lệnh: Gõ chữ `C` (Close) rồi nhấn [Enter].
6. **Kết thúc lệnh:** Nhấn phím [Spacebar], [Enter] hoặc [Esc].

## Tuỳ chọn và mẹo

> [!TIP]
> Ngay sau khi vừa kết thúc một lệnh LINE, nếu bạn gõ lại lệnh `LINE` và nhấn [Enter] ngay tại dòng nhắc `Specify first point:`, AutoCAD sẽ tự động bắt tiếp điểm xuất phát vào điểm mút cuối cùng bạn vừa vẽ.

> [!TIP]
> Kết hợp phím [F8] (chế độ Ortho) khi dùng lệnh LINE để vẽ các hệ khung xương ngang dọc vuông góc tuyệt đối mà không sợ lệch góc.

## Tự kiểm tra

```quiz
id: q-ac-02-01-1
type: single
question: Khi đang vẽ chuỗi nhiều đoạn thẳng bằng lệnh LINE, tuỳ chọn "Close" (gõ chữ C) có tác dụng gì?
options:
  - text: Nối một đoạn thẳng từ điểm hiện tại về điểm đầu tiên và kết thúc lệnh
    correct: true
    why: Tuỳ chọn Close tự động nối khép kín chuỗi đường thẳng về điểm xuất phát ban đầu
  - text: Đóng cửa sổ bản vẽ AutoCAD hiện tại
    why: Đóng bản vẽ dùng lệnh CLOSE
  - text: Huỷ bỏ toàn bộ các đoạn thẳng vừa vẽ
    why: Huỷ bỏ toàn bộ dùng phím Esc
  - text: Chuyển các đoạn thẳng thành hình tròn
    why: Lệnh LINE không thể biến thành hình tròn
explain: "Khi gõ chữ C (Close) trong lệnh LINE, AutoCAD sẽ tự động tạo một đoạn thẳng nối từ vị trí con trỏ hiện tại về điểm đầu tiên của chuỗi lệnh và tự động thoát lệnh."
tags: [line, options, close]
```

```quiz
id: q-ac-02-01-2
type: single
question: Điểm khác biệt cơ bản giữa đoạn thẳng tạo bởi lệnh LINE và đường đa tuyến tạo bởi lệnh PLINE là gì?
options:
  - text: LINE tạo các đoạn thẳng rời rạc độc lập, PLINE tạo một đối tượng liền khối duy nhất
    correct: true
    why: Mỗi đoạn LINE là một thực thể riêng biệt, trong khi PLINE là một khối liền mạch
  - text: LINE chỉ vẽ được đường màu trắng, PLINE vẽ được màu đỏ
    why: Cả hai đều thay đổi được màu sắc tuỳ ý qua layer và properties
  - text: LINE không thể xoá được sau khi vẽ
    why: LINE xoá bình thường bằng lệnh ERASE
  - text: PLINE chỉ vẽ được đường cong
    why: PLINE vẽ được cả đoạn thẳng và cung tròn
explain: "Đối tượng LINE gồm nhiều đoạn rời nhau có thể xoá hoặc chọn riêng lẻ; trong khi PLINE liên kết toàn bộ chuỗi nét thành một đối tượng duy nhất."
tags: [line, pline, so-sanh]
```

```quiz
id: q-ac-02-01-3
type: truefalse
question: Nhấn phím [Spacebar] (phím cách) trong AutoCAD có tác dụng xác nhận lệnh tương đương phím [Enter].
answer: true
explain: "Trong AutoCAD, phím Spacebar và phím Enter có chức năng giống hệt nhau trong hầu hết các tình huống gọi lệnh và xác nhận nhập toạ độ."
tags: [line, spacebar]
```

```quiz
id: q-ac-02-01-4
type: hotspot
question: Bấm vào dòng nhắc lệnh LINE trên thanh trạng thái phía dưới hình minh hoạ.
use: hotspots
answer: cmd-prompt
explain: "Dòng nhắc lệnh LINE nằm ở thanh đáy, hiển thị tuỳ chọn Specify next point or [Undo]."
tags: [line, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Vẽ xong một hình chữ nhật bằng lệnh LINE, bấm chọn một cạnh thì chỉ sáng 1 đoạn chứ không chọn được cả hình.
  - *Nguyên nhân:* Đây là đặc tính bình thường của lệnh LINE (tạo các đoạn rời).
  - *Cách sửa:* Nếu muốn đối tượng liền mạch thành một khối, hãy dùng lệnh `PLINE` để vẽ hoặc dùng lệnh `JOIN` để gộp các đoạn LINE lại.
- **Triệu chứng:** Đoạn thẳng nhìn có vẻ ngang nhưng khi phóng to lại thấy bị nghiêng chênh 0.1 độ.
  - *Nguyên nhân:* Không bật chế độ Ortho ([F8]) hoặc chưa nhập toạ độ chính xác mà bấm chuột tự do.
  - *Cách sửa:* Luôn bật phím [F8] hoặc bật Polar Tracking ([F10]) khi vẽ các cạnh cần song song trục toạ độ.

## Bài tập thực hành

- [ ] Gõ `LINE` và chọn điểm đầu tiên tại toạ độ `0,0`. <!-- expect: LINE -->
- [ ] Bật [F8] (Ortho), rê chuột sang phải và gõ khoảng cách `120` rồi nhấn [Enter]. <!-- expect: LINE -->
- [ ] Rê chuột thẳng đứng lên trên, gõ `80` rồi nhấn [Enter]. <!-- expect: LINE -->
- [ ] Rê chuột sang trái, gõ `120` rồi nhấn [Enter]. <!-- expect: LINE -->
- [ ] Gõ chữ `C` (Close) và nhấn [Enter] để khép kín hình chữ nhật kích thước 120×80mm. <!-- expect: LINE -->
- [ ] Nhấp chuột chọn thử từng cạnh để xác nhận 4 cạnh là 4 đối tượng độc lập.

## Nguồn tham khảo

```links
- title: Lệnh LINE và tuỳ chọn dòng lệnh (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=LINE+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về cú pháp và các tuỳ chọn Close, Undo của lệnh LINE
- title: Khái niệm phân đoạn thẳng trong CAD (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Lines
  kind: official
  lang: en
  note: Giải thích cấu trúc thực thể hình học đường thẳng trong cơ sở dữ liệu AutoCAD
```
