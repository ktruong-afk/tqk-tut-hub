---
id: ac-09-01
title: Làm quen không gian 3D và hệ toạ độ người dùng UCS
category: Mô hình hoá 3D
tags: [3d, ucs, viewcube, wcs, truc-do]
level: intermediate
minutes: 25
needs: [ac-08-07]
appVersions: ['2024', '2025']
edition: full-only
---
# Làm quen không gian 3D và hệ toạ độ người dùng UCS

> **Mục tiêu:**
> - Nhận diện trục tọa độ Z chiều cao và điều hướng góc nhìn 3D mượt mà với ViewCube và 3D Orbit.
> - Hiểu và phân biệt giữa hệ toạ độ thế giới WCS và hệ toạ độ người dùng [[UCS]].
> - Thao tác xoay mặt phẳng làm việc XY bám dính vào các mặt phẳng nghiêng trong không gian 3 chiều.

## Bước chân vào thế giới 3D của AutoCAD

Từ đầu lộ trình đến giờ, bạn đã thuần thục việc vẽ trên mặt phẳng 2D phẳng lì với hai trục X (ngang) và Y (đứng). Nhưng trong thực tế, các chi tiết cơ khí, nhà cửa hay địa hình đều tồn tại trong không gian 3 chiều có thêm **trục Z (Chiều cao)**.

Trong phiên bản AutoCAD đầy đủ (AutoCAD Full), không gian 3D là một môi trường mô hình hóa cực kỳ trực quan:
- Bạn có thể dựng các khối đặc [[Solid]] có khối lượng, thể tích và trọng tâm.
- Bạn có thể xoay mô hình 360 độ để soi ngắm mọi ngóc ngách bên trong.
- Và quan trọng nhất: Từ một mô hình 3D duy nhất, bạn có thể tự động xuất ra toàn bộ các hình chiếu 2D mặt bằng, mặt đứng, mặt cắt mà không bao giờ lo sai lệch kích thước!

![Không gian 3D và hệ toạ độ UCS](media/ac-09-01-3d-ucs-views.svg)

```hotspots
image: media/ac-09-01-3d-ucs-views.svg
alt: Không gian 3D hệ toạ độ UCS và khối điều hướng ViewCube
layout: central
points:
  - id: spot-1
    x: 23
    y: 35
    title: Trục toạ độ Z chiều cao
    text: "Trục Z màu xanh dương vuông góc với mặt phẳng XY, quy định chiều cao và độ sâu vật thể."
  - id: spot-2
    x: 23
    y: 75
    title: Hệ toạ độ người dùng UCS
    text: "Cho phép dời gốc toạ độ và xoay mặt phẳng XY tự do lên bất kỳ bề mặt nghiêng nào."
  - id: spot-3
    x: 75
    y: 35
    title: Khối điều hướng ViewCube
    text: "Bấm vào các mặt Top, Front, Right hoặc các góc để vào góc nhìn trục đo Isometric."
  - id: spot-4
    x: 75
    y: 75
    title: Phím tắt 3D Orbit
    text: "Nhấn giữ Shift + Chuột giữa để xoay tự do mô hình 3D trong không gian."
```

## Điều hướng không gian 3D trong nháy mắt

- **Xoay tự do (3D Orbit):** Nhấn giữ phím **[Shift]** kết hợp nhấn giữ **[Bánh xe chuột giữa]** rồi di chuột. Bạn sẽ thấy bản vẽ xoay tròn trong không gian 3D cực kỳ mượt mà!
- **Khối điều hướng ViewCube:** Ở góc trên bên phải màn hình, bấm vào các đỉnh góc của khối lập phương ViewCube (ví dụ góc Tây Nam `SW Isometric`) để đưa bản vẽ về góc nhìn trục đo tiêu chuẩn 30 độ.
- **Biểu tượng trục UCS Icon:**
  - Trục X màu **Đỏ**.
  - Trục Y màu **Xanh lá**.
  - Trục Z màu **Xanh dương**.
  *(Mẹo nhớ màu RGB tương ứng với thứ tự trục XYZ).*

## Nguyên lý số 1 của 3D: Quy tắc mặt phẳng làm việc XY

AutoCAD có một nguyên lý bất biến: **Mọi lệnh vẽ 2D cơ bản (`LINE`, `CIRCLE`, `RECTANG`, `ARC`) luôn luôn chỉ được vẽ nằm bẹp trên mặt phẳng XY!**

Nếu bạn muốn vẽ một hình tròn nằm trên mái nhà dốc 45 độ, hoặc trên mặt hông của một khối hộp:
- Bạn bắt buộc phải xoay mặt phẳng XY của hệ toạ độ bám dính vào mặt phẳng nghiêng đó.
- Lệnh **`UCS` (User Coordinate System)** sinh ra để làm nhiệm vụ này.

## Cách dùng từng bước lệnh UCS

1. Gõ `UCS` rồi nhấn [Enter].
2. Thanh nhắc lệnh liệt kê các tuỳ chọn xoay toạ độ:
   - **`Face` (Gõ F):** Rê chuột vào mặt phẳng nào của vật thể 3D, mặt phẳng XY sẽ tự động hít chặt vào mặt đó! Bấm chuột trái chấp nhận.
   - **`3point` (Gõ 3):** Chỉ định 3 điểm: Điểm 1 là gốc tọa độ mới (0,0,0), Điểm 2 là hướng trục X mới, Điểm 3 là hướng trục Y mới.
   - **`View` (Gõ V):** Xoay mặt phẳng XY song song với màn hình mắt nhìn hiện tại.
   - **`World` (Gõ W hoặc nhấn Enter):** Đưa hệ toạ độ quay trở về hệ quy chuẩn toàn cầu mặc định (WCS).
