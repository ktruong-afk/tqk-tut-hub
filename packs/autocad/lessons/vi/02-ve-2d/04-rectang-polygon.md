---
id: ac-02-04
title: Vẽ hình chữ nhật với RECTANG và đa giác với POLYGON
category: Vẽ 2D
tags: [rectang, polygon, ve-2d, hinh-chu-nhat, da-giac]
level: beginner
minutes: 15
needs: [ac-02-01]
appVersions: ['2024', '2025']
edition: all
---
# Vẽ hình chữ nhật với RECTANG và đa giác với POLYGON

> **Mục tiêu:**
> - Sử dụng lệnh RECTANG để tạo hình chữ nhật chính xác theo kích thước dài rộng (Dimensions).
> - Phân biệt phương thức vẽ đa giác đều nội tiếp (Inscribed) và ngoại tiếp (Circumscribed) trong lệnh POLYGON.
> - Hiểu rõ cấu trúc hình học của hình chữ nhật và đa giác là một đối tượng đường đa tuyến khép kín (Polyline).

## Lệnh này làm gì và khi nào dùng

Thay vì phải gõ lệnh LINE 4 lần để vẽ một khung hình, AutoCAD cung cấp hai lệnh dựng hình đa giác khép kín cực kỳ nhanh chóng:
- `RECTANG` (phím tắt `REC`): Tạo [[Hình chữ nhật]] hoặc hình vuông từ hai điểm góc đối diện chéo nhau.
- `POLYGON` (phím tắt `POL`): Tạo [[Đa giác đều]] có số cạnh từ 3 đến 1024 cạnh (tam giác đều, ngũ giác, lục giác đầu bu lông, bát giác...).

Đặc điểm rất quan trọng: Cả hình chữ nhật và đa giác đều được AutoCAD lưu trữ dưới dạng một [[Đường đa tuyến]] khép kín duy nhất. Khi bạn bấm chọn một cạnh, toàn bộ các cạnh còn lại đều được chọn cùng một lúc.

```hotspots
image: media/ac-02-04-rect-poly.svg
alt: Minh hoạ thông số góc chéo đối diện của RECTANG và đa giác đều nội tiếp ngoại tiếp của POLYGON
layout: central
points:
  - id: rect-corners
    x: 25
    y: 35
    title: Lệnh RECTANG (Hai góc đối diện)
    text: Xác định qua toạ độ góc thứ nhất (X1,Y1) và toạ độ góc thứ hai đối diện (@W,H).
    quiz: q-ac-02-04-1
  - id: poly-inscribed
    x: 65
    y: 40
    title: Đa giác nội tiếp (Inscribed in circle)
    text: Các đỉnh của đa giác nằm tiếp xúc trên chu vi đường tròn bán kính R.
    quiz: q-ac-02-04-2
  - id: poly-circumscribed
    x: 85
    y: 40
    title: Đa giác ngoại tiếp (Circumscribed about circle)
    text: Trung điểm các cạnh của đa giác tiếp xúc với chu vi đường tròn bán kính R.
```

## Cách dùng từng bước

1. **Vẽ hình chữ nhật theo toạ độ tương đối (RECTANG):**
   - Gõ `RECTANG` hoặc `REC` rồi nhấn [Enter].
   - Bấm điểm góc thứ nhất (First corner).
   - Nhập toạ độ góc đối diện dạng `@Chiều_dài,Chiều_rộng` (ví dụ `@150,80`) rồi nhấn [Enter].
2. **Vẽ hình chữ nhật theo kích thước (Dimensions):**
   - Gõ `REC` [Enter], bấm điểm góc thứ nhất.
   - Gõ chữ `D` (Dimensions) rồi nhấn [Enter].
   - Nhập chiều dài (Length, ví dụ `200`) rồi [Enter].
   - Nhập chiều rộng (Width, ví dụ `100`) rồi [Enter].
   - Nhấp chuột trái để chọn 1 trong 4 góc phần tư đặt hình.
3. **Vẽ đa giác đều (POLYGON):**
   - Gõ `POLYGON` hoặc `POL` rồi nhấn [Enter].
   - Nhập số lượng cạnh (ví dụ `6` cho đầu bu lông lục giác) rồi [Enter].
   - Nhấp chọn tâm đa giác (Center of polygon).
   - Chọn kiểu đa giác:
     - Gõ `I` (Inscribed): Đa giác nội tiếp trong đường tròn.
     - Gõ `C` (Circumscribed): Đa giác ngoại tiếp ngoài đường tròn.
   - Nhập bán kính đường tròn chuẩn (ví dụ `40`) rồi nhấn [Enter].

## Tuỳ chọn và mẹo

> [!TIP]
> Lệnh `RECTANG` có các tuỳ chọn vát mép (Chamfer) và bo tròn góc (Fillet) trực tiếp. Gõ `F` trước khi chọn điểm góc đầu tiên để đặt bán kính bo tròn cho cả 4 góc cùng lúc.

> [!TIP]
> Khi vẽ đầu bu lông lục giác cơ khí, khoảng cách giữa 2 cạnh đối diện (cỡ chìa vặn cờ-lê S) bằng hai lần bán kính đường tròn ngoại tiếp (Circumscribed). Hãy chọn tuỳ chọn `C` với bán kính `S / 2`.

