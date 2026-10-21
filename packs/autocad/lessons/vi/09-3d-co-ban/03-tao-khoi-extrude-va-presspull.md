---
id: ac-09-03
title: Tạo khối 3D từ hình phẳng 2D với EXTRUDE và PRESSPULL
category: Mô hình hoá 3D
tags: [extrude, presspull, tao-khoi, solid, 3d-co-ban]
level: intermediate
minutes: 25
needs: [ac-09-01]
appVersions: ['2024', '2025']
edition: full-only
---
# Tạo khối 3D từ hình phẳng 2D với EXTRUDE và PRESSPULL

> **Mục tiêu:**
> - Sử dụng lệnh `EXTRUDE` để kéo đùn các hình phẳng 2D thành các khối đặc [[Solid]] 3D theo chiều cao hoặc đường dẫn.
> - Làm chủ lệnh `PRESSPULL` để tạo khối và khoét lỗ trực quan chỉ bằng một thao tác ấn/kéo chuột.
> - Phân biệt điều kiện tạo khối đặc khép kín (Solid) so với bề mặt mỏng hở (Surface).

## Từ bản vẽ 2D biến thành vật thể 3D thực tế

Trong quy trình thiết kế công nghiệp hoặc xây dựng, 90% các vật thể 3D đều bắt đầu từ một bản vẽ phẳng 2D:
- Bạn vẽ mặt bằng ngôi nhà (tường dày 220mm) $\to$ Đùn cao lên 3.6 mét thành những bức tường gạch 3D vững chãi.
- Bạn vẽ mặt cắt một bánh răng hoặc một mặt bích có nhiều lỗ bu lông $\to$ Đùn dày lên 25mm thành một chi tiết cơ khí bằng thép.

Hai công cụ quyền lực nhất để thực hiện phép màu này trong AutoCAD là **`EXTRUDE`** và **`PRESSPULL`**.

![So sánh EXTRUDE và PRESSPULL](media/ac-09-03-extrude-presspull.svg)

```hotspots
image: media/ac-09-03-extrude-presspull.svg
alt: So sánh hai phương pháp đùn khối EXTRUDE và PRESSPULL
layout: central
points:
  - id: spot-1
    x: 23
    y: 35
    title: Lệnh EXTRUDE (EXT)
    text: "Kéo đùn đối tượng hình học khép kín theo phương vuông góc hoặc theo góc nghiêng Taper."
  - id: spot-2
    x: 23
    y: 75
    title: Yêu cầu biên dạng khép kín
    text: "Phải là Polyline, Circle hoặc Region khép kín để tạo thành khối đặc Solid."
  - id: spot-3
    x: 75
    y: 35
    title: Lệnh PRESSPULL (Ấn/Kéo)
    text: "Tự nhận diện vùng khép kín bất kỳ không cần biến thành Polyline trước."
  - id: spot-4
    x: 75
    y: 75
    title: Kéo lên = Đắp; Đùn xuống = Khoét
    text: "Kéo chuột lên trên để đắp thêm thịt, ấn chuột xuống dưới để khoét thủng lỗ tức thì."
```

## 1. Kéo đùn chuẩn mực với lệnh EXTRUDE (Lệnh tắt EXT)

### Điều kiện tiên quyết:
Để `EXTRUDE` tạo ra được một khối đặc [[Solid]] 3D: Biên dạng 2D **bắt buộc phải là một đường khép kín hoàn hảo** (Hình tròn, Hình chữ nhật, hoặc đường `PLINE` đã được khép góc bằng lệnh `JOIN`).
*Nếu bạn chọn một đoạn thẳng `LINE` hở để Extrude, AutoCAD chỉ tạo ra một bề mặt mỏng tanh không có thể tích ruột (`Surface`)!*

