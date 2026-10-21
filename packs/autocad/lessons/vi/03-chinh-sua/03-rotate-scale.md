---
id: ac-03-03
title: Xoay với ROTATE và thu phóng với SCALE
category: Chỉnh sửa
tags: [rotate, scale, xoay, thu-phong, reference, copy]
level: beginner
minutes: 15
needs: [ac-03-02]
appVersions: ['2024', '2025']
edition: all
---
# Xoay với ROTATE và thu phóng với SCALE

> **Mục tiêu:**
> - Sử dụng lệnh ROTATE để xoay đối tượng quanh một điểm tâm theo góc chính xác hoặc góc tham chiếu (Reference).
> - Sử dụng lệnh SCALE để phóng to, thu nhỏ đối tượng theo tỷ lệ đồng dạng (Scale Factor).
> - Áp dụng tuỳ chọn Copy trong lệnh Rotate và Scale để giữ lại hình gốc sau khi biến hình.

## Lệnh này làm gì và khi nào dùng

Hai phép biến hình hình học cơ bản tiếp theo là phép quay và phép vị tự đồng dạng:
- `ROTATE` (phím tắt `RO`): Xoay đối tượng quanh một [[Điểm chuẩn]] (Base Point) làm tâm quay theo một góc xác định.
- `SCALE` (phím tắt `SC`): Phóng to hoặc thu nhỏ kích thước của đối tượng theo một tỷ lệ đồng dạng (hệ số vị tự) tính từ điểm gốc.

Cả hai lệnh này đều sở hữu một vũ khí cực mạnh là tuỳ chọn **Reference (Tham chiếu - gõ chữ R)**. Khi bạn không biết chính xác góc quay hiện tại hay tỷ lệ phóng to là bao nhiêu phần trăm mà chỉ biết kích thước thực tế cần đạt được (ví dụ muốn kéo một cạnh bất kỳ thành đúng 100mm), tuỳ chọn Reference sẽ tự động tính toán cho bạn.

## Cách dùng từng bước

1. **Xoay đối tượng theo góc (ROTATE):**
   - Gõ `ROTATE` hoặc `RO` rồi nhấn [Enter].
   - Nhấp chọn các đối tượng cần xoay rồi nhấn [Enter].
   - Chọn điểm tâm xoay (Specify base point): Nhấp vào điểm bạn muốn làm trục giữ cố định.
   - Nhập góc xoay (Specify rotation angle):
     - Nhập số dương (ví dụ `45`): Xoay ngược chiều kim đồng hồ.
     - Nhập số âm (ví dụ `-30`): Xoay cùng chiều kim đồng hồ.
2. **Xoay giữ lại hình gốc (Rotate Copy):**
   - Đang trong lệnh Rotate sau khi chọn Base Point, gõ chữ `C` (Copy) rồi [Enter].
   - Nhập góc xoay: Vật thể gốc sẽ đứng yên và một bản sao xoay sẽ được tạo ra.
3. **Phóng to thu nhỏ theo tỷ lệ (SCALE):**
   - Gõ `SCALE` hoặc `SC` rồi nhấn [Enter].
   - Chọn đối tượng cần thu phóng rồi nhấn [Enter].
   - Chọn điểm gốc phóng (Base point).
   - Nhập hệ số tỷ lệ (Scale factor):
     - Nhập `2`: Phóng to gấp đôi (200%).
     - Nhập `0.5`: Thu nhỏ một nửa (50%).
4. **Phóng to đối tượng về kích thước mong muốn (Scale Reference):**
   - Gõ `SC` [Enter], chọn hình, chọn Base Point.
   - Gõ chữ `R` (Reference) rồi [Enter].
   - Bấm 2 điểm mút của cạnh hiện tại (chiều dài cũ).
   - Gõ chiều dài mới mong muốn (ví dụ `150`) rồi nhấn [Enter]. Toàn bộ hình sẽ tự động co giãn sao cho cạnh đó dài đúng 150mm!

## Tuỳ chọn và mẹo

> [!TIP]
> Tuỳ chọn `Reference` trong lệnh SCALE là cứu cánh số 1 khi bạn chèn ảnh mặt bằng hoặc file PDF vào AutoCAD và cần căn chỉnh (calibrate) tỷ lệ của ảnh khớp 100% với kích thước thật.

> [!TIP]
> Luôn nhớ quy tắc góc quay chuẩn: Góc dương quay ngược chiều kim đồng hồ, góc âm quay cùng chiều kim đồng hồ.

