---
id: ac-02-06
title: Vẽ đường đa tuyến liên tục với lệnh PLINE
category: Vẽ 2D
tags: [pline, polyline, ve-2d, be-day, width, lien-khoi]
level: beginner
minutes: 15
needs: [ac-02-01]
appVersions: ['2024', '2025']
edition: all
---
# Vẽ đường đa tuyến liên tục với lệnh PLINE

> **Mục tiêu:**
> - Sử dụng lệnh PLINE để tạo đường đa tuyến liên tục gồm nhiều đoạn thẳng và cung tròn kết hợp.
> - Thiết lập bề dày nét vẽ (Width / Halfwidth) cho từng phân đoạn hoặc tạo mũi tên chỉ dẫn.
> - Phân biệt ưu thế vượt trội của Polyline so với Line trong việc tính diện tích và xuất mô hình 3D.

## Lệnh này làm gì và khi nào dùng

Lệnh `PLINE` (phím tắt `PL`) dùng để tạo đối tượng [[Đường đa tuyến]] (Polyline). Đây là một trong những đối tượng quyền lực và linh hoạt nhất trong AutoCAD.

Khác với lệnh LINE tạo ra các phân đoạn rời rạc, lệnh PLINE gom toàn bộ các đoạn thẳng và cung cong nối tiếp thành **một đối tượng duy nhất, liền khối**. Bạn có thể gán bề dày thực tế cho nét vẽ, chuyển đổi linh hoạt giữa vẽ đoạn thẳng và [[Cung tròn]] ngay trong cùng một lệnh, và dễ dàng tra cứu chu vi, diện tích chỉ bằng một cú nhấp chuột.

Trong thực tế, Polyline là đối tượng bắt buộc khi vẽ đường bao công trình, mặt bằng tường kiến trúc, đường đồng mức địa hình và tiết diện kín để kéo khối 3D (Extrude).

```hotspots
image: media/ac-02-06-pline-vs-line.svg
alt: So sánh trực quan giữa các đoạn rời rạc của lệnh LINE và đường liền khối có bề dày của lệnh PLINE
layout: central
points:
  - id: compare-line
    x: 25
    y: 35
    title: Lệnh LINE (Rời rạc)
    text: Mỗi phân đoạn là một thực thể riêng. Không có thuộc tính bề rộng Width trên từng phân đoạn.
  - id: compare-pline
    x: 75
    y: 35
    title: Lệnh PLINE (Đa tuyến liền khối)
    text: Toàn bộ đường đi là 1 đối tượng duy nhất. Có thể chỉnh bề rộng nét vẽ (Width) và lồng ghép cung cong.
    quiz: q-ac-02-06-1
```

## Cách dùng từng bước

1. **Gọi lệnh:** Gõ `PLINE` hoặc phím tắt `PL` rồi nhấn [Enter].
2. **Chọn điểm bắt đầu:** Bấm chuột tại điểm xuất phát hoặc gõ toạ độ (ví dụ `0,0`).
3. **Vẽ đoạn thẳng:** Rê chuột theo hướng mong muốn, nhập chiều dài (ví dụ `100`) rồi [Enter].
4. **Chuyển sang vẽ cung tròn (Arc):**
   - Đang trong lệnh, gõ chữ `A` (Arc) rồi [Enter].
   - Rê chuột để uốn cong và nhập đường kính hoặc bấm điểm mút cung tròn.
5. **Chuyển ngược lại vẽ đoạn thẳng (Line):**
   - Gõ chữ `L` (Line) rồi [Enter] để tiếp tục vẽ đường thẳng tiếp tuyến với cung vừa rồi.
6. **Đặt bề dày nét vẽ (Width):**
   - Gõ chữ `W` (Width) rồi [Enter].
   - Nhập bề dày tại điểm bắt đầu phân đoạn (Starting width, ví dụ `5`).
   - Nhập bề dày tại điểm kết thúc phân đoạn (Ending width, ví dụ `5`).
7. **Khép kín hoặc hoàn tất:**
   - Gõ `C` (Close) để nối về điểm đầu tiên và tạo hình kín, hoặc nhấn [Enter] để kết thúc.

## Tuỳ chọn và mẹo

> [!TIP]
> Muốn vẽ mũi tên chỉ dẫn nhanh không cần chèn block: Dùng lệnh `PLINE`, bấm điểm đuôi mũi tên, gõ `W` đặt *Starting width = 10*, *Ending width = 0* rồi kéo dài đoạn mũi tên ra một khoảng ngắn.

> [!TIP]
> Chọn một Polyline khép kín và mở bảng thuộc tính Properties ([Ctrl + 1]), bạn sẽ thấy ngay diện tích (Area) và chu vi (Length) được tính toán chính xác tuyệt đối mà không cần đo đạc thủ công.

## Tự kiểm tra

