---
id: ac-02-02
title: Vẽ đường tròn với lệnh CIRCLE
category: Vẽ 2D
tags: [circle, ve-2d, duong-tron, ban-kinh, duong-kinh]
level: beginner
minutes: 15
needs: [ac-02-01]
appVersions: ['2024', '2025']
edition: all
---
# Vẽ đường tròn với lệnh CIRCLE

> **Mục tiêu:**
> - Sử dụng lệnh CIRCLE để vẽ đường tròn theo bán kính (Radius) và đường kính (Diameter).
> - Phân biệt các phương pháp vẽ đường tròn phụ trợ: 2-Point (2P), 3-Point (3P) và Tan, Tan, Radius (TTR).
> - Bắt chính xác điểm tâm tròn (Center) và các điểm góc phần tư (Quadrant) bằng Osnap.

## Lệnh này làm gì và khi nào dùng

Lệnh `CIRCLE` (phím tắt `C`) dùng để tạo [[Đường tròn]] khép kín trong không gian 2D. Trong thiết kế cơ khí và xây dựng, đường tròn xuất hiện ở khắp nơi: lỗ bu lông, mặt cắt trục, ống dẫn nước và các góc lượn.

AutoCAD cung cấp 6 phương pháp xác định đường tròn:
1. **Center, Radius (Tâm, Bán kính):** Cách mặc định, chọn tâm rồi nhập [[Bán kính]].
2. **Center, Diameter (Tâm, Đường kính):** Chọn tâm, gõ `D` rồi nhập [[Đường kính]].
3. **2-Point (2P):** Xác định qua 2 điểm mút của đường kính.
4. **3-Point (3P):** Đi qua 3 điểm bất kỳ trong không gian.
5. **Tan, Tan, Radius (TTR):** Tiếp xúc với 2 đối tượng có sẵn và có bán kính cho trước.
6. **Tan, Tan, Tan:** Tiếp xúc đồng thời với 3 cạnh hoặc 3 đường tròn khác.

```hotspots
image: media/ac-02-02-circle-methods.svg
alt: Sơ đồ minh hoạ 5 phương pháp dựng đường tròn bằng lệnh CIRCLE trong AutoCAD
layout: central
points:
  - id: method-center-radius
    x: 20
    y: 20
    title: 1. Center, Radius
    text: Phương pháp cơ bản nhất. Bấm điểm tâm rồi nhập khoảng cách bán kính R.
    quiz: q-ac-02-02-1
  - id: method-center-diameter
    x: 50
    y: 20
    title: 2. Center, Diameter
    text: Bấm điểm tâm, kích hoạt tuỳ chọn Diameter (phím D) rồi nhập đường kính danh nghĩa Ø.
  - id: method-2p
    x: 80
    y: 20
    title: 3. 2-Point (2P)
    text: Vẽ đường tròn đi qua 2 điểm đầu mút của đường kính đối diện nhau.
  - id: method-ttr
    x: 35
    y: 75
    title: 4. Tan, Tan, Radius (TTR)
    text: Dựng đường tròn tiếp xúc (Tangent) với hai đối tượng và có bán kính xác định.
    quiz: q-ac-02-02-2
```

## Cách dùng từng bước

1. **Vẽ theo Tâm và Bán kính (Center, Radius):**
   - Gõ `CIRCLE` hoặc `C` rồi nhấn [Enter].
   - Nhấp chuột chọn vị trí tâm (hoặc gõ toạ độ `100,100`).
   - Gõ giá trị bán kính (ví dụ `35`) rồi nhấn [Enter].
2. **Vẽ theo Tâm và Đường kính (Center, Diameter):**
   - Gõ `C` rồi nhấn [Enter].
   - Nhấp chọn tâm đường tròn.
   - Gõ chữ `D` rồi nhấn [Enter] để chuyển sang chế độ đường kính.
   - Nhập đường kính (ví dụ `70`) rồi nhấn [Enter].
3. **Vẽ tiếp xúc 2 cạnh và bán kính (TTR):**
   - Gõ `C` rồi nhấn [Enter].
   - Gõ `TTR` rồi nhấn [Enter].
   - Nhấp chọn đường thẳng thứ nhất, nhấp chọn đường thẳng thứ hai.
   - Nhập bán kính tiếp xúc (ví dụ `25`) rồi nhấn [Enter].
4. **Vẽ qua 2 điểm (2P):**
   - Gõ `C` [Enter] rồi gõ `2P` [Enter].
   - Bấm điểm đầu tiên, sau đó bấm điểm thứ hai đối diện.

## Tuỳ chọn và mẹo

> [!TIP]
> Trong bản vẽ cơ khí, thông số thường cho theo đường kính Ø (ví dụ lỗ Ø20). Hãy nhớ gõ thêm chữ `D` sau khi bấm tâm để không phải mất công chia đôi giá trị nhẩm ra bán kính.

> [!TIP]
> Bật chế độ bắt điểm Quadrant (góc phần tư) trong Osnap để bắt chính xác 4 điểm cực Bắc, Nam, Đông, Tây (0°, 90°, 180°, 270°) của đường tròn.

## Tự kiểm tra

