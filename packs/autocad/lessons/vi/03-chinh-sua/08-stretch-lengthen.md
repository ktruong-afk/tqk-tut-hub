---
id: ac-03-08
title: Kéo giãn với STRETCH và kéo dài với LENGTHEN
category: Chỉnh sửa
tags: [stretch, lengthen, keo-gian, crossing, chinh-sua, kich-thuoc]
level: beginner
minutes: 15
needs: [ac-03-02]
appVersions: ['2024', '2025']
edition: all
---
# Kéo giãn với STRETCH và kéo dài với LENGTHEN

> **Mục tiêu:**
> - Sử dụng lệnh STRETCH để thay đổi kích thước một phần của đối tượng mà vẫn giữ nguyên các liên kết hình học.
> - Nắm vững quy tắc bắt buộc phải sử dụng hộp chọn Crossing Selection (Phải sang Trái) trong lệnh STRETCH.
> - Sử dụng lệnh LENGTHEN để thay đổi chiều dài đoạn thẳng theo giá trị chênh lệch (Delta), tổng số (Total) hoặc tỷ lệ phần trăm (Percent).

## Lệnh này làm gì và khi nào dùng

Khi bản vẽ đã hoàn thành nhưng khách hàng yêu cầu: *"Hãy kéo dài căn phòng thêm 1 mét"* hoặc *"Hãy kéo dài thân trục van thêm 20mm"*, nếu bạn phải xoá đi vẽ lại hoặc di chuyển từng đường nét rồi dùng Trim/Extend thì sẽ mất hàng giờ. Lệnh cứu tinh ở đây chính là `STRETCH`:
- `STRETCH` (phím tắt `S`): [[Kéo giãn]] hoặc co ngắn một phần hình học của đối tượng. Tất cả các đỉnh (vertices) nằm bên trong vùng chọn sẽ được tịnh tiến đi, trong khi các cạnh bị cắt qua sẽ tự động giãn dài ra hoặc co ngắn lại như một dải cao su đàn hồi.
- `LENGTHEN` (phím tắt `LEN`): Thay đổi chiều dài của đoạn thẳng hoặc góc mở của cung tròn theo 4 phương thức toán học: Delta (cộng/trừ thêm khoảng d), Percent (tăng theo %), Total (đặt tổng chiều dài mới) hoặc Dynamic (kéo tự do).

Quy tắc bất biến của lệnh STRETCH: Bạn **bắt buộc** phải chọn đối tượng bằng khung chọn [[Hộp chọn cắt qua]] (Crossing Selection - quét từ Phải sang Trái). Nếu chọn sai khung, lệnh STRETCH sẽ biến thành lệnh MOVE thông thường!

```hotspots
image: media/ac-03-08-stretch-crossing.svg
alt: Sơ đồ minh hoạ quy tắc bắt buộc dùng khung chọn Crossing Selection khi thực hiện lệnh STRETCH
layout: central
points:
  - id: stretch-crossing-box
    x: 25
    y: 35
    title: "Bước 1: Quét khung Crossing (Xanh lá)"
    text: Quét từ Phải sang Trái bao quanh các đỉnh cần kéo giãn và cắt qua các cạnh cần kéo dài.
    quiz: q-ac-03-08-1
  - id: stretch-result
    x: 75
    y: 35
    title: "Bước 2: Kéo giãn theo khoảng cách"
    text: Nhập cự ly muốn kéo dài thêm (+40mm). Phần thân bên trái hoàn toàn giữ nguyên vị trí.
    quiz: q-ac-03-08-2
```

## Cách dùng từng bước

1. **Kéo giãn hình học bằng STRETCH:**
   - Gõ `STRETCH` hoặc phím tắt `S` rồi nhấn [Enter].
   - **Bắt buộc:** Nhấp chuột một điểm bên phải, rê chuột sang trái để mở khung chữ nhật màu xanh lá viền nét đứt (Crossing Selection).
   - Bao quanh các đỉnh mút mà bạn muốn kéo dời đi, sau đó nhấp chuột lần hai để xác nhận chọn.
   - Nhấn [Enter] để kết thúc bước chọn đối tượng.
   - Chọn điểm chuẩn (Specify base point): Nhấp vào một điểm bất kỳ trên màn hình.
   - Bật [F8] (Ortho), kéo chuột theo hướng muốn kéo dài (sang phải/trái/lên/xuống), gõ cự ly muốn kéo giãn thêm (ví dụ `50`) rồi nhấn [Enter].
2. **Kéo dài chính xác bằng LENGTHEN:**
   - Gõ `LENGTHEN` hoặc phím tắt `LEN` rồi nhấn [Enter].
   - Chọn tuỳ chọn:
     - Gõ `DE` (Delta): Nhập độ dài muốn nối dài thêm (ví dụ `25`) rồi nhấp vào đầu mút đoạn thẳng. Đoạn thẳng sẽ dài thêm đúng 25mm.
     - Gõ `T` (Total): Nhập tổng chiều dài mới mong muốn (ví dụ `120`) rồi nhấp vào đoạn thẳng. Đoạn thẳng tự động co hoặc giãn thành đúng 120mm.
     - Gõ `P` (Percent): Nhập tỷ lệ phần trăm (ví dụ `150` để tăng lên 1.5 lần).

## Tuỳ chọn và mẹo

> [!TIP]
> Nếu bạn vô tình dùng khung Window (Trái sang Phải) bao trọn toàn bộ vật thể trong lệnh STRETCH, toàn bộ vật thể sẽ bị di chuyển (MOVE) thay vì bị kéo giãn! Hãy luôn nhớ: Chỉ bao quanh một phần các đỉnh cần kéo.