```quiz
id: q-ac-02-06-1
type: single
question: Khi đang vẽ đường bằng lệnh PLINE, tuỳ chọn nào cho phép chuyển đổi sang chế độ vẽ cung tròn tiếp tuyến?
options:
  - text: Arc (gõ chữ A)
    correct: true
    why: Tuỳ chọn Arc chuyển ngay sang vẽ cung tròn trong chuỗi Polyline
  - text: Circle (gõ chữ C)
    why: Chữ C trong lệnh PLINE là tuỳ chọn Close để khép kín hình
  - text: Spline (gõ chữ S)
    why: Chữ S không phải tuỳ chọn chuyển cung cong của PLINE
  - text: Halfwidth (gõ chữ H)
    why: Halfwidth dùng để đặt nửa bề rộng nét
explain: "Khi gõ chữ A (Arc) trong lệnh PLINE, AutoCAD sẽ chuyển từ chế độ vẽ đoạn thẳng sang vẽ cung tròn tiếp xúc mượt mà với phân đoạn trước."
tags: [pline, options, arc]
```

```quiz
id: q-ac-02-06-2
type: single
question: Để vẽ một mũi tên có đuôi to bản 8mm và vuốt nhọn dần về đỉnh bằng 0mm, bạn cài đặt thông số Width như thế nào?
options:
  - text: Starting width = 8, Ending width = 0
    correct: true
    why: Điểm bắt đầu dày 8mm và vuốt nhọn dần về 0mm tại điểm kết thúc tạo hình mũi tên
  - text: Starting width = 0, Ending width = 8
    why: Cài đặt này sẽ tạo mũi tên quay ngược hướng lại
  - text: Starting width = 8, Ending width = 8
    why: Bề dày hai đầu bằng nhau tạo thành đoạn thẳng phẳng
  - text: Halfwidth = 8
    why: Halfwidth là nửa bề rộng nét
explain: "Tuỳ chọn Width (gõ W) trong PLINE cho phép chỉ định bề dày khác nhau tại điểm đầu và điểm cuối của một phân đoạn, giúp tạo mũi tên hình nón dễ dàng."
tags: [pline, width, mui-ten]
```

```quiz
id: q-ac-02-06-3
type: truefalse
question: Khi bạn chọn một hình khép kín vẽ bằng lệnh PLINE, bạn có thể tra cứu ngay lập tức diện tích (Area) trong bảng thuộc tính Properties.
answer: true
explain: "Do Polyline là một thực thể liền khối, AutoCAD tự động tính toán và hiển thị trường dữ liệu Area (diện tích) và Length (chu vi) trong bảng Properties (Ctrl + 1)."
tags: [pline, properties, dien-tich]
```

```quiz
id: q-ac-02-06-4
type: hotspot
question: Bấm vào vị trí minh hoạ đường đa tuyến PLINE liền khối trên hình.
use: hotspots
answer: compare-pline
explain: "Đường đa tuyến PLINE nằm ở nửa bên phải của sơ đồ, có bề dày nét và đường cong liền mạch."
tags: [pline, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Nét vẽ Polyline cứ bị dày cộm như một dải băng đen sau khi lỡ chỉnh Width.
  - *Nguyên nhân:* Giá trị Width vừa nhập trước đó được AutoCAD ghi nhớ làm mặc định cho mọi lệnh PLINE tiếp theo.
  - *Cách sửa:* Gõ lại lệnh `PLINE`, bấm điểm xuất phát, gõ chữ `W` và đặt lại cả *Starting width = 0* và *Ending width = 0*.
- **Triệu chứng:** Không thể bo tròn góc (Fillet) hai đoạn thẳng vì chúng thuộc hai đối tượng rời rạc.
  - *Nguyên nhân:* Đoạn thẳng được vẽ bằng lệnh LINE thông thường thay vì Polyline.
  - *Cách sửa:* Gõ lệnh `JOIN` (gõ tắt `J`), quét chọn toàn bộ các đoạn Line để hợp nhất chúng thành một đường Polyline duy nhất.

## Bài tập thực hành

- [ ] Gõ `PLINE` và chọn điểm bắt đầu tại toạ độ `0,0`. <!-- expect: PLINE -->
- [ ] Bật [F8], vẽ đoạn thẳng sang phải dài `100` rồi [Enter].
- [ ] Gõ chữ `A` (Arc), uốn cung tròn lên trên với đường kính `60` rồi [Enter].
- [ ] Gõ chữ `L` (Line), vẽ tiếp đoạn thẳng sang trái dài `100` rồi [Enter].
- [ ] Gõ chữ `C` (Close) để khép kín hình thành một chi tiết cơ khí dạng chốt. <!-- expect: PLINE -->
- [ ] Nhấp chọn hình và mở bảng Properties ([Ctrl + 1]) để quan sát thông số Area.

## Nguồn tham khảo

```links
- title: Lệnh PLINE và cách tạo đường đa tuyến 2D (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=PLINE+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn Arc, Halfwidth, Length, Undo, Width của lệnh PLINE
- title: Chỉnh sửa và kết hợp Polyline bằng lệnh PEDIT (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=PEDIT+Command
  kind: official
  lang: en
  note: Hướng dẫn nối gộp (Join), uốn mịn (Fit/Spline) và sửa bề dày đường đa tuyến
```
