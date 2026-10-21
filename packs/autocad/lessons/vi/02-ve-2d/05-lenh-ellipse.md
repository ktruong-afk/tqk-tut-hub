---
id: ac-02-05
title: Vẽ hình elip và cung elip với lệnh ELLIPSE
category: Vẽ 2D
tags: [ellipse, ve-2d, hinh-elip, truc-lon, truc-nho]
level: beginner
minutes: 15
needs: [ac-02-02]
appVersions: ['2024', '2025']
edition: all
---
# Vẽ hình elip và cung elip với lệnh ELLIPSE

> **Mục tiêu:**
> - Sử dụng lệnh ELLIPSE để vẽ hình elip theo tâm và các bán trục (Center) hoặc theo trục và khoảng cách (Axis, End).
> - Tạo cung elip mở (Elliptical Arc) với góc bắt đầu và góc kết thúc xác định.
> - Phân biệt giữa elip thực thể toán học chính xác và elip xấp xỉ bằng đường đa tuyến (PELLIPSE).

## Lệnh này làm gì và khi nào dùng

Lệnh `ELLIPSE` (phím tắt `EL`) dùng để tạo đối tượng [[Hình elip]] khép kín hoặc cung elip mở. Trong bản vẽ kỹ thuật, elip là hình chiếu của đường tròn khi nhìn nghiêng một góc (hình chiếu trục đo isometric, miệng bồn chứa nghiêng, lỗ xiên trên mặt phẳng nghiêng cơ khí).

Một hình elip hoàn chỉnh được xác định bởi hai trục đối xứng vuông góc nhau: **Trục lớn (Major axis)** và **Trục nhỏ (Minor axis)**. AutoCAD hỗ trợ hai cách dựng chính:
- **Axis, End:** Xác định chiều dài toàn bộ trục thứ nhất qua hai điểm mút, sau đó nhập bán trục thứ hai.
- **Center:** Xác định tâm elip, sau đó nhập bán trục thứ nhất và bán trục thứ hai.

## Cách dùng từng bước

1. **Vẽ theo Trục và Khoảng cách (Axis, End - Mặc định):**
   - Gõ lệnh `ELLIPSE` hoặc phím tắt `EL` rồi nhấn [Enter].
   - Nhấp chọn điểm mút thứ nhất của trục (First axis endpoint).
   - Bật [F8] (Ortho), kéo ngang và nhập chiều dài trục thứ nhất (ví dụ `140`) rồi nhấn [Enter].
   - Di chuyển chuột lên trên và nhập độ dài bán trục thứ hai (ví dụ `40`) rồi nhấn [Enter].
2. **Vẽ theo Tâm và Bán trục (Center):**
   - Gõ `EL` rồi nhấn [Enter].
   - Gõ chữ `C` (Center) rồi bấm chọn điểm tâm của elip.
   - Nhập độ dài bán trục lớn (ví dụ `60`) rồi nhấn [Enter].
   - Nhập độ dài bán trục nhỏ (ví dụ `30`) rồi nhấn [Enter].
3. **Vẽ cung elip mở (Elliptical Arc):**
   - Gõ `EL` [Enter], gõ chữ `A` (Arc) rồi [Enter].
   - Xác định trục elip tương tự như trên.
   - Nhập góc bắt đầu (Start angle, ví dụ `0`) rồi [Enter].
   - Nhập góc kết thúc (End angle, ví dụ `180` hoặc `270`) rồi [Enter].

## Tuỳ chọn và mẹo

> [!TIP]
> Khi nhập thông số trục thứ hai trong lệnh ELLIPSE, giá trị bạn nhập luôn là **bán trục** (khoảng cách từ tâm đến cạnh), không phải chiều dài toàn bộ trục.

> [!TIP]
> Biến hệ thống `PELLIPSE`: Mặc định bằng 0 (tạo elip chuẩn toán học dạng spline/ellipse). Nếu đổi thành 1, AutoCAD sẽ tạo elip bằng các đoạn cung tròn Polyline xấp xỉ (hữu ích khi xuất sang một số máy CNC đời cũ).

## Tự kiểm tra