## Tự kiểm tra

```quiz
id: q-ac-02-04-1
type: single
question: Khi vẽ hình chữ nhật bằng lệnh RECTANG, cú pháp toạ độ nào dùng để tạo hình có chiều dài 120mm và chiều cao 60mm từ góc thứ nhất?
options:
  - text: "@120,60"
    correct: true
    why: "@X,Y biểu thị độ dời chiều dài 120 theo phương ngang và 60 theo phương đứng"
  - text: "@120<60"
    why: "Ký tự < dùng cho toạ độ cực khoảng cách và góc"
  - text: "120,60"
    why: "Không có @ sẽ bị hiểu là toạ độ tuyệt đối so với gốc 0,0"
  - text: "REC 120 60"
    why: "Sai cú pháp dòng lệnh AutoCAD"
explain: "Cú pháp @120,60 nhập độ dời tương đối delta X = 120 (chiều dài) và delta Y = 60 (chiều cao) so với điểm góc bạn vừa bấm chọn."
tags: [rectang, toa-do]
```

```quiz
id: q-ac-02-04-2
type: single
question: Trong lệnh POLYGON, tuỳ chọn "Inscribed in circle" (gõ chữ I) có nghĩa là gì?
options:
  - text: Đa giác có các đỉnh nằm trên đường tròn bán kính R (nội tiếp)
    correct: true
    why: Inscribed nghĩa là đa giác nội tiếp bên trong đường tròn
  - text: Đa giác có các cạnh tiếp xúc với đường tròn bán kính R (ngoại tiếp)
    why: Đó là định nghĩa của Circumscribed
  - text: Đa giác có diện tích bằng diện tích đường tròn
    why: AutoCAD không tính đa giác theo diện tích tương đương
  - text: Đa giác chỉ có 4 cạnh vuông góc
    why: Số cạnh đa giác do người dùng tự nhập từ 3 đến 1024
explain: "Đa giác nội tiếp (Inscribed in circle) có bán kính tính từ tâm đến các đỉnh của đa giác, tương ứng với đường tròn đi qua tất cả các đỉnh đó."
tags: [polygon, inscribed]
```

```quiz
id: q-ac-02-04-3
type: truefalse
question: Một hình chữ nhật tạo bằng lệnh RECTANG có thể được tách rời thành 4 đoạn thẳng độc lập bằng lệnh EXPLODE.
answer: true
explain: "Vì hình chữ nhật là một đường Polyline liền khối, bạn hoàn toàn có thể dùng lệnh EXPLODE (gõ tắt X) để phá vỡ nó thành 4 đoạn thẳng Line độc lập."
tags: [rectang, explode, pline]
```

```quiz
id: q-ac-02-04-4
type: hotspot
question: Bấm vào sơ đồ đa giác nội tiếp (Inscribed in circle) trên hình minh hoạ.
use: hotspots
answer: poly-inscribed
explain: "Đa giác nội tiếp nằm ở giữa bên phải, có các đỉnh chạm vào chu vi đường tròn nét đứt."
tags: [polygon, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Nhập `@150,80` nhưng hình chữ nhật bị vẽ lệch hướng xuống dưới sang trái.
  - *Nguyên nhân:* Nhập nhầm dấu âm hoặc hướng con trỏ chuột trong chế độ Dimensions.
  - *Cách sửa:* Nhập giá trị dương `@150,80` để hình mở rộng lên trên sang phải, hoặc dùng tuỳ chọn `Dimensions` rồi nhấp chuột vào góc phần tư mong muốn.
- **Triệu chứng:** Muốn vẽ lục giác đều bu lông nhưng khi đo giữa hai mặt phẳng cạnh lại bị to hơn kích thước cờ-lê.
  - *Nguyên nhân:* Chọn nhầm tuỳ chọn *Inscribed* (nội tiếp, bán kính tính đến góc) thay vì *Circumscribed* (ngoại tiếp, bán kính tính đến cạnh).
  - *Cách sửa:* Chọn tuỳ chọn `Circumscribed` (phím `C`) khi vẽ bu lông đai ốc.

## Bài tập thực hành

- [ ] Gõ `RECTANG`, bấm một điểm góc và nhập `@160,90` để vẽ hình chữ nhật kích thước 160×90mm. <!-- expect: RECTANG -->
- [ ] Gõ `POLYGON`, nhập số cạnh là `6`. <!-- expect: POLYGON -->
- [ ] Chọn tâm trùng với tâm của hình chữ nhật vừa vẽ.
- [ ] Chọn tuỳ chọn `Inscribed in circle` (gõ `I`) và nhập bán kính `35`.
- [ ] Nhấp chọn hình chữ nhật để xác nhận toàn bộ 4 cạnh được chọn liền mạch như một đối tượng Polyline.

## Nguồn tham khảo

```links
- title: Lệnh RECTANG và tuỳ chọn kích thước (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=RECTANG+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn Chamfer, Fillet, Elevation, Thickness của lệnh RECTANG
- title: Lệnh POLYGON dựng đa giác đều (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=POLYGON+Command
  kind: official
  lang: en
  note: Hướng dẫn vẽ đa giác nội tiếp, ngoại tiếp và theo độ dài cạnh Edge
```
