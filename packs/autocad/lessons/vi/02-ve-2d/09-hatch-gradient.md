---
id: ac-02-09
title: Tô mặt cắt với HATCH và chuyển sắc với GRADIENT
category: Vẽ 2D
tags: [hatch, gradient, ve-2d, mat-cat, ansi31, hoa-van]
level: beginner
minutes: 20
needs: [ac-02-04]
appVersions: ['2024', '2025']
edition: all
---
# Tô mặt cắt với HATCH và chuyển sắc với GRADIENT

> **Mục tiêu:**
> - Sử dụng lệnh HATCH để tô mặt cắt vật liệu kỹ thuật (ANSI31, gạch, bê tông, kim loại).
> - Phân biệt phương pháp chọn điểm trong biên (Pick Points) và chọn đối tượng bao (Select Objects).
> - Điều chỉnh tỷ lệ hoa văn (Scale), góc nghiêng (Angle) và kiểm soát tính liên kết (Associative).

## Lệnh này làm gì và khi nào dùng

Trên bản vẽ kỹ thuật cơ khí và xây dựng, [[Mặt cắt]] (Hatch) là ngôn ngữ quy ước để thể hiện vật liệu bên trong khi một chi tiết bị cắt bổ ra (mặt cắt kim loại gang thép, bê tông cốt thép, tường gạch, mặt đất tự nhiên hoặc lớp cách nhiệt).

Lệnh `HATCH` (phím tắt `H`) tự động dò tìm đường biên kín và phủ kín hoa văn lặp lại theo tiêu chuẩn ISO/ANSI.

Lệnh `GRADIENT` (phím tắt `GD`) là một biến thể của Hatch, dùng để tô hiệu ứng chuyển sắc giữa một hoặc hai dải màu mượt mà, rất thích hợp khi vẽ phối cảnh 2D, mặt đứng kiến trúc hoặc mô phỏng bề mặt cong tròn bóng bẩy.

```hotspots
image: media/ac-02-09-hatch-pattern.svg
alt: Sơ đồ minh hoạ mặt cắt kim loại ANSI31 với phương pháp Pick Point và tô chuyển sắc Gradient
layout: central
points:
  - id: hatch-pick
    x: 22
    y: 35
    title: Mặt cắt ANSI31 (Pick Points)
    text: Bấm một điểm bất kỳ bên trong vùng kín. AutoCAD tự động nhận diện đường bao xung quanh và trừ đi các lỗ hổng (Island).
    quiz: q-ac-02-09-1
  - id: grad-fill
    x: 75
    y: 35
    title: Tô màu chuyển sắc (Gradient)
    text: Chuyển tiếp mượt mà giữa hai sắc thái màu trong vùng biên kín, tạo cảm giác bóng bẩy 3D trên bản vẽ 2D.
    quiz: q-ac-02-09-2
```

## Cách dùng từng bước

1. **Chuẩn bị đường bao kín:** Đảm bảo vùng cần tô là một đa giác hoặc đường cong khép kín 100% không có kẽ hở.
2. **Gọi lệnh HATCH:** Gõ `HATCH` hoặc phím tắt `H` rồi nhấn [Enter]. Thanh Ribbon theo ngữ cảnh *Hatch Creation* sẽ tự động kích hoạt.
3. **Chọn mẫu hoa văn (Pattern):**
   - Bấm vào bảng mẫu trên Ribbon, chọn mẫu mong muốn:
     - `ANSI31`: Các nét gạch chéo 45 độ quy ước cho kim loại cơ khí (thép, gang).
     - `SOLID`: Tô một mảng màu đơn sắc đặc hoàn toàn.
     - `AR-CONC`: Hoa văn đá sỏi bê tông xây dựng.
4. **Xác định vùng tô:**
   - **Pick Points (Khuyến nghị):** Nhấp chuột vào một khoảng trống bên trong vùng kín. AutoCAD sẽ tự phân tích biên bao và tự động trừ các lỗ tròn nằm bên trong.
   - **Select Objects:** Nhấp trực tiếp vào đường bao Polyline kín.
5. **Điều chỉnh tỷ lệ và góc nghiêng:**
   - *Hatch Pattern Scale:* Nếu nét gạch quá mau (đặc như một khối đen) hoặc quá thưa không thấy nét, hãy tăng hoặc giảm ô tỷ lệ Scale (ví dụ gõ `10` hoặc `0.1`).
   - *Angle:* Đổi góc nghiêng hoa văn nếu cần (mặc định 0 độ).
6. **Xác nhận hoàn tất:** Nhấn nút **Close Hatch Creation** trên Ribbon hoặc nhấn phím [Enter].

## Tuỳ chọn và mẹo

> [!TIP]
> Luôn giữ tính năng **Associative** (Liên kết) được bật sáng trên Ribbon. Khi Associative bật, mỗi khi bạn kéo giãn co giãn đường bao bên ngoài, hoa văn Hatch bên trong sẽ tự động co giãn theo mà không bị hở.

> [!TIP]
> Nếu bấm Pick Point mà bị treo máy vài giây, nguyên nhân do bản vẽ quá rộng và phức tạp. Hãy zoom to lại gần vùng cần tô trước khi gõ lệnh H để AutoCAD chỉ phải tính toán các nét trong khung hình hiện hành.

## Tự kiểm tra

