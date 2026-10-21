---
id: ac-03-06
title: Bo tròn góc với FILLET và vát mép với CHAMFER
category: Chỉnh sửa
tags: [fillet, chamfer, bo-goc, vat-mep, radius, chinh-sua]
level: beginner
minutes: 15
needs: [ac-03-05]
appVersions: ['2024', '2025']
edition: all
---
# Bo tròn góc với FILLET và vát mép với CHAMFER

> **Mục tiêu:**
> - Sử dụng lệnh FILLET để bo tròn góc giữa hai đường thẳng bằng một cung tròn có bán kính xác định.
> - Sử dụng lệnh CHAMFER để vát mép góc phẳng theo cự ly khoảng cách hoặc góc vát nghiêng.
> - Áp dụng mẹo đặc biệt Fillet với bán kính R=0 để nối góc vuông nhọn sạch sẽ tức thì.

## Lệnh này làm gì và khi nào dùng

Trong gia công cơ khí và chế tạo máy, hầu như không có chi tiết kim loại nào được phép để lại góc sắc nhọn vì sẽ gây nguy hiểm cho người vận hành và tạo ra điểm tập trung ứng suất dễ gây nứt gãy. Hai thao tác gia công mép cạnh chuẩn mực là:
- `FILLET` (phím tắt `F`): [[Bo tròn góc]] chuyển tiếp giữa hai đối tượng bằng một [[Cung tròn]] mượt mà có bán kính R xác định.
- `CHAMFER` (phím tắt `CHA`): [[Vát mép]] phẳng góc nhọn theo hai khoảng cách vát (Distance 1, Distance 2) hoặc theo một cự ly và một góc nghiêng (Angle, ví dụ vát 2×45°).

Ngoài công năng cơ khí, lệnh FILLET còn là công cụ nối hai đường thẳng giao nhau sạch sẽ nhất trong kiến trúc khi đặt bán kính R=0.

## Cách dùng từng bước

1. **Bo tròn góc bằng FILLET:**
   - Gõ `FILLET` hoặc phím tắt `F` rồi nhấn [Enter].
   - Đặt bán kính bo tròn: Gõ chữ `R` (Radius) rồi [Enter].
   - Nhập giá trị bán kính (ví dụ `15`) rồi nhấn [Enter].
   - Nhấp chọn đường thẳng thứ nhất.
   - Nhấp chọn đường thẳng thứ hai: Một cung tròn bán kính R=15 sẽ tự động được tạo ra kết nối mượt hai cạnh và xén sạch phần thừa.
2. **Mẹo nối góc vuông nhọn với Fillet R=0:**
   - Gõ `F` [Enter], gõ `R` [Enter] rồi nhập số `0` [Enter].
   - Nhấp chọn hai đường thẳng đang bị hở hoặc bị đan chéo thừa thãi: Hai đường sẽ tự động kéo dài hoặc xén ngắn để gặp nhau tại một góc vuông nhọn hoàn hảo 100%!
3. **Vát mép góc phẳng bằng CHAMFER:**
   - Gõ `CHAMFER` hoặc phím tắt `CHA` rồi nhấn [Enter].
   - Đặt khoảng cách vát: Gõ chữ `D` (Distance) rồi [Enter].
   - Nhập khoảng cách vát thứ nhất (First chamfer distance, ví dụ `10`) rồi [Enter].
   - Nhập khoảng cách vát thứ hai (Second chamfer distance, ví dụ `10`) rồi [Enter].
   - Nhấp chọn cạnh thứ nhất, sau đó nhấp chọn cạnh thứ hai.
4. **Bo tròn hoặc vát mép toàn bộ Polyline:**
   - Đang trong lệnh FILLET hoặc CHAMFER, gõ chữ `P` (Polyline).
   - Nhấp chọn một hình chữ nhật hoặc đường Polyline: Toàn bộ tất cả các góc của hình sẽ được bo tròn hoặc vát phẳng đồng loạt chỉ bằng 1 cú nhấp!

## Tuỳ chọn và mẹo

> [!TIP]
> Bạn có thể bo tròn giữa hai đoạn thẳng song song bằng lệnh FILLET: AutoCAD sẽ tự động tạo một cung bán nguyệt khép kín nối tròn hai đầu mút của hai đường song song đó mà không cần đo khoảng cách.

> [!TIP]
> Đè giữ phím [Shift] khi chọn cạnh trong lệnh FILLET sẽ tạm thời ép bán kính về R=0 để nối nhọn góc ngay lập tức mà không làm mất bán kính R bạn đã cài đặt trước đó.

## Tự kiểm tra