3. Sau khi xoay UCS xong, bạn có thể vẽ đường tròn hoặc chữ viết nằm khít trên mặt phẳng nghiêng đó một cách hoàn hảo!

## Tính năng tự động Dynamic UCS (Phím F6)

Nếu bạn không muốn mỗi lần vẽ lại phải gõ lệnh `UCS`:
- Nhấn phím chức năng **[F6]** để bật chế độ **Dynamic UCS (DUCS)**.
- Khi bật F6, bạn chỉ cần gọi lệnh vẽ (ví dụ `CIRCLE`), rê chuột qua bất kỳ mặt nào của khối 3D, mặt đó sẽ sáng xanh lên và nhận diện mặt phẳng làm việc tức thì!

> [!TIP]
> Luôn gõ lệnh `UCS` rồi nhấn phím [Enter] hai lần để trả hệ toạ độ về lại hệ toạ độ thế giới (`World`) sau khi hoàn tất các thao tác vẽ nghiêng.

## Tự kiểm tra

```quiz
id: q-ac-09-01-1
type: single
question: "Thao tác chuột nhanh nhất để xoay tự do (3D Orbit) mô hình 3D trong không gian AutoCAD là gì?"
options:
  - text: "Nhấn giữ phím Shift kết hợp nhấn giữ bánh xe chuột giữa và di chuột"
    correct: true
    why: "Tổ hợp Shift + Chuột giữa kích hoạt ngay chế độ xoay 3D Orbit mượt mà."
  - text: "Nhấp đúp chuột trái hai lần"
    correct: false
    why: "Nhấp đúp chuột trái chỉ mở bảng sửa thuộc tính."
  - text: "Lăn bánh xe chuột tiến và lùi"
    correct: false
    why: "Lăn chuột chỉ thực hiện thao tác Zoom phóng to thu nhỏ."
  - text: "Nhấn giữ phím Ctrl + chuột phải"
    correct: false
    why: "Ctrl + chuột phải mở menu truy bắt điểm Osnap."
explain: "Tổ hợp phím Shift + bánh xe chuột giữa là phản xạ vàng của mọi kỹ sư mô hình hóa 3D trong AutoCAD."
```

```quiz
id: q-ac-09-01-2
type: single
question: "Theo quy chuẩn biểu diễn màu sắc trục toạ độ 3D (RGB tương ứng XYZ), trục Z chiều cao có màu sắc gì?"
options:
  - text: "Màu xanh dương (Blue)"
    correct: true
    why: "R = Đỏ (X), G = Xanh lá (Y), B = Xanh dương (Z)."
  - text: "Màu đỏ (Red)"
    correct: false
    why: "Màu đỏ là trục X."
  - text: "Màu xanh lá (Green)"
    correct: false
    why: "Màu xanh lá là trục Y."
  - text: "Màu vàng (Yellow)"
    correct: false
    why: "Không có trục toạ độ chuẩn màu vàng."
explain: "Trục Z luôn mang màu xanh dương đại diện cho chiều cao trong hệ toạ độ 3 chiều."
```

```quiz
id: q-ac-09-01-3
type: truefalse
question: "Phím chức năng F6 (Dynamic UCS) cho phép AutoCAD tự động nhận diện và áp mặt phẳng vẽ XY lên bề mặt khối 3D khi rê chuột."
answer: true
explain: "Dynamic UCS giúp người vẽ tiết kiệm rất nhiều thao tác xoay trục toạ độ thủ công khi dựng hình trên các mặt bên của vật thể."
```

## Lỗi thường gặp

- **Vẽ hình tròn nhưng hình cứ bay lơ lửng ngoài không gian:** Do mặt phẳng XY của hệ toạ độ UCS đang bị lệch trục so với bề mặt bạn muốn vẽ. Khắc phục: Gõ `UCS` chọn `Face` bấm vào mặt phẳng của khối trước khi vẽ, hoặc bật phím `F6`.
- **Mất phương hướng không biết đâu là mặt trước mặt trên:** Do xoay mô hình quá đà. Khắc phục: Bấm vào chữ **Top** hoặc nút biểu tượng ngôi nhà (Home) trên ViewCube để đưa bản vẽ về góc chuẩn.

## Bài tập thực hành

- [ ] Nhấn giữ phím `Shift` + bánh xe chuột giữa để xoay không gian vẽ sang góc nhìn 3D trục đo.
- [ ] Bấm vào góc trên ViewCube để chuyển về góc nhìn `SW Isometric`.
- [ ] Gõ lệnh `BOX`, vẽ một khối hộp chữ nhật có kích thước 100 x 80 x 50 mm. <!-- expect: BOX -->
- [ ] Gõ lệnh `UCS`, chọn tuỳ chọn `Face` và bấm chọn vào mặt bên hông của khối hộp. <!-- expect: UCS -->
- [ ] Dùng lệnh `CIRCLE` vẽ một hình tròn bán kính 15mm ngay trên mặt hông vừa chọn. <!-- expect: CIRCLE -->
- [ ] Gõ lệnh `UCS` và nhấn [Enter] 2 lần để đưa hệ toạ độ về lại hệ chuẩn `World`. <!-- expect: UCS -->

## Nguồn tham khảo

```links
- title: "Hệ toạ độ UCS trong không gian 3D từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=UCS+3D"
  kind: official
- title: "Điều hướng mô hình 3D với ViewCube từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=ViewCube"
  kind: official
```
