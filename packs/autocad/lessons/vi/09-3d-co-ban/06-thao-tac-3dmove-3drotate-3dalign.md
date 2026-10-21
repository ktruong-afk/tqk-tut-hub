---
id: ac-09-06
title: Thao tác biến đổi trong không gian với 3DMOVE, 3DROTATE và 3DALIGN
category: Mô hình hoá 3D
tags: [3dmove, 3drotate, 3dalign, gizmo, lap-rap-3d]
level: intermediate
minutes: 25
needs: [ac-09-05]
appVersions: ['2024', '2025']
edition: full-only
---
# Thao tác biến đổi trong không gian với 3DMOVE, 3DROTATE và 3DALIGN

> **Mục tiêu:**
> - Sử dụng công cụ con trỏ trục toạ độ 3D Gizmo để di chuyển và xoay vật thể trực quan trong không gian 3 chiều.
> - Làm chủ lệnh `3DMOVE` và `3DROTATE` khóa theo từng trục toạ độ X, Y, Z.
> - Sử dụng lệnh `3DALIGN` để ráp nối chính xác các bề mặt và khớp tiếp xúc giữa hai chi tiết máy 3D.

## Con trỏ trực quan 3D Gizmo: Trợ thủ đắc lực trong không gian

Khi thao tác trong không gian 2D, các lệnh `MOVE` và `ROTATE` chỉ hoạt động trên một mặt phẳng duy nhất. Nhưng trong không gian 3D:
- Bạn muốn nâng một cái dầm lên cao thêm 2.5 mét theo trục Z.
- Bạn muốn xoay nghiêng một cánh quạt góc 30 độ quanh trục nghiêng.
- Bạn muốn ốp một tấm thép bích vào đúng mặt bên của một cột chịu lực.

Nếu chỉ dùng lệnh di chuyển thông thường, con trỏ chuột rất dễ bị bắt nhầm độ sâu trong không gian ảo.

Để giải quyết vấn đề này, AutoCAD cung cấp công cụ **3D Gizmo** (hiển thị dưới dạng 3 mũi tên màu sắc hoặc 3 vòng tròn xoay bao quanh vật thể) cùng bộ ba lệnh biến đổi: **`3DMOVE`**, **`3DROTATE`** và **`3DALIGN`**.

## 1. Di chuyển khóa trục với 3DMOVE và Move Gizmo

Khi bạn bấm chọn một khối 3D bất kỳ (trong chế độ hiển thị `Shaded` hoặc `Conceptual`), một biểu tượng gồm 3 mũi tên màu **Đỏ (X)**, **Xanh lá (Y)**, **Xanh dương (Z)** sẽ xuất hiện ngay tại tâm vật thể:
1. Gõ `3DMOVE` rồi nhấn [Enter], bấm chọn khối 3D.
2. Bấm chuột trái vào **đầu mũi tên màu xanh dương (trục Z)**:
   - Toàn bộ chuyển động của chuột lập tức bị khóa cứng chỉ được phép chạy thẳng đứng lên trên hoặc xuống dưới theo trục Z!
3. Nhập khoảng cách nâng cao: ví dụ gõ `150` rồi nhấn [Enter].
4. Vật thể được nhấc bổng lên cao đúng 150mm theo phương thẳng đứng mà không bao giờ bị lệch sang hai bên!

## 2. Xoay góc trong không gian với 3DROTATE và Rotate Gizmo

Khi cần dựng đứng một chi tiết đang nằm bẹp dưới sàn, hoặc xoay nghiêng chi tiết trong không gian:
1. Gõ `3DROTATE` rồi nhấn [Enter].
2. Bấm chọn vật thể 3D cần xoay, nhấn [Enter].
3. Ba vòng tròn màu sắc bao quanh khối xuất hiện (Vòng đỏ xoay quanh trục X, vòng xanh lá xoay quanh trục Y, vòng xanh dương xoay quanh trục Z).
4. Bấm chuột chọn vào **vòng tròn màu đỏ**:
   - Một đường trục xoay màu đỏ sáng rực lên. Vật thể giờ đây chỉ có thể quay quanh trục X.
5. Gõ góc quay: ví dụ `90` rồi nhấn [Enter].
6. Vật thể lập tức dựng đứng vuông góc 90 độ một cách chuẩn xác!

## 3. Lắp ráp và căn gióng hai chi tiết máy với 3DALIGN

Lệnh `3DALIGN` (3D Align) là công cụ tối thượng cho bài toán lắp ráp cơ khí: Nó cho phép bạn bê một chi tiết và dán áp chặt vào một chi tiết khác thông qua việc so khớp 3 điểm mốc (Mặt phẳng tiếp xúc $\to$ Hướng trục $\to$ Điểm chốt định vị).

### Quy trình 3 cặp điểm của 3DALIGN:
1. Gõ `3DALIGN` rồi nhấn [Enter].
2. Bấm chọn chi tiết cần mang đi lắp ráp (vật thể di chuyển), nhấn [Enter].
3. **Phần 1: Chọn 3 điểm trên vật thể di chuyển (Source points):**
   - *Base point:* Bấm điểm gốc 1 (ví dụ tâm của đáy lỗ khoan).
   - *Second point:* Bấm điểm 2 quy định hướng trục X (ví dụ mép cạnh).
   - *Third point:* Bấm điểm 3 quy định hướng mặt phẳng XY.
