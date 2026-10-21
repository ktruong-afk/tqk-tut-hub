---
id: ac-02-08
title: Đối tượng điểm POINT và chia đoạn với DIVIDE, MEASURE
category: Vẽ 2D
tags: [point, divide, measure, ptype, chia-doan]
level: beginner
minutes: 15
needs: [ac-02-01]
appVersions: ['2024', '2025']
edition: all
---
# Đối tượng điểm POINT và chia đoạn với DIVIDE, MEASURE

> **Mục tiêu:**
> - Tạo và thay đổi kiểu hiển thị đối tượng điểm (Point Style) bằng lệnh PTYPE.
> - Sử dụng lệnh DIVIDE để chia một đối tượng hình học thành N phần bằng nhau.
> - Sử dụng lệnh MEASURE để rải các điểm đánh dấu theo một cự ly khoảng cách cố định.

## Lệnh này làm gì và khi nào dùng

Đối tượng Điểm (Point) là thực thể hình học nhỏ nhất trong AutoCAD, chỉ gồm một toạ độ duy nhất (X, Y, Z). Điểm đóng vai trò cực kỳ quan trọng làm mốc toạ độ, cắm cọc tim đường hoặc đánh dấu vị trí khoan lỗ bu lông.

Mặc định, đối tượng Point chỉ là một dấu chấm pixel đơn lẻ rất khó nhìn thấy trên màn hình. Lệnh `PTYPE` cho phép bạn đổi điểm thành hình chữ thập, dấu nhân hoặc hình tròn có dấu X to rõ.

Hai lệnh ứng dụng điểm mạnh nhất trong kỹ thuật:
- `DIVIDE` (phím tắt `DIV`): Chia đều một đoạn thẳng, cung tròn hay đường cong thành **N phần bằng nhau**.
- `MEASURE` (phím tắt `ME`): Rải các điểm đánh dấu dọc theo đối tượng với **khoảng cách cố định L** (ví dụ cắm cọc tiêu cách nhau đều đặn 20 mét).

Cần lưu ý: Cả DIVIDE và MEASURE đều **không cắt rời** đường thẳng của bạn ra, chúng chỉ đặt các đối tượng Point lên trên thân đường thẳng để bạn bắt điểm (chế độ Osnap Node).

## Cách dùng từng bước

1. **Đổi kiểu hiển thị điểm dễ nhìn (PTYPE):**
   - Gõ lệnh `PTYPE` (hoặc `DDPTYPE`) rồi nhấn [Enter]. Hộp thoại *Point Style* hiện ra.
   - Chọn một biểu tượng dễ nhìn (ví dụ hình tròn lồng dấu X).
   - Đặt kích thước *Point Size* thành `5%` (*Set Size Relative to Screen*) rồi bấm **OK**.
2. **Chấm điểm đơn lẻ (POINT):**
   - Gõ `POINT` hoặc phím tắt `PO` rồi nhấn [Enter].
   - Nhấp chuột lên màn hình để tạo điểm mốc toạ độ.
3. **Chia đều thành N phần bằng nhau (DIVIDE):**
   - Vẽ một đoạn thẳng dài bằng lệnh `LINE`.
   - Gõ `DIVIDE` hoặc `DIV` rồi nhấn [Enter].
   - Nhấp chọn đoạn thẳng vừa vẽ.
   - Nhập số phần muốn chia đều (ví dụ `5`) rồi nhấn [Enter]. Các điểm Point sẽ lập tức xuất hiện chia đều đoạn thẳng làm 5 phần.
4. **Chia theo khoảng cách bước cố định (MEASURE):**
   - Gõ `MEASURE` hoặc `ME` rồi nhấn [Enter].
   - Nhấp chọn đối tượng tại đầu bạn muốn làm mốc xuất phát.
   - Nhập độ dài khoảng cách mỗi bước (ví dụ `30`) rồi nhấn [Enter].
5. **Bắt điểm vào các điểm vừa tạo:**
   - Bật chế độ bắt điểm `Node` trong Osnap ([F3]) để bắt dính chính xác vào tâm của các điểm Point.

## Tuỳ chọn và mẹo

> [!TIP]
> Luôn bật chế độ *Set Size Relative to Screen* trong hộp thoại `PTYPE`. Kích thước điểm sẽ tự động phóng to thu nhỏ vừa tầm mắt (5% màn hình) mỗi khi bạn Zoom và gõ lệnh `REGEN`.

> [!TIP]
> Cả lệnh DIVIDE và MEASURE đều có tuỳ chọn chèn khối (Block) thay vì chèn điểm Point. Bạn có thể tự động rải một hàng cây, cột đèn hay ghế ngồi dọc theo tim đường chỉ bằng 1 lệnh.

## Tự kiểm tra

