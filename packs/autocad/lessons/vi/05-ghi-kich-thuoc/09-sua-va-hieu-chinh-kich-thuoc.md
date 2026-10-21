---
id: ac-05-09
title: Hiệu chỉnh và xử lý kích thước với DIMEDIT và DIMTEDIT
category: Ghi kích thước
tags: [dimedit, dimtedit, dimreassociate, hieu-chinh, meo-ve]
level: intermediate
minutes: 20
needs: [ac-05-01]
appVersions: ['2024', '2025']
edition: all
---
# Hiệu chỉnh và xử lý kích thước với DIMEDIT và DIMTEDIT

> **Mục tiêu:**
> - Sử dụng lệnh `DIMEDIT` để xoay nghiêng đường gióng (Oblique) và chèn ký hiệu dung sai, tiền tố/hậu tố.
> - Sử dụng `DIMTEDIT` để di chuyển và định vị lại vị trí chữ số kích thước linh hoạt.
> - Khôi phục tính liên kết kích thước với đối tượng hình học bằng `DIMREASSOCIATE`.

## Tại sao cần hiệu chỉnh kích thước sau khi đo?

Khi hoàn thiện một bản vẽ kỹ thuật chi tiết, rất hiếm khi các đường kích thước đo ra là xong ngay. Bạn sẽ gặp các tình huống:
- Đường gióng kích thước đè lên nét thấy hoặc đường tim trục, cần phải nghiêng đi một góc để tránh rối mắt (đặc biệt trong bản vẽ hình chiếu trục đo Isodraft).
- Chữ số kích thước bị chèn chúc ở những đoạn hẹp, cần dời vị trí hoặc xoay ngang/dọc.
- Cần thêm tiền tố số lượng (ví dụ: `4xØ12` thay vì chỉ hiển thị `Ø12`) hoặc thêm dung sai `±0.05`.
- Chi tiết hình học bị di chuyển khiến đường kích thước bị "mất gốc" (bị ngắt liên kết - Non-associative).

Bộ ba công cụ `DIMEDIT`, `DIMTEDIT` và `DIMREASSOCIATE` sinh ra để giải quyết triệt để những tình huống này.

## Cách dùng từng bước

### 1. Thay đổi nội dung chữ và độ nghiêng đường gióng với DIMEDIT
Lệnh tắt: `DED` hoặc `DIMEDIT`. Khi chạy lệnh, có 4 tuỳ chọn chính:
- **`Home`:** Đưa chữ số kích thước quay trở lại vị trí và góc nghiêng chuẩn mực mặc định của Dimstyle.
- **`New`:** Mở hộp thoại soạn thảo văn bản để thêm tiền tố hoặc hậu tố.
  *(Quy tắc quan trọng: Cặp dấu ngoặc nhọn `<>` đại diện cho giá trị kích thước thực đo. Nếu bạn gõ `4x<>` thì trên bản vẽ sẽ hiển thị `4x50`. Nếu bạn xoá mất `<>`, con số tự động sẽ bị thay thế bằng chữ tĩnh).*
- **`Rotate`:** Nhập góc xoay nghiêng của riêng con số kích thước.
- **`Oblique`:** Làm xiên đường gióng kích thước một góc tùy ý (rất hay dùng khi vẽ kích thước hình chiếu trục đo hoặc tránh đè nét chữ khác).

### 2. Dời vị trí chữ số kích thước nhanh với DIMTEDIT
Lệnh tắt: `DIMTEDIT` (Dimension Text Edit):
1. Gõ `DIMTEDIT` rồi nhấn [Enter].
2. Bấm chọn đường kích thước cần chỉnh.
3. Di chuột để kéo con số sang trái, sang phải hoặc kéo ra ngoài đường gióng.
4. Bấm chuột để đặt con số vào vị trí mới thông thoáng hơn.

### 3. Gắn lại liên kết kích thước bị mất với DIMREASSOCIATE
Khi một đối tượng hình học bị kéo dãn hoặc sao chép cắt dán, đường kích thước đôi khi bị mất liên kết (mất chấm tròn màu vàng cảnh báo).
1. Gõ `DIMREASSOCIATE` rồi nhấn [Enter].
2. Chọn các đường kích thước bị mất liên kết, nhấn [Enter].
3. AutoCAD sẽ đánh dấu chữ X vào từng đầu mút kích thước. Bạn chỉ việc dùng bắt điểm `Endpoint` bấm lại vào các góc chi tiết tương ứng.
4. Kích thước sẽ lập tức gắn chặt trở lại với đối tượng!

## Ký hiệu đặc biệt hay dùng trong kích thước

Khi sửa nội dung kích thước (trong `DIMEDIT` hoặc nhấp đúp chuột vào chữ số), bạn có thể gõ các mã ký tự tắt sau:
- **`%%c`:** Tạo ký hiệu đường kính phi $\varnothing$ (ví dụ: `%%c50` $\to$ $\varnothing 50$).
- **`%%d`:** Tạo ký hiệu độ góc $^{\circ}$ (ví dụ: `45%%d` $\to$ $45^{\circ}$).
- **`%%p`:** Tạo ký hiệu cộng trừ sai số $\pm$ (ví dụ: `<>%%p0.02` $\to$ $100 \pm 0.02$).

