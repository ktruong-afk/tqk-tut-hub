---
id: ac-03-09
title: Hợp nhất và rã đối tượng với EXPLODE, JOIN và PEDIT
category: Chỉnh sửa
tags: [explode, join, pedit, polyline, ra-khoi, hop-nhat, chinh-sua]
level: beginner
minutes: 15
needs: [ac-03-08]
appVersions: ['2024', '2025']
edition: all
---
# Hợp nhất và rã đối tượng với EXPLODE, JOIN và PEDIT

> **Mục tiêu:**
> - Sử dụng lệnh EXPLODE để phá vỡ các thực thể phức hợp (hình chữ nhật, đa tuyến, mảng, khối) thành các đoạn rời.
> - Sử dụng lệnh JOIN để liên kết các đoạn thẳng và cung tròn tiếp giáp thành một đường Polyline liền khối.
> - Sử dụng lệnh PEDIT để chỉnh sửa nâng cao đường đa tuyến: đổi bề dày nét, làm mịn Fit/Spline và nối gộp.

## Lệnh này làm gì và khi nào dùng

Trong quá trình thiết kế, mối quan hệ giữa các thực thể đơn lẻ (đoạn thẳng Line, cung tròn Arc) và các thực thể phức hợp (đường đa tuyến Polyline, hình chữ nhật Rectangle, mảng Array, khối Block) luôn chuyển đổi qua lại:
- `EXPLODE` (phím tắt `X`): [[Phá vỡ đối tượng]] phức hợp thành các thành phần cấu tạo cơ bản đơn lẻ nhất. Ví dụ: Rã hình chữ nhật thành 4 đoạn Line riêng biệt; rã mảng Array thành từng hình độc lập.
- `JOIN` (phím tắt `J`): [[Nối đối tượng]] các phân đoạn tiếp xúc mút nhau thành một [[Đường đa tuyến]] Polyline duy nhất, khép kín hoặc hở.
- `PEDIT` (phím tắt `PE`): Bộ công cụ chuyên dụng chỉnh sửa đa tuyến (Polyline Edit), cho phép biến đường Line thành Polyline, đổi bề dày nét vẽ cho toàn bộ hình và nắn mịn góc cua.

Bộ ba lệnh này là cầu nối giúp bạn tự do chuyển đổi cấu trúc đối tượng khi cần gia công cắt dây CNC, tính diện tích hoặc phá vỡ bản vẽ đối tác gửi đến.

## Cách dùng từng bước

1. **Phá vỡ đối tượng bằng EXPLODE:**
   - Gõ `EXPLODE` hoặc phím tắt `X` rồi nhấn [Enter].
   - Nhấp chọn đối tượng phức hợp (ví dụ hình chữ nhật hoặc mảng Array).
   - Nhấn [Enter] để xác nhận. Ngay lập tức đối tượng sẽ bị rã thành các đoạn Line/Arc độc lập.
2. **Nối liền đối tượng thành Polyline bằng JOIN:**
   - Đảm bảo các đoạn thẳng/cung tròn có các đầu mút tiếp xúc chạm khít vào nhau (dùng Osnap Endpoint).
   - Gõ `JOIN` hoặc phím tắt `J` rồi nhấn [Enter].
   - Quét chọn toàn bộ các đoạn thẳng cần nối lại với nhau.
   - Nhấn [Enter]. Toàn bộ các đoạn rời rạc sẽ hợp nhất thành một đường Polyline liền khối duy nhất!
3. **Chỉnh sửa đa tuyến chuyên sâu bằng PEDIT:**
   - Gõ `PEDIT` hoặc phím tắt `PE` rồi nhấn [Enter].
   - Nhấp chọn một đoạn thẳng đơn lẻ: AutoCAD hỏi `Do you want to turn it into one? <Y>`. Nhấn [Enter] để đồng ý chuyển nó thành Polyline.
   - Chọn các tuỳ chọn chỉnh sửa:
     - `Join` (gõ `J`): Nối thêm các đoạn khác vào đa tuyến.
     - `Width` (gõ `W`): Nhập bề dày nét mới cho toàn bộ đa tuyến (ví dụ gõ `5`).
     - `Fit` (gõ `F`): Uốn mịn các góc cua của đa tuyến thành đường cong tiếp tuyến mượt mà.
     - `Decurve` (gõ `D`): Huỷ bỏ uốn cong, đưa đa tuyến trở lại dạng gãy góc ban đầu.
     - `Close` (gõ `C`): Tự động nối khép kín đầu và đuôi.

## Tuỳ chọn và mẹo

> [!TIP]
> Lệnh `JOIN` chỉ có thể nối các đối tượng khi đầu mút của chúng chạm nhau chính xác 100%. Nếu hai đầu mút bị hở dù chỉ 0.001mm, lệnh JOIN sẽ thất bại. Hãy dùng Osnap hoặc Fillet R=0 để khép góc trước khi Join.

> [!TIP]
> Trong lệnh PEDIT, bạn có thể gõ tuỳ chọn `M` (Multiple) trước khi chọn đối tượng để chọn đồng loạt hàng trăm đoạn thẳng và chuyển thành Polyline cùng một lúc.

## Tự kiểm tra