```quiz
id: q-ac-02-08-1
type: single
question: Điểm khác biệt mấu chốt giữa lệnh DIVIDE và lệnh MEASURE là gì?
options:
  - text: DIVIDE chia theo số phần bằng nhau, MEASURE chia theo chiều dài khoảng cách cố định
    correct: true
    why: DIVIDE nhận số đoạn chia, MEASURE nhận chiều dài bước nhảy
  - text: DIVIDE cắt đứt đoạn thẳng, MEASURE không cắt
    why: Cả hai lệnh đều không cắt đứt đối tượng gốc
  - text: DIVIDE chỉ dùng cho hình tròn, MEASURE chỉ dùng cho đường thẳng
    why: Cả hai đều dùng được cho đường thẳng, cung tròn, polyline, spline
  - text: MEASURE chỉ dùng để đo khoảng cách hiển thị ra màn hình
    why: Đo khoảng cách dùng lệnh DIST
explain: "Lệnh DIVIDE chia đối tượng thành số lượng phần bằng nhau (N phần), còn lệnh MEASURE chia đối tượng theo một cự ly độ dài cố định tính từ đầu mốc."
tags: [divide, measure, so-sanh]
```

```quiz
id: q-ac-02-08-2
type: single
question: Để bắt điểm chuẩn xác vào tâm của đối tượng điểm (Point) đã tạo bởi DIVIDE, bạn cần bật chế độ bắt điểm nào trong Osnap?
options:
  - text: Node
    correct: true
    why: Node là chế độ Osnap chuyên dụng để bắt vào đối tượng Point
  - text: Endpoint
    why: Endpoint chỉ bắt mút của đường thẳng hoặc cung
  - text: Midpoint
    why: Midpoint bắt trung điểm
  - text: Intersection
    why: Intersection bắt giao điểm
explain: "Trong hệ thống bắt điểm Object Snap của AutoCAD, chế độ Node được dùng để bắt dính chính xác vào các đối tượng điểm (Point) và điểm định vị văn bản."
tags: [osnap, node, point]
```

```quiz
id: q-ac-02-08-3
type: truefalse
question: Khi thực hiện lệnh DIVIDE chia một đoạn thẳng làm 4 phần, đoạn thẳng ban đầu sẽ bị chặt đứt thành 4 đoạn rời nhau.
answer: false
explain: "Lệnh DIVIDE hoàn toàn không cắt rời đoạn thẳng gốc, nó chỉ thả các đối tượng Point nằm dọc theo đường thẳng để đánh dấu mốc toạ độ."
tags: [divide, point]
```

## Lỗi thường gặp

- **Triệu chứng:** Chạy xong lệnh DIVIDE nhưng nhìn trên màn hình không thấy có gì thay đổi.
  - *Nguyên nhân:* Điểm Point đang ở kiểu mặc định (dấu chấm 1 pixel) trùng khít lên nét vẽ nên mắt người không nhìn thấy được.
  - *Cách sửa:* Gõ lệnh `PTYPE`, chọn biểu tượng hình tròn có dấu X và chỉnh Size thành `5%`, sau đó gõ lệnh `REGEN` để điểm hiện rõ.
- **Triệu chứng:** Dùng lệnh DIVIDE xong nhưng không rê chuột bắt điểm vào các mốc chia được.
  - *Nguyên nhân:* Chưa kích hoạt chế độ bắt điểm *Node* trong hộp thoại Drafting Settings.
  - *Cách sửa:* Gõ lệnh `OSNAP` và tích chọn vào ô *Node*.

## Bài tập thực hành

- [ ] Gõ `PTYPE` mở hộp thoại Point Style, chọn kiểu dấu X tròn và đặt kích thước là 5% màn hình. <!-- expect: PTYPE -->
- [ ] Gõ `LINE` vẽ một đoạn thẳng nằm ngang dài đúng `200`mm. <!-- expect: LINE -->
- [ ] Gõ `DIVIDE`, chọn đoạn thẳng vừa vẽ và nhập số đoạn chia là `5`. <!-- expect: DIVIDE -->
- [ ] Bật Osnap [F3] với chế độ Node, gõ `LINE` và vẽ các vách đứng từ các điểm mốc Node vừa chia. <!-- expect: LINE -->
- [ ] Gõ `MEASURE`, chọn đoạn thẳng ban đầu và thử rải các điểm cách nhau mỗi bước `45`mm. <!-- expect: MEASURE -->

## Nguồn tham khảo

```links
- title: Lệnh DIVIDE và ứng dụng chia đoạn (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=DIVIDE+Command
  kind: official
  lang: en
  note: Hướng dẫn phân chia đối tượng hình học thành các phần đều nhau
- title: Lệnh MEASURE và tuỳ chọn chèn Block (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=MEASURE+Command
  kind: official
  lang: en
  note: Rải điểm và khối thư viện theo khoảng cách cố định trong AutoCAD
```