```quiz
id: q-ac-02-09-1
type: single
question: Mẫu hoa văn mặt cắt nào dưới đây là tiêu chuẩn thông dụng nhất để thể hiện mặt cắt vật liệu kim loại (gang, thép)?
options:
  - text: ANSI31
    correct: true
    why: ANSI31 là mẫu gạch chéo 45 độ tiêu chuẩn thể hiện kim loại
  - text: SOLID
    why: SOLID tô mảng màu đặc kín
  - text: AR-CONC
    why: AR-CONC dùng cho bê tông cốt liệu sỏi
  - text: BRICK
    why: BRICK thể hiện gạch xây tường
explain: "Mẫu hoa văn ANSI31 (các đường chéo song song nghiêng 45 độ) là quy ước kỹ thuật tiêu chuẩn quốc tế để biểu diễn mặt cắt của các chi tiết kim loại gia công cơ khí."
tags: [hatch, ansi31, hoa-van]
```

```quiz
id: q-ac-02-09-2
type: single
question: Khi tô Hatch xong, hoa văn hiển thị như một mảng màu đặc đen sì không thấy từng đường gạch đâu. Nguyên nhân chủ yếu là gì?
options:
  - text: Tỷ lệ hoa văn (Hatch Scale) đang quá nhỏ so với kích thước vùng vẽ
    correct: true
    why: Scale quá bé làm hàng vạn nét vẽ xếp sít nhau đặc kín
  - text: Bản vẽ bị lỗi hở đường bao
    why: Hở đường bao thì AutoCAD sẽ báo lỗi không cho tô
  - text: Chọn nhầm màu đen
    why: Do mật độ nét quá dày đặc tạo cảm giác như mảng đặc
  - text: AutoCAD không hỗ trợ mẫu hoa văn đó
    why: Mẫu hoa văn có sẵn trong thư viện
explain: "Khi Hatch Pattern Scale đặt quá nhỏ, các đường nét hoa văn vẽ cách nhau chỉ 0.01mm sẽ xếp chồng khít lên nhau tạo thành một mảng đen kín. Bạn chỉ cần tăng giá trị Scale lên (ví dụ từ 1 lên 20)."
tags: [hatch, scale, loi]
```

```quiz
id: q-ac-02-09-3
type: truefalse
question: Tính năng Associative trong Hatch giúp mặt cắt tự động co giãn cập nhật hình dáng khi đường biên xung quanh bị di dời hoặc kéo giãn.
answer: true
explain: "Associative (Hatch liên kết) khoá chặt thực thể Hatch vào đường biên bao. Mọi biến đổi hình học của đường biên sẽ kéo theo mặt cắt cập nhật tức thì."
tags: [hatch, associative]
```

```quiz
id: q-ac-02-09-4
type: hotspot
question: Bấm vào vùng tô mặt cắt ANSI31 trên sơ đồ minh hoạ.
use: hotspots
answer: hatch-pick
explain: "Mặt cắt ANSI31 nằm ở nửa bên trái của sơ đồ, có các đường gạch chéo song song 45 độ tự trừ lỗ tròn rỗng ở tâm."
tags: [hatch, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Xuất hiện thông báo lỗi *"A closed boundary cannot be determined"* kèm các vòng tròn đỏ nhấp nháy trên màn hình.
  - *Nguyên nhân:* Đường biên của bạn bị hở (hai đầu mút chưa chạm khít nhau) nên AutoCAD không xác định được vùng kín.
  - *Cách sửa:* Quan sát các chấm đỏ đánh dấu vị trí hở, phóng to lên và dùng Osnap Endpoint hoặc lệnh FILLET bo kín góc hở lại.
- **Triệu chứng:** Khi tô mặt cắt, toàn bộ màn hình xung quanh bị tô kín luôn cả những vùng không mong muốn.
  - *Nguyên nhân:* Vùng chọn bị thủng hoặc có lỗ hở khiến mực Hatch tràn ra ngoài không gian Model.
  - *Cách sửa:* Nhấn [Ctrl + Z], kiểm tra kỹ lại toàn bộ chu vi đường bao xem có phân đoạn nào bị đứt quãng không.

## Bài tập thực hành

- [ ] Gõ `RECTANG` vẽ một hình chữ nhật kích thước `@150,100`. <!-- expect: RECTANG -->
- [ ] Gõ `CIRCLE` vẽ một đường tròn bán kính `25` nằm hoàn toàn bên trong hình chữ nhật đó. <!-- expect: CIRCLE -->
- [ ] Gõ `HATCH`, chọn mẫu hoa văn `ANSI31`. <!-- expect: HATCH -->
- [ ] Nhấp chuột (Pick Point) vào khoảng trống giữa hình chữ nhật và đường tròn.
- [ ] Quan sát thấy mặt cắt tự động lấp đầy phần ngoài và để chừa rỗng lỗ tròn ở giữa.
- [ ] Nhấn [Enter] để hoàn thành lệnh Hatch.

## Nguồn tham khảo

```links
- title: Lệnh HATCH và cách tô mặt cắt vật liệu (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=HATCH+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn Pick Points, Select, Pattern, Scale, Associative của lệnh HATCH
- title: Lệnh GRADIENT tô màu chuyển sắc (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=GRADIENT+Command
  kind: official
  lang: en
  note: Hướng dẫn phối màu 1 màu hoặc 2 màu cho đồ hoạ kiến trúc
```