### Cách dùng từng bước:
1. Chuyển góc nhìn sang 3D trục đo (ví dụ: `SW Isometric`).
2. Vẽ một hình chữ nhật khép kín kích thước 100 x 60 mm bằng `RECTANG`.
3. Gõ `EXT` hoặc `EXTRUDE` rồi nhấn [Enter].
4. Bấm chọn hình chữ nhật vừa vẽ, nhấn [Enter].
5. Di chuột lên trên hoặc gõ độ cao: ví dụ `80` rồi nhấn [Enter].
6. Hình chữ nhật 2D phẳng lì ngay lập tức hóa thân thành một khối hộp chữ nhật 3D đặc ruột cao 80mm!

### Các tùy chọn nâng cao của EXTRUDE:
- **`Direction` (Hướng):** Đùn khối theo một phương xiên bất kỳ thay vì phương vuông góc mặc định.
- **`Path` (Đường dẫn):** Kéo đùn biên dạng chạy dọc theo một đường cong uốn lượn (Spline hoặc Arc).
- **`Taper angle` (Góc vát chóp):** Vát thon nhỏ dần lên đỉnh để tạo các khối hình kim tự tháp hoặc hình nón cụt (ví dụ vát góc 10 độ).

## 2. Kéo đùn siêu tốc và khoét lỗ tức thì với PRESSPULL

Nếu như `EXTRUDE` đòi hỏi bạn phải mất công nối các nét thành Polyline khép kín, thì **`PRESSPULL`** vượt trội hơn hẳn:
Nó hoạt động tương tự lệnh tô mặt cắt `HATCH`: Tự động nhận diện ranh giới của bất kỳ vùng khép kín nào!

### Cách dùng từng bước:
1. Vẽ một hình chữ nhật bằng các nét thẳng `LINE` rời rạc, bên trong vẽ thêm 2 hình tròn lỗ bu lông.
2. Gõ `PRESSPULL` rồi nhấn [Enter] (hoặc bấm biểu tượng Presspull nổi bật trên Ribbon).
3. Đưa con trỏ chuột vào vùng trống nằm giữa hình chữ nhật và 2 hình tròn:
   - Toàn bộ vùng diện tích xung quanh sẽ sáng rực lên (AutoCAD tự trừ bỏ 2 hình tròn).
4. Bấm chuột trái một cái, rồi kéo chuột lên trên nhập chiều cao `30` mm.
5. Một tấm bích thép dày 30mm có sẵn 2 lỗ khoét thông suốt xuất hiện ngay lập tức mà không cần thêm bất kỳ lệnh cắt gọt nào!

### Thao tác khoét lỗ thần kỳ:
- Vẽ một hình tròn trên bề mặt trên của một khối hộp đã có sẵn.
- Gõ `PRESSPULL`, bấm vào bên trong hình tròn đó.
- Kéo chuột **ấn tụt xuống phía dưới** đáy khối hộp.
- Khối hộp lập tức bị khoét một lỗ thủng xuyên suốt cực kỳ mượt mà!

> [!TIP]
> Giữ phím [Ctrl + Alt] khi bấm vào một vùng kín trên màn hình cũng là phím tắt nhanh để gọi ngay tính năng PRESSPULL trong AutoCAD.

## Tự kiểm tra

```quiz
id: q-ac-09-03-1
type: single
question: "Điều kiện bắt buộc của biên dạng 2D để lệnh EXTRUDE tạo ra được một khối đặc 3D Solid (thay vì bề mặt Surface) là gì?"
options:
  - text: "Biên dạng phải là một đường khép kín hoàn hảo (như Circle, Polygon, Polyline khép kín)"
    correct: true
    why: "Chỉ các biên dạng kín mới chứa đựng diện tích để sinh ra thể tích khối đặc 3D."
  - text: "Biên dạng bắt buộc phải có màu đỏ"
    correct: false
    why: "Màu sắc không ảnh hưởng đến khả năng tạo khối."
  - text: "Biên dạng phải có kích thước lớn hơn 1 mét"
    correct: false
    why: "Kích thước to hay nhỏ đều Extrude được bình thường."
  - text: "Phải vẽ bằng nét đứt"
    correct: false
    why: "Nét đứt hay nét liền đều Extrude được."
explain: "Nếu đùn một đường thẳng hoặc cung hở bằng EXTRUDE, phần mềm sẽ tạo ra bề mặt mỏng Surface không có khối lượng thể tích."
```