4. **Phần 2: Chọn 3 điểm tương ứng trên vật thể đích (Destination points):**
   - *First destination point:* Bấm vào tâm mặt bích cần áp vào.
   - *Second destination point:* Bấm hướng trục tương ứng.
   - *Third destination point:* Bấm mặt phẳng tương ứng.
5. Ngay lập tức, chi tiết di chuyển sẽ bay đến, tự động xoay lật đúng góc và áp khít chặt chẽ vào vị trí đích mà không để lại bất kỳ khe hở nào!

> [!TIP]
> Bạn có thể chuyển đổi nhanh giữa Move Gizmo, Rotate Gizmo và Scale Gizmo bằng cách nhấp chuột phải vào biểu tượng Gizmo trên màn hình và chọn chế độ mong muốn.

## Tự kiểm tra

```quiz
id: q-ac-09-06-1
type: single
question: "Khi sử dụng lệnh 3DMOVE, thao tác nào giúp người vẽ khóa hướng di chuyển chỉ chạy dọc theo phương thẳng đứng chiều cao?"
options:
  - text: "Bấm chuột vào mũi tên màu xanh dương (trục Z) của con trỏ 3D Gizmo"
    correct: true
    why: "Mũi tên màu xanh dương đại diện cho trục Z chiều cao trong hệ toạ độ 3D."
  - text: "Bấm chuột vào mũi tên màu đỏ"
    why: "Mũi tên màu đỏ khóa hướng theo trục X."
  - text: "Bấm chuột vào mũi tên màu xanh lá"
    why: "Mũi tên màu xanh lá khóa hướng theo trục Y."
  - text: "Tắt màn hình máy tính"
    why: "Không liên quan đến thao tác lệnh."
explain: "Bấm vào từng trục màu trên Gizmo sẽ khóa cứng hướng chuyển động của vật thể theo đúng phương toạ độ đó."
```

```quiz
id: q-ac-09-06-2
type: single
question: "Lệnh nào trong AutoCAD là tối ưu nhất để mang một chi tiết 3D và lắp ráp áp khớp mặt phẳng vào một chi tiết khác thông qua 3 điểm mốc toạ độ?"
options:
  - text: "3DALIGN"
    correct: true
    why: "3DALIGN căn gióng và xoay áp sát đồng thời mặt phẳng và điểm tiếp xúc giữa hai vật thể 3D."
  - text: "MOVE"
    why: "MOVE thông thường chỉ tịnh tiến mà không xoay áp góc 3 chiều."
  - text: "ALIGN"
    why: "ALIGN thông thường chuyên dùng căn gióng 2D."
  - text: "MIRROR"
    why: "MIRROR là lệnh lấy đối xứng."
explain: "Lệnh 3DALIGN là công cụ đắc lực nhất cho các bài toán lắp ghép cụm chi tiết máy 3D."
```

```quiz
id: q-ac-09-06-3
type: truefalse
question: "Lệnh 3DROTATE hiển thị ba vòng tròn màu sắc quanh vật thể cho phép người vẽ chỉ định xoay quanh trục X, Y hoặc Z độc lập."
answer: true
explain: "Ba vòng tròn xoay của Rotate Gizmo giúp việc xoay góc 3D trở nên trực quan và không bị xoay nhầm hướng trong không gian."
```

## Lỗi thường gặp

- **Chi tiết bị văng ra xa hàng cây số khi dùng 3DALIGN:** Do chọn thứ tự 3 cặp điểm không tương ứng (ví dụ: điểm 1 bấm góc trên nhưng điểm đích 1 lại bấm góc dưới). Hãy kiểm tra bấm đối ứng chuẩn xác từng cặp điểm một.
- **Không thấy biểu tượng Gizmo hiện lên khi bấm vào khối:** Do đang ở chế độ hiển thị `2D Wireframe`. Khắc phục: Chuyển kiểu hiển thị sang `Shaded with Edges` hoặc `Conceptual`.

## Bài tập thực hành

- [ ] Gõ `BOX`, vẽ một khối hộp kích thước 100 x 60 x 30 mm. <!-- expect: BOX -->
- [ ] Gõ lệnh `3DMOVE`, chọn khối hộp, bấm vào mũi tên màu xanh dương (trục Z) và nhấc khối hộp lên cao 50 mm. <!-- expect: 3DMOVE -->
- [ ] Gõ lệnh `3DROTATE`, chọn khối hộp, bấm vào vòng tròn màu đỏ (trục X) và xoay khối đứng lên một góc 90 độ. <!-- expect: 3DROTATE -->
- [ ] Gõ `CYLINDER`, vẽ một hình trụ tròn bán kính 20mm cao 40mm ở vị trí bên cạnh. <!-- expect: CYLINDER -->
- [ ] Dùng lệnh `3DALIGN`, chọn hình trụ và căn gióng áp sát đáy hình trụ vào mặt trên của khối hộp vừa xoay. <!-- expect: 3DALIGN -->

## Nguồn tham khảo

```links
- title: "Thao tác với 3D Gizmos từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=3D+Gizmos"
  kind: official
- title: "Lệnh 3DALIGN căn gióng lắp ráp 3D từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=3DALIGN"
  kind: official
```