> [!TIP]
> Thay vì dùng lệnh phức tạp, cách nhanh nhất để dời số kích thước là bấm chọn đường kích thước, rê chuột vào điểm kẹp màu xanh (Grip) ngay chính giữa con số, chọn **Move text only** để dời số tự do.

> [!WARNING]
> Tuyệt đối hạn chế việc gõ đè một con số "chết" (fake số kích thước) bằng cách xoá mất ký hiệu `<>`. Nếu sau này chi tiết bị co giãn, số kích thước sẽ không tự cập nhật theo, dẫn đến sai sót cực kỳ nghiêm trọng trong sản xuất!

## Tự kiểm tra

```quiz
id: q-ac-05-09-1
type: single
question: "Trong lệnh DIMEDIT (DED), ký hiệu nào đại diện cho giá trị đo thực tế tự động của đối tượng?"
options:
  - text: "Cặp dấu ngoặc nhọn <>"
    correct: true
    why: "Ký hiệu <> giữ nguyên giá trị tự tính toán của kích thước hình học."
  - text: "Cặp dấu ngoặc vuông []"
    correct: false
    why: "Dấu [] chỉ dùng để hiển thị đơn vị phụ Alternate Units."
  - text: "Ký hiệu dấu thăng ##"
    correct: false
    why: "Ký hiệu ## không phải cú pháp giữ số đo trong AutoCAD."
  - text: "Ký hiệu @@@"
    correct: false
    why: "@@@ không mang ý nghĩa giá trị đo."
explain: "Nếu bạn gõ '2x<>' thì kích thước sẽ hiển thị '2x' kèm theo chiều dài thực tế được cập nhật động."
```

```quiz
id: q-ac-05-09-2
type: single
question: "Để gõ nhanh ký hiệu cộng trừ sai số (±) vào sau kích thước, bạn dùng mã ký tự nào?"
options:
  - text: "%%p"
    correct: true
    why: "%%p là mã shortcut xuất ký hiệu Plus/Minus (±)."
  - text: "%%c"
    correct: false
    why: "%%c là mã xuất ký hiệu đường kính Ø."
  - text: "%%d"
    correct: false
    why: "%%d là mã xuất ký hiệu độ góc °."
  - text: "%%u"
    correct: false
    why: "%%u là mã gạch chân chữ (Underline)."
explain: "Bộ ba mã %%c, %%d, %%p là những phím tắt kinh điển mọi người dùng AutoCAD đều phải thuộc lòng."
```

```quiz
id: q-ac-05-09-3
type: truefalse
question: "Lệnh DIMREASSOCIATE dùng để liên kết lại đường kích thước với các đỉnh của đối tượng hình học khi liên kết bị đứt đoạn."
answer: false
explain: "Khi kích thước bị rời rạc không co giãn theo hình chi tiết, dùng DIMREASSOCIATE để bấm lại các điểm chốt đo."
```

## Lỗi thường gặp

- **Sửa đè số kích thước (Fake Dim):** Thợ gia công sản xuất phàn nàn bản vẽ sai kích thước vì người vẽ lười vẽ lại hình nên gõ đè con số khác vào. Khắc phục: Dùng `DIMEDIT` chọn tuỳ chọn `New`, xoá chữ đè đi và gõ lại `<>` để trả về giá trị thực.
- **Kích thước không chạy theo khi dùng lệnh STRETCH:** Do điểm đặt của chân đường gióng không nằm trọn trong khung chọn Crossing của lệnh Stretch, hoặc do kích thước đã bị ngắt liên kết. Khắc phục: Dùng `DIMREASSOCIATE`.

## Bài tập thực hành

- [ ] Vẽ đoạn thẳng dài 80mm bằng `LINE` và đo bằng `DIMLINEAR`. <!-- expect: DIMLINEAR -->
- [ ] Gõ lệnh `DIMEDIT` (hoặc `DED`), chọn tuỳ chọn `New`, nhập `2x<>` để hiển thị thành `2x80`. <!-- expect: DIMEDIT -->
- [ ] Gõ `DIMTEDIT`, chọn đường kích thước trên và di chuột kéo con số lệch sang mép bên phải. <!-- expect: DIMTEDIT -->
- [ ] Vẽ một góc nhọn, dùng `DIMEDIT` với tuỳ chọn `Oblique` nghiêng đường gióng một góc 30 độ. <!-- expect: DIMEDIT -->

## Nguồn tham khảo

```links
- title: "Tài liệu lệnh DIMEDIT từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=DIMEDIT"
  kind: official
- title: "Tài liệu lệnh DIMTEDIT từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=DIMTEDIT"
  kind: official
```