## Tự kiểm tra

```quiz
id: q-ac-03-03-1
type: single
question: Khi xoay đối tượng bằng lệnh ROTATE, nếu bạn nhập giá trị góc là 45 độ (số dương), đối tượng sẽ quay theo chiều nào?
options:
  - text: Ngược chiều kim đồng hồ (Counter-Clockwise)
    correct: true
    why: Quy ước chuẩn của AutoCAD là góc dương quay ngược chiều kim đồng hồ
  - text: Cùng chiều kim đồng hồ (Clockwise)
    why: Muốn cùng chiều kim đồng hồ phải nhập góc âm (-45)
  - text: Quay ngẫu nhiên tuỳ vị trí con trỏ chuột
    why: Chiều quay tuân theo quy tắc góc toán học
  - text: Đối tượng bị lật ngược đối xứng
    why: Lật đối xứng là chức năng của lệnh MIRROR
explain: "Trong AutoCAD, quy ước chiều quay góc dương luôn là chiều ngược chiều kim đồng hồ (Counter-Clockwise)."
tags: [rotate, goc-quay]
```

```quiz
id: q-ac-03-03-2
type: single
question: Để thu nhỏ kích thước của một chi tiết cơ khí đi một nửa (còn 50%), bạn nhập hệ số Scale factor bằng bao nhiêu trong lệnh SCALE?
options:
  - text: "0.5"
    correct: true
    why: Hệ số 0.5 tương ứng với 50% kích thước gốc
  - text: "-2"
    why: Hệ số Scale phải là số dương lớn hơn 0
  - text: "2"
    why: Hệ số 2 là phóng to gấp đôi
  - text: "50"
    why: Nhập 50 sẽ phóng to đối tượng lên 50 lần
explain: "Lệnh SCALE nhận hệ số tỷ lệ đồng dạng dạng số thập phân: nhỏ hơn 1 là thu nhỏ (0.5 là còn một nửa), lớn hơn 1 là phóng to."
tags: [scale, he-so]
```

```quiz
id: q-ac-03-03-3
type: truefalse
question: Tuỳ chọn Reference (gõ R) trong lệnh SCALE cho phép bạn phóng to thu nhỏ hình vẽ về một kích thước chiều dài xác định mà không cần tự tính toán tỷ lệ phần trăm.
answer: true
explain: "Tuỳ chọn Reference cho phép bạn chỉ định chiều dài hiện tại và chiều dài mới mong muốn, AutoCAD sẽ tự động tính toán hệ số tỷ lệ co giãn cho toàn bộ hình."
tags: [scale, reference]
```

## Lỗi thường gặp

- **Triệu chứng:** Nhập hệ số Scale âm (ví dụ `-2`) để mong muốn lật ngược hình.
  - *Nguyên nhân:* Lệnh SCALE không chấp nhận giá trị âm (*"Value must be positive and nonzero"*).
  - *Cách sửa:* Nếu muốn lật ngược hình học, hãy dùng lệnh `MIRROR` thay vì lệnh SCALE.
- **Triệu chứng:** Đối tượng sau khi xoá bị bay lệch ra xa khỏi vị trí mong muốn.
  - *Nguyên nhân:* Chọn điểm tâm xoay (Base Point) nằm quá xa đối tượng.
  - *Cách sửa:* Luôn chọn Base Point là tâm hoặc góc của chính đối tượng đó.

## Bài tập thực hành

- [ ] Gõ `RECTANG` vẽ một hình chữ nhật kích thước `@100,50`. <!-- expect: RECTANG -->
- [ ] Gõ `ROTATE`, chọn hình chữ nhật, chọn Base Point tại góc dưới bên trái. <!-- expect: ROTATE -->
- [ ] Nhập góc `45` rồi nhấn [Enter] để xoay nghiêng 45 độ.
- [ ] Gõ `SCALE`, chọn hình chữ nhật, bắt Base Point tại tâm hình. <!-- expect: SCALE -->
- [ ] Nhập hệ số tỷ lệ `2.0` rồi nhấn [Enter] để phóng to gấp đôi kích thước.

## Nguồn tham khảo

```links
- title: Lệnh ROTATE và xoay góc tham chiếu (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=ROTATE+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về tuỳ chọn Base Point, Copy và Reference của ROTATE
- title: Lệnh SCALE và tỷ lệ đồng dạng (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=SCALE+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn phóng to thu nhỏ và căn chỉnh kích thước với Reference
```