```quiz
id: q-ac-03-09-1
type: single
question: Khi bạn vẽ một hình chữ nhật bằng lệnh RECTANG rồi thực hiện lệnh EXPLODE lên nó, kết quả là gì?
options:
  - text: Hình chữ nhật bị tách thành 4 đoạn thẳng (Line) độc lập riêng biệt
    correct: true
    why: EXPLODE phá vỡ đường bao Polyline của hình chữ nhật thành các phân đoạn Line đơn lẻ
  - text: Hình chữ nhật bị xoá khỏi bản vẽ
    why: Xoá là lệnh ERASE
  - text: Hình chữ nhật bị thu nhỏ lại
    why: Thu nhỏ là lệnh SCALE
  - text: Hình chữ nhật biến thành hình tròn
    why: EXPLODE không thay đổi hình dạng hình học
explain: "Lệnh EXPLODE (phím tắt X) phá vỡ tính liên kết liền khối của đường Polyline, đưa hình chữ nhật trở về 4 đoạn thẳng Line đơn lẻ có thể chọn và xoá riêng rẽ."
tags: [explode, rectang, pline]
```

```quiz
id: q-ac-03-09-2
type: single
question: Điều kiện bắt buộc để lệnh JOIN có thể hợp nhất 3 đoạn thẳng thành một đường Polyline duy nhất là gì?
options:
  - text: Các đầu mút của các đoạn thẳng phải chạm khít tiếp xúc vào nhau
    correct: true
    why: JOIN yêu cầu các đối tượng phải liên tục đầu mút với nhau
  - text: Các đoạn thẳng phải có màu sắc hoàn toàn giống nhau
    why: Khác màu vẫn Join được và nhận màu của đối tượng đầu tiên
  - text: Các đoạn thẳng phải nằm song song với nhau
    why: Các đoạn thẳng song song cách nhau không thể nối thành polyline liên tục
  - text: Phải có cùng chiều dài
    why: Chiều dài các đoạn có thể hoàn toàn khác nhau
explain: "Lệnh JOIN chỉ có thể liên kết các đối tượng hình học thành một chuỗi khi các điểm đầu và điểm mút của chúng chạm khít vào nhau không có khe hở."
tags: [join, dieu-kien]
```

```quiz
id: q-ac-03-09-3
type: truefalse
question: Lệnh PEDIT cho phép bạn gán bề dày nét vẽ (Width) đồng nhất cho toàn bộ các cạnh của một đường đa tuyến.
answer: true
explain: "Tuỳ chọn Width (gõ W) trong lệnh PEDIT cho phép bạn đặt chiều rộng nét vẽ đồng loạt cho toàn bộ các phân đoạn của đường Polyline."
tags: [pedit, width]
```

## Lỗi thường gặp

- **Triệu chứng:** Dùng lệnh JOIN quét chọn các đường nhưng dòng lệnh báo *"0 objects converted to polyline"*.
  - *Nguyên nhân:* Giữa các đoạn thẳng có khe hở nhỏ (không chạm nhau) hoặc các đoạn thẳng không nằm trên cùng một mặt phẳng (khác cao độ Z).
  - *Cách sửa:* Bật Osnap Endpoint kiểm tra kỹ các mối nối, hoặc dùng lệnh `FILLET` với bán kính R=0 để khép góc trước khi Join.
- **Triệu chứng:** Lỡ tay bấm EXPLODE lên một khối Block phức tạp có nhiều thuộc tính chữ làm chữ bị biến đổi kỳ lạ.
  - *Nguyên nhân:* Lệnh EXPLODE rã khối Block chứa thuộc tính Attribute khiến các giá trị điền sẵn trở về thẻ gốc ban đầu (Tag).
  - *Cách sửa:* Dùng [Ctrl + Z] ngay lập tức để huỷ lệnh Explode; nếu muốn rã Block giữ nguyên chữ hãy dùng lệnh `BURST` trong bộ Express Tools.

## Bài tập thực hành

- [ ] Gõ `RECTANG` vẽ một hình chữ nhật kích thước `@100,60`. <!-- expect: RECTANG -->
- [ ] Gõ `EXPLODE`, chọn hình chữ nhật và nhấn [Enter]. Nhấp chuột kiểm tra thấy 4 cạnh đã bị tách rời độc lập. <!-- expect: EXPLODE -->
- [ ] Gõ `JOIN`, quét chọn lại cả 4 cạnh vừa rã và nhấn [Enter]. Nhấp chuột kiểm tra thấy hình đã hợp nhất lại thành 1 Polyline liền khối. <!-- expect: JOIN -->
- [ ] Gõ `PEDIT`, nhấp chọn hình Polyline vừa Join. <!-- expect: PEDIT -->
- [ ] Gõ tuỳ chọn `W` (Width), nhập bề dày `4.0` rồi nhấn [Enter] để quan sát nét vẽ dày lên.

## Nguồn tham khảo

```links
- title: Lệnh EXPLODE phá vỡ đối tượng (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=EXPLODE+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về rã khối Block, mảng Array, Polyline và Mesh
- title: Lệnh JOIN và kết nối hình học (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=JOIN+Command
  kind: official
  lang: en
  note: Toàn bộ quy tắc hợp nhất Line, Arc, Polyline, Spline và Helix
```