```quiz
id: q-ac-02-02-1
type: single
question: Khi thực hiện lệnh CIRCLE, giá trị số bạn nhập sau khi chọn tâm mặc định được AutoCAD hiểu là gì?
options:
  - text: Bán kính (Radius)
    correct: true
    why: AutoCAD mặc định nhận giá trị bán kính nếu không gõ thêm tuỳ chọn
  - text: Đường kính (Diameter)
    why: Muốn nhập đường kính bạn phải gõ tuỳ chọn D trước
  - text: Chu vi đường tròn
    why: AutoCAD không hỗ trợ nhập trực tiếp chu vi
  - text: Diện tích hình tròn
    why: Diện tích không phải thông số đầu vào của lệnh CIRCLE
explain: "Theo mặc định của lệnh CIRCLE, sau khi chọn tâm, AutoCAD sẽ yêu cầu Specify radius of circle. Muốn nhập đường kính phải gõ D (Diameter)."
tags: [circle, radius, diameter]
```

```quiz
id: q-ac-02-02-2
type: single
question: Để vẽ một đường tròn tiếp xúc với hai cạnh góc vuông và có bán kính R=30, bạn chọn tuỳ chọn nào của lệnh CIRCLE?
options:
  - text: TTR (Tan, Tan, Radius)
    correct: true
    why: TTR xác định đường tròn qua 2 tiếp tuyến và 1 bán kính
  - text: 2P (2-Point)
    why: 2P chỉ đi qua 2 điểm mút đường kính, không đảm bảo tiếp tuyến
  - text: 3P (3-Point)
    why: 3P cần 3 điểm đi qua thay vì tiếp xúc
  - text: Center, Radius
    why: Bạn chưa biết toạ độ tâm để bấm Center
explain: "Tuỳ chọn TTR (Tangent, Tangent, Radius) cho phép bạn nhấp vào hai đối tượng tiếp xúc rồi nhập bán kính để AutoCAD tự tính toán vị trí tâm."
tags: [circle, ttr]
```

```quiz
id: q-ac-02-02-3
type: truefalse
question: Chế độ bắt điểm Quadrant trong Osnap giúp bắt chính xác 4 điểm góc phần tư ở các vị trí 0°, 90°, 180° và 270° trên đường tròn.
answer: true
explain: "Điểm bắt Quadrant nằm ở 4 đỉnh giao của đường tròn với hệ trục toạ độ đi qua tâm (hướng 3h, 6h, 9h và 12h)."
tags: [circle, quadrant, osnap]
```

```quiz
id: q-ac-02-02-4
type: hotspot
question: Bấm vào phương pháp Tan, Tan, Radius (TTR) trên sơ đồ lệnh CIRCLE.
use: hotspots
answer: method-ttr
explain: "Phương pháp TTR nằm ở nửa dưới bên trái của sơ đồ minh hoạ."
tags: [circle, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Cần vẽ lỗ đường kính 50mm nhưng khi đo kích thước lại ra thành đường kính 100mm.
  - *Nguyên nhân:* Quên không gõ chữ `D` sau khi chọn tâm, dẫn đến AutoCAD hiểu số 50 là bán kính (R50 tương đương Ø100).
  - *Cách sửa:* Khi gõ lệnh `C`, chọn tâm xong hãy gõ ngay chữ `D` [Enter] rồi mới nhập số `50`.
- **Triệu chứng:** Dùng tuỳ chọn TTR nhưng AutoCAD báo lỗi *"Circle does not exist"*.
  - *Nguyên nhân:* Bán kính nhập vào quá nhỏ hoặc hai đối tượng tiếp xúc nằm ở vị trí không thể tạo được hình tròn thoả mãn.
  - *Cách sửa:* Kiểm tra lại kích thước hình học và tăng bán kính R phù hợp với khoảng cách giữa hai đối tượng.

## Bài tập thực hành

- [ ] Gõ lệnh `CIRCLE` và chọn tâm tại toạ độ `100,100`. <!-- expect: CIRCLE -->
- [ ] Nhập bán kính `40` và nhấn [Enter] để hoàn thành đường tròn thứ nhất.
- [ ] Gõ lại `CIRCLE`, chọn tâm đồng tâm tại điểm tâm của hình tròn vừa vẽ (bắt điểm Center). <!-- expect: CIRCLE -->
- [ ] Gõ chữ `D` và nhập đường kính `50` rồi nhấn [Enter].
- [ ] Gõ `CIRCLE`, nhập tuỳ chọn `2P` rồi bấm hai điểm bất kỳ để tạo đường tròn qua 2 điểm. <!-- expect: CIRCLE -->

## Nguồn tham khảo

```links
- title: Lệnh CIRCLE và các phương pháp dựng hình (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=CIRCLE+Command
  kind: official
  lang: en
  note: Hướng dẫn chi tiết các tuỳ chọn 2P, 3P, TTR và tiếp xúc trong AutoCAD
- title: Chế độ bắt điểm Quadrant và Center (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Snap+to+Geometric+Points
  kind: official
  lang: en
  note: Hướng dẫn bắt điểm hình học trên đường tròn và cung tròn
```