```quiz
id: q-ac-03-06-1
type: single
question: Khi thực hiện lệnh FILLET với giá trị bán kính Radius đặt bằng 0 (R=0), kết quả tạo ra giữa hai đường thẳng giao nhau là gì?
options:
  - text: Hai đường thẳng sẽ nối liền góc nhọn chuẩn xác và xén sạch phần thừa
    correct: true
    why: Bán kính R=0 biến cung tròn thành điểm góc nhọn hoàn hảo
  - text: AutoCAD báo lỗi không cho thực hiện
    why: R=0 là tính năng được hỗ trợ chính thức và rất phổ biến
  - text: Hai đường thẳng bị xoá bỏ hoàn toàn
    why: FILLET không xoá đối tượng
  - text: Một cung tròn bán kính vô cùng lớn
    why: R=0 không tạo cung tròn mà tạo góc nhọn
explain: "Mẹo Fillet với R=0 là tuyệt chiêu kinh điển của người dùng AutoCAD chuyên nghiệp để nối liền hoặc xén gọn hai đường thẳng thành một góc nhọn sạch sẽ chỉ bằng một lệnh."
tags: [fillet, radius, meo]
```

```quiz
id: q-ac-03-06-2
type: single
question: Để bo tròn đồng loạt tất cả các góc của một hình chữ nhật chỉ bằng một cú nhấp chuột, bạn chọn tuỳ chọn nào trong lệnh FILLET?
options:
  - text: Polyline (gõ chữ P)
    correct: true
    why: Tuỳ chọn Polyline tự động áp dụng bán kính bo cho mọi đỉnh của đường đa tuyến
  - text: Multiple (gõ chữ M)
    why: Multiple chỉ cho phép nhấp nhiều lần không cần thoát lệnh
  - text: Radius (gõ chữ R)
    why: Radius dùng để cài đặt bán kính
  - text: Trim (gõ chữ T)
    why: Trim quy định có xén góc hay giữ góc
explain: "Khi gõ chữ P (Polyline) trong lệnh FILLET, AutoCAD sẽ áp dụng bán kính R lên toàn bộ các góc của đối tượng Polyline được chọn."
tags: [fillet, polyline]
```

```quiz
id: q-ac-03-06-3
type: truefalse
question: Lệnh FILLET có thể dùng để tạo cung tròn nửa vòng nối giữa hai đoạn thẳng nằm song song với nhau.
answer: true
explain: "Khi nhấp chọn hai đường thẳng song song, lệnh FILLET sẽ tự động tạo một cung tròn đường kính đúng bằng khoảng cách giữa hai đường đó nối mượt hai đầu mút."
tags: [fillet, song-song]
```

## Lỗi thường gặp

- **Triệu chứng:** Gõ lệnh FILLET và chọn hai cạnh nhưng AutoCAD báo lỗi *"Radius is too large"*.
  - *Nguyên nhân:* Bán kính R nhập vào quá lớn so với chiều dài của đoạn thẳng, không đủ không gian hình học để đặt cung tròn.
  - *Cách sửa:* Gõ `R` trong lệnh FILLET và giảm giá trị bán kính nhỏ hơn chiều dài của cạnh ngắn nhất.
- **Triệu chứng:** Bo tròn góc xong thì hai đường thẳng ban đầu bị xén mất cả đoạn thân.
  - *Nguyên nhân:* Tuỳ chọn *Trim Mode* trong lệnh Fillet đang bị chỉnh sai.
  - *Cách sửa:* Trong lệnh FILLET, gõ `T` (Trim) và chọn chế độ `Trim` chuẩn.

## Bài tập thực hành

- [ ] Gõ `LINE` vẽ hai đoạn thẳng vuông góc giao nhau tạo thành góc nhọn 90 độ. <!-- expect: LINE -->
- [ ] Gõ `FILLET`, gõ `R` và nhập bán kính `20`. <!-- expect: FILLET -->
- [ ] Nhấp chọn lần lượt hai đoạn thẳng để bo tròn góc với cung tròn R20.
- [ ] Gõ `LINE` vẽ hai đoạn thẳng xiên đan chéo thừa thãi qua nhau. <!-- expect: LINE -->
- [ ] Gõ `FILLET`, gõ `R` nhập `0` rồi nhấp chọn hai đoạn thẳng để xén gọn thành góc nhọn. <!-- expect: FILLET -->
- [ ] Gõ `CHAMFER`, gõ `D` nhập khoảng cách vát `15` cho cả hai cạnh rồi vát một góc thử nghiệm. <!-- expect: CHAMFER -->

## Nguồn tham khảo

```links
- title: Lệnh FILLET bo tròn góc cạnh (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=FILLET+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về tuỳ chọn Radius, Polyline, Trim, Multiple của FILLET
- title: Lệnh CHAMFER vát mép kỹ thuật (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=CHAMFER+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn Distance, Angle, Method của lệnh vát mép CHAMFER
```