```quiz
id: q-ac-09-03-2
type: single
question: "Ưu điểm vượt trội lớn nhất của lệnh PRESSPULL so với EXTRUDE là gì?"
options:
  - text: "Tự nhận diện vùng khép kín như lệnh HATCH và tự động khoét lỗ khi ấn chuột xuống dưới"
    correct: true
    why: "PRESSPULL tự phân tích ranh giới và hỗ trợ thao tác đắp thêm / khoét bỏ khối cực kỳ linh hoạt."
  - text: "Chỉ chạy được trên máy tính cấu hình yếu"
    correct: false
    why: "PRESSPULL là lệnh tiêu chuẩn cho mọi máy tính cài AutoCAD."
  - text: "Không bao giờ tốn dung lượng RAM"
    correct: false
    why: "Mọi đối tượng 3D đều tiêu tốn bộ nhớ đồ họa."
  - text: "Tự động đổi màu vật thể sang màu tím"
    correct: false
    why: "Màu sắc do Layer quản lý."
explain: "Tính năng nhận diện vùng thông minh và tự trừ khối khi đẩy chuột xuống biến PRESSPULL thành công cụ tạo khối 3D được dùng nhiều nhất hiện nay."
```

```quiz
id: q-ac-09-03-3
type: truefalse
question: "Tùy chọn Taper Angle trong lệnh EXTRUDE cho phép kéo đùn khối bóp thon nhỏ dần theo góc vát để tạo các khối hình kim tự tháp hoặc hình nón cụt."
answer: true
explain: "Taper Angle tạo độ nghiêng vát cho các mặt bên trong quá trình đùn chiều cao."
```

## Lỗi thường gặp

- **Extrude ra một chiếc hộp rỗng ruột chỉ có 4 mặt bên:** Do khi vẽ hình chữ nhật, bạn vẽ bằng 4 đoạn thẳng `LINE` rời rạc chưa nối `JOIN` thành một Polyline kín. Khắc phục: Dùng `JOIN` quét chọn 4 cạnh để đóng kín lại trước khi Extrude.
- **PRESSPULL không nhận diện được vùng:** Do vùng ranh giới bị hở một khe nhỏ ở góc, hoặc do góc nhìn xoay quá nghiêng. Khắc phục: Xoay lại góc nhìn trực diện hơn và kiểm tra khép kín góc.

## Bài tập thực hành

- [ ] Chuyển góc nhìn sang `SW Isometric` và đổi kiểu hiển thị sang `Shaded with Edges`.
- [ ] Dùng `RECTANG` vẽ một hình chữ nhật 120 x 80 mm. <!-- expect: RECTANG -->
- [ ] Gõ lệnh `EXTRUDE` (hoặc `EXT`), chọn hình chữ nhật và đùn cao lên 60 mm. <!-- expect: EXTRUDE -->
- [ ] Dùng lệnh `CIRCLE` vẽ một hình tròn bán kính 20mm trên mặt trên của khối hộp vừa tạo. <!-- expect: CIRCLE -->
- [ ] Gõ lệnh `PRESSPULL`, bấm vào trong hình tròn và đẩy chuột xuống dưới để khoét thủng một lỗ tròn xuyên suốt thân hộp. <!-- expect: PRESSPULL -->

## Nguồn tham khảo

```links
- title: "Kéo đùn khối với lệnh EXTRUDE từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=EXTRUDE"
  kind: official
- title: "Thao tác ấn kéo tạo khối với PRESSPULL từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=PRESSPULL"
  kind: official
```