> [!TIP]
> Các đường kích thước (Dimension) đi kèm chi tiết sẽ tự động cập nhật số đo mới theo chiều dài sau khi bạn dùng lệnh STRETCH mà không cần phải ghi lại kích thước.

## Tự kiểm tra

```quiz
id: q-ac-03-08-1
type: single
question: Khi thực hiện lệnh STRETCH để kéo dài một chi tiết hình học, bạn bắt buộc phải dùng phương pháp chọn đối tượng nào?
options:
  - text: Crossing Selection (quét từ Phải sang Trái với khung xanh lá)
    correct: true
    why: STRETCH bắt buộc phải dùng Crossing để phân biệt đỉnh cần di chuyển và cạnh cần kéo giãn
  - text: Window Selection (quét từ Trái sang Phải với khung xanh dương)
    why: Window Selection sẽ biến lệnh STRETCH thành lệnh di chuyển MOVE
  - text: Nhấp chuột trực tiếp từng đoạn
    why: Nhấp trực tiếp từng đoạn không xác định được nhóm đỉnh cần kéo giãn
  - text: Lệnh SELECT ALL (Ctrl + A)
    why: Chọn tất cả sẽ di chuyển toàn bộ bản vẽ
explain: "Quy tắc vàng của lệnh STRETCH là luôn luôn dùng Crossing Window (quét từ Phải sang Trái): đỉnh nào nằm trọn trong khung sẽ bị tịnh tiến, cạnh nào bị khung cắt ngang qua sẽ bị kéo giãn dài ra."
tags: [stretch, crossing, quy-tac]
```

```quiz
id: q-ac-03-08-2
type: single
question: Trong lệnh LENGTHEN, tuỳ chọn "Delta" (gõ chữ DE) có chức năng gì?
options:
  - text: Kéo dài thêm hoặc thu ngắn bớt một khoảng khoảng cách xác định
    correct: true
    why: Delta biểu thị sự gia tăng hoặc giảm bớt độ dài
  - text: Đặt tổng chiều dài mới cho đoạn thẳng
    why: Đặt tổng chiều dài là tuỳ chọn Total
  - text: Thay đổi chiều dài theo phần trăm
    why: Thay đổi theo phần trăm là tuỳ chọn Percent
  - text: Đổi màu sắc đoạn thẳng
    why: LENGTHEN không thay đổi màu sắc
explain: "Tuỳ chọn Delta trong lệnh LENGTHEN cho phép bạn cộng thêm một lượng chiều dài dương (kéo dài thêm) hoặc nhập giá trị âm (thu ngắn bớt) cho đoạn thẳng."
tags: [lengthen, delta]
```

```quiz
id: q-ac-03-08-3
type: truefalse
question: Nếu khung chọn trong lệnh STRETCH bao trọn toàn bộ 100% tất cả các đỉnh của đối tượng, đối tượng sẽ bị di chuyển (Move) thay vì kéo giãn.
answer: true
explain: "Khi toàn bộ các đỉnh của đối tượng đều nằm trọn bên trong khung chọn, không có cạnh nào bị kéo giãn mà toàn bộ đối tượng sẽ bị dời sang vị trí mới như lệnh MOVE."
tags: [stretch, nguyen-ly]
```

```quiz
id: q-ac-03-08-4
type: hotspot
question: Bấm vào vị trí khung chọn Crossing Selection màu xanh lá trên hình minh hoạ.
use: hotspots
answer: stretch-crossing-box
explain: "Khung chọn Crossing nằm ở nửa bên trái của sơ đồ, có viền nét đứt màu xanh lá bao quanh các đỉnh cần kéo giãn."
tags: [stretch, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Dùng lệnh STRETCH nhưng cả hình vẽ bị bay đi nguyên khối chứ không chịu giãn dài ra.
  - *Nguyên nhân:* Quét khung chọn bao trọn toàn bộ hình, hoặc quét từ Trái sang Phải (Window) thay vì Phải sang Trái (Crossing).
  - *Cách sửa:* Quét từ Phải sang Trái và chỉ bao phủ một nửa phía đầu cần kéo dài của hình.
- **Triệu chứng:** Đường tròn không thể kéo giãn thành hình elip bằng lệnh STRETCH.
  - *Nguyên nhân:* STRETCH chỉ tác dụng lên các đỉnh hình học (vertices) của đoạn thẳng, đa tuyến. Đường tròn không có đỉnh nên sẽ bị di chuyển tâm.
  - *Cách sửa:* Nếu muốn đổi đường kính hình tròn, hãy dùng lệnh SCALE hoặc chỉnh bán kính trong Properties.

## Bài tập thực hành

- [ ] Gõ `RECTANG` vẽ một hình chữ nhật kích thước `@120,60`. <!-- expect: RECTANG -->
- [ ] Gõ `STRETCH` (phím tắt `S`). <!-- expect: STRETCH -->
- [ ] Quét khung Crossing (từ phải sang trái) bao phủ 2 góc bên phải của hình chữ nhật.
- [ ] Nhấn [Enter], chọn Base Point bất kỳ, bật [F8], kéo sang phải và nhập khoảng cách `40` để kéo dài hình thành 160×60mm.
- [ ] Gõ `LINE` vẽ một đoạn thẳng dài 100mm. <!-- expect: LINE -->
- [ ] Gõ `LENGTHEN`, gõ `DE` (Delta), nhập số `30` rồi nhấp vào đầu mút đoạn thẳng để kéo dài thêm 30mm. <!-- expect: LENGTHEN -->

## Nguồn tham khảo

```links
- title: Lệnh STRETCH kéo giãn hình học (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=STRETCH+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về quy tắc Crossing Selection và kéo giãn đa tuyến
- title: Lệnh LENGTHEN điều chỉnh độ dài (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=LENGTHEN+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn Delta, Percent, Total, Dynamic của lệnh LENGTHEN
```
