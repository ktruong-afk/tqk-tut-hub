---
id: ac-02-11
title: Thực hành tổng hợp bản vẽ chi tiết cơ khí 2D
category: Vẽ 2D
tags: [tong-hop, co-khi, ve-2d, thuc-hanh, flange]
level: beginner
minutes: 25
needs: [ac-02-09, ac-02-10]
appVersions: ['2024', '2025']
edition: all
---
# Thực hành tổng hợp bản vẽ chi tiết cơ khí 2D

> **Mục tiêu:**
> - Kết hợp thành thạo các lệnh LINE, CIRCLE, RECTANG và HATCH để hoàn thành bản vẽ mặt bích cơ khí 2D hoàn chỉnh.
> - Áp dụng các chế độ bắt điểm Osnap (Center, Endpoint, Midpoint) và phương pháp toạ độ để định vị chính xác.
> - Ghi chú tên gọi và thông số kỹ thuật cho chi tiết bằng lệnh TEXT kèm ký hiệu đường kính phi (%%c).

## Lệnh này làm gì và khi nào dùng

Sau khi đã nắm vững từng lệnh vẽ hình học riêng lẻ trong Chặng 02, đây là bài thực hành tổng hợp thực chiến để bạn kết nối toàn bộ kỹ năng lại với nhau.

Chúng ta sẽ cùng nhau vẽ một chi tiết kỹ thuật kinh điển trong ngành cơ khí: **Mặt bích tròn (Flange)** gồm:
1. Đường tròn viền ngoài đường kính Ø280mm.
2. Vòng chia tâm lỗ bu lông đường kính Ø210mm.
3. 4 lỗ bắt bu lông phân bố đều đối xứng kích thước Ø28mm.
4. Lỗ trục tâm đường kính Ø90mm có rãnh then (keyway) kích thước 16×10mm.
5. Mặt cắt hoa văn gạch chéo kim loại ANSI31 phủ lên thân mặt bích.
6. Chữ ghi chú tên chi tiết và vật liệu bằng lệnh TEXT.

```hotspots
image: media/ac-02-11-tong-hop-part.svg
alt: Bản vẽ chi tiết mặt bích cơ khí tròn gồm các lỗ bu lông, lỗ then và mặt cắt ANSI31
layout: central
points:
  - id: outer-flange
    x: 50
    y: 52
    title: Thân mặt bích ngoài (Ø280)
    text: Đường tròn bao lớn nhất được tô hoa văn mặt cắt kim loại ANSI31.
    quiz: q-ac-02-11-1
  - id: bolt-holes
    x: 50
    y: 29
    title: 4 Lỗ bu lông đối xứng (Ø28)
    text: Phân bố đều trên đường tròn tâm Ø210 tại 4 vị trí góc phần tư 0°, 90°, 180°, 270°.
    quiz: q-ac-02-11-2
  - id: shaft-keyway
    x: 50
    y: 47
    title: Lỗ trục và rãnh then (Ø90 + rãnh 16×10)
    text: Kết hợp đường tròn tâm và hình chữ nhật RECTANG để tạo rãnh then truyền mô-men xoắn.
```

## Cách dùng từng bước

1. **Vẽ hệ trục định vị tâm:**
   - Gõ `LINE`, bật [F8] (Ortho), vẽ một đường ngang dài 340mm và một đường đứng dài 340mm giao nhau tại gốc toạ độ `0,0`.
2. **Vẽ đường tròn thân bích ngoài:**
   - Gõ `CIRCLE` (phím tắt `C`), chọn tâm tại giao điểm `0,0`.
   - Gõ `D` (Diameter), nhập đường kính `280` rồi nhấn [Enter].
3. **Vẽ đường tròn chia lỗ bu lông:**
   - Gõ `C`, chọn tâm tại `0,0`.
   - Gõ `D`, nhập đường kính `210` rồi nhấn [Enter].
4. **Vẽ 4 lỗ bu lông Ø28:**
   - Bật Osnap [F3] chế độ *Quadrant* và *Intersection*.
   - Gõ `C`, chọn tâm tại điểm góc phần tư trên đỉnh của vòng chia vừa vẽ.
   - Gõ `D`, nhập đường kính `28` rồi [Enter].
   - Lặp lại để vẽ tiếp 3 lỗ bu lông ở các vị trí dưới đáy, bên trái và bên phải.
5. **Vẽ lỗ trục tâm và rãnh then:**
   - Gõ `C`, chọn tâm tại `0,0`, gõ `D` và nhập đường kính `90` rồi [Enter].
   - Gõ `RECTANG` vẽ hình chữ nhật kích thước `@16,20` tại đỉnh lỗ tròn để tạo rãnh then.
6. **Tô mặt cắt Hatch:**
   - Gõ `HATCH` (phím tắt `H`), chọn mẫu `ANSI31`.
   - Nhấp chuột (Pick Point) vào khoảng thân giữa đường tròn Ø280 và đường tròn Ø90. AutoCAD sẽ tự động chừa trống 4 lỗ bu lông và lỗ trục.
   - Đặt tỷ lệ Scale phù hợp (ví dụ `2.0`) rồi nhấn [Enter].
7. **Ghi chú tiêu đề bản vẽ:**
   - Gõ `TEXT`, bấm điểm đặt chữ phía dưới hình.
   - Nhập chiều cao chữ `7.0`, góc xoay `0`.
   - Gõ: `MAT BICH TRUC - %%c280` rồi nhấn [Enter] hai lần.

## Tuỳ chọn và mẹo