```quiz
id: q-ac-02-05-1
type: single
question: Khi xác định thông số trục thứ hai trong lệnh ELLIPSE, AutoCAD yêu cầu bạn nhập giá trị nào?
options:
  - text: Độ dài bán trục (khoảng cách từ tâm đến đỉnh trục)
    correct: true
    why: Thông số trục thứ hai luôn tính từ tâm ra cạnh (bán trục)
  - text: Toàn bộ chiều dài trục (từ đỉnh này sang đỉnh đối diện)
    why: Trục thứ nhất có thể nhập toàn bộ, nhưng trục thứ hai luôn là bán trục
  - text: Diện tích hình elip
    why: Diện tích không phải thông số đầu vào của lệnh ELLIPSE
  - text: Tỉ số giữa hai trục
    why: AutoCAD nhận giá trị khoảng cách hoặc góc quay
explain: "Trong lệnh ELLIPSE, bước nhập thông số trục thứ hai luôn là Specify distance to other axis (khoảng cách bán trục từ tâm đến biên elip)."
tags: [ellipse, thong-so]
```

```quiz
id: q-ac-02-05-2
type: single
question: Để vẽ một cung elip hở (không khép kín) bằng lệnh ELLIPSE, bạn sử dụng tuỳ chọn nào?
options:
  - text: Arc (gõ chữ A)
    correct: true
    why: Tuỳ chọn Arc cho phép nhập góc bắt đầu và kết thúc để cắt cung elip
  - text: Center (gõ chữ C)
    why: Center dùng để vẽ elip khép kín từ tâm
  - text: Isocircle (gõ chữ I)
    why: Isocircle vẽ đường tròn trục đo
  - text: Rotation (gõ chữ R)
    why: Rotation xoay góc nghiêng của elip
explain: "Tuỳ chọn Arc (gõ A) trong lệnh ELLIPSE cho phép bạn tạo một cung elip mở với các góc giới hạn Start angle và End angle."
tags: [ellipse, arc]
```

```quiz
id: q-ac-02-05-3
type: truefalse
question: Một hình elip có bán trục lớn bằng bán trục nhỏ chính là một đường tròn.
answer: true
explain: "Về mặt hình học, đường tròn là trường hợp đặc biệt của hình elip khi độ dài trục lớn bằng độ dài trục nhỏ (tâm sai e = 0)."
tags: [ellipse, hinh-hoc]
```

## Lỗi thường gặp

- **Triệu chứng:** Elip bị to gấp đôi so với kích thước thiết kế mong muốn theo phương đứng.
  - *Nguyên nhân:* Nhập nhầm toàn bộ chiều cao elip thay vì nhập bán trục (nửa chiều cao).
  - *Cách sửa:* Lấy chiều cao mong muốn chia đôi trước khi nhập giá trị cho trục thứ hai.
- **Triệu chứng:** Không thể thực hiện lệnh bo tròn Fillet hoặc vát mép Chamfer lên đối tượng elip.
  - *Nguyên nhân:* Elip là thực thể cong phi tròn bậc cao (True Ellipse) nên một số lệnh cơ bản không tác dụng trực tiếp được.
  - *Cách sửa:* Cắt tỉa elip bằng lệnh TRIM hoặc chuyển biến `PELLIPSE` về 1 trước khi vẽ nếu cần đối tượng dạng Polyline.

## Bài tập thực hành

- [ ] Gõ `ELLIPSE` và chọn phương thức mặc định (Axis, End). <!-- expect: ELLIPSE -->
- [ ] Bấm điểm thứ nhất tại toạ độ `50,50`.
- [ ] Bật [F8], kéo chuột sang phải và gõ chiều dài `120` rồi nhấn [Enter].
- [ ] Kéo chuột lên trên, gõ bán trục thứ hai là `30` rồi nhấn [Enter] để tạo hình elip 120×60mm.
- [ ] Gõ `ELLIPSE`, gõ tuỳ chọn `C` (Center) và vẽ một elip đồng tâm với bán trục lớn 40mm và bán trục nhỏ 20mm. <!-- expect: ELLIPSE -->

## Nguồn tham khảo

```links
- title: Lệnh ELLIPSE và các tuỳ chọn dựng hình (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=ELLIPSE+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về hình elip, cung elip và đường tròn trục đo Isocircle
- title: Biến hệ thống PELLIPSE trong AutoCAD (Autodesk Support)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=PELLIPSE+System+Variable
  kind: official
  lang: en
  note: Giải thích sự khác nhau giữa True Ellipse và Polyline Ellipse
```