> [!TIP]
> Tận dụng 4 điểm góc phần tư (Quadrant) của đường tròn tâm giúp bạn đặt 4 lỗ bu lông đối xứng tuyệt đối mà không cần phải gõ toạ độ hay đo góc.

> [!TIP]
> Luôn tô mặt cắt Hatch ở bước cuối cùng sau khi toàn bộ đường nét biên bao và lỗ khoan đã được định hình hoàn tất để tránh phải xoá Hatch tô lại nhiều lần.

## Tự kiểm tra

```quiz
id: q-ac-02-11-1
type: single
question: Khi tô mặt cắt HATCH vào một chi tiết có các lỗ tròn bên trong, tính năng nào giúp AutoCAD tự động không tô đè lên các lỗ tròn đó?
options:
  - text: Tự động phát hiện đảo rỗng (Island Detection)
    correct: true
    why: Island Detection nhận diện các biên kín bên trong và chừa rỗng không tô
  - text: Lệnh ERASE tự động
    why: ERASE là lệnh xoá thủ công
  - text: Tự động đổi layer của lỗ tròn
    why: Hatch không đổi layer của đối tượng khác
  - text: Phím F8 Ortho
    why: F8 chỉ dùng để khoá phương thẳng
explain: "Tính năng Island Detection tích hợp sẵn trong thuật toán Pick Point của HATCH sẽ tự động nhận diện các đường biên kín nằm lọt bên trong và giữ nguyên không tô."
tags: [tong-hop, hatch, island]
```

```quiz
id: q-ac-02-11-2
type: single
question: Để vẽ 4 lỗ bu lông nằm chính xác ở các hướng trên, dưới, trái, phải của vòng tròn chia tâm, bạn nên dùng chế độ bắt điểm Osnap nào?
options:
  - text: Quadrant (Góc phần tư)
    correct: true
    why: Quadrant bắt chính xác 4 đỉnh 0°, 90°, 180°, 270° của đường tròn
  - text: Midpoint
    why: Đường tròn khép kín không có Midpoint
  - text: Endpoint
    why: Đường tròn khép kín không có Endpoint
  - text: Tangent
    why: Tangent dùng để bắt tiếp tuyến
explain: "Chế độ bắt điểm Quadrant (F3) tự động hút vào 4 điểm cực của đường tròn, là cách nhanh và chính xác nhất để định vị lỗ bu lông đối xứng."
tags: [tong-hop, osnap, quadrant]
```

```quiz
id: q-ac-02-11-3
type: truefalse
question: Khi ghi kích thước đường kính cho mặt bích, cú pháp `%%c280` trong lệnh TEXT sẽ hiển thị thành `Ø280` trên bản vẽ.
answer: true
explain: "Mã điều khiển %%c tự động được AutoCAD biên dịch thành ký hiệu phi đường kính Ø trong mọi phông chữ tiêu chuẩn."
tags: [tong-hop, text, phi]
```

```quiz
id: q-ac-02-11-4
type: hotspot
question: Bấm vào vị trí lỗ bu lông Ø28 trên bản vẽ chi tiết mặt bích.
use: hotspots
answer: bolt-holes
explain: "Lỗ bu lông nằm ở góc trên của vòng chia tâm, được thể hiện bằng đường tròn đường kính Ø28."
tags: [tong-hop, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Mực Hatch tô đè kín mít toàn bộ không chừa lại các lỗ bu lông hay lỗ trục tâm.
  - *Nguyên nhân:* Tùy chọn *Island Display Style* đang bị chỉnh sang chế độ *Ignore* (bỏ qua mọi đảo rỗng).
  - *Cách sửa:* Chọn Hatch, mở bảng tùy chọn và chuyển *Island Detection* về chế độ *Normal* hoặc *Outer*.
- **Triệu chứng:** 4 lỗ bu lông bị lệch tâm không đều nhau.
  - *Nguyên nhân:* Bắt điểm tự do bằng mắt thay vì bật chế độ Osnap Quadrant hoặc Intersection trên vòng tròn tâm.
  - *Cách sửa:* Gõ `OSNAP`, tích chọn ô *Quadrant* rồi dùng lệnh `MOVE` chỉnh lại tâm các lỗ bu lông về đúng 4 vị trí đỉnh.

## Bài tập thực hành

- [ ] Gõ `CIRCLE`, chọn tâm tại `0,0`, gõ `D` và nhập đường kính `280` để tạo thân bích. <!-- expect: CIRCLE -->
- [ ] Gõ `CIRCLE`, chọn tâm tại `0,0`, gõ `D` và nhập `90` để tạo lỗ trục giữa. <!-- expect: CIRCLE -->
- [ ] Gõ `CIRCLE` vẽ một lỗ bu lông đường kính `28` tại điểm Quadrant phía trên của vòng chia. <!-- expect: CIRCLE -->
- [ ] Gõ `HATCH`, chọn mẫu `ANSI31` và bấm một điểm vào thân mặt bích để tô hoa văn kim loại. <!-- expect: HATCH -->
- [ ] Gõ `TEXT` và ghi dòng nhãn `MAT BICH %%c280` phía dưới bản vẽ. <!-- expect: TEXT -->

## Nguồn tham khảo

```links
- title: Quy trình tạo bản vẽ cơ khí 2D hoàn chỉnh (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=2D+Mechanical+Drawings
  kind: official
  lang: en
  note: Hướng dẫn kết hợp các đối tượng 2D và tiêu chuẩn bản vẽ cơ khí quốc tế
- title: Lệnh HATCH và phát hiện đảo rỗng Island (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Island+Detection
  kind: official
  lang: en
  note: Giải thích cơ chế lồng nhau và trừ diện tích vùng kín của Hatch
```
