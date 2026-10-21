# Bài 07: Quy Trình Điêu Khắc Nhân Vật 3D Toàn Diện (Từ Khối Lớn Đến Chi Tiết)

> **Danh mục:** Tạo Hình Nhân Vật
> **Tags:** character, sculpt, anatomy, blockout, head, body, highpoly

---

## 1. Nguyên Tắc Ba Cấp Độ Khối trong Điêu Khắc Nhân Vật

Sai lầm phổ biến nhất của người mới học điêu khắc nhân vật là: Vừa tạo khối cầu đã vội vàng phóng to để nặn lông mi, khóe môi hay nếp nhăn trán. Khi tỷ lệ tổng thể (độ to của sọ, vị trí xương hàm) bị sai, dù bạn có vẽ chi tiết đẹp đến mấy thì khuôn mặt trông vẫn méo mó, biến dạng.

Mọi họa sĩ nhân vật 3D hàng đầu đều tuân thủ nghiêm ngặt **Quy tắc 3 Cấp Độ Hình Khối**:

```text
┌─────────────────────────────────────────────────────────────┐
│ 1. Khối Lớn (Primary Forms - 70% thời gian & quyết định)   │
│    • Dáng tổng thể (Silhouette), tỷ lệ đầu thân, khung xương│
│    • Dùng cọ lớn: Grab, Move, Snake Hook                     │
├─────────────────────────────────────────────────────────────┤
│ 2. Khối Trung (Secondary Forms - 20% thời gian)             │
│    • Các mảng cơ bắp giải phẫu, hốc mắt, xương quai xanh   │
│    • Dùng cọ: Clay Strips, Clay, Flatten                    │
├─────────────────────────────────────────────────────────────┤
│ 3. Chi Tiết Nhỏ (Tertiary Forms / Micro Details - 10%)      │
│    • Nếp nhăn khóe mắt, lỗ chân lông, gân da, vân môi       │
│    • Dùng cọ: Crease, Pinch, Texture Alpha Stencil          │
└─────────────────────────────────────────────────────────────┘
```

---

## 2. Giai Đoạn 1: Chặn Dáng Thô (Blockout) và Tư Thế Chuẩn A-Pose

Thay vì nặn toàn bộ cơ thể từ một khối cầu duy nhất, phương pháp khoa học nhất là ghép nhân vật từ nhiều khối hình học đơn giản độc lập:
* **Hộp sọ:** Một khối cầu UV Sphere hơi bẹp hai bên thái dương.
* **Hàm dưới:** Một khối hộp Cube kéo vát hình chữ V.
* **Cổ & Cánh tay & Chân:** Các khối hình trụ (Cylinder) xoay uốn theo hướng cử động.
* **Lồng ngực & Xương chậu:** Hai khối hình quả trứng úp ngược.

### Tư thế chuẩn: Vì sao nên chọn A-Pose thay vì T-Pose?
* **T-Pose (Hai tay dang ngang 90 độ):** Đây là tư thế truyền thống cũ, nhưng nhược điểm là cơ vai (Deltoid) bị kéo căng quá mức, khi hạ tay xuống sát sườn sẽ sinh ra nếp nhăn xấu xí.
* **A-Pose (Hai tay xuôi chéo 45 độ):** Là **chuẩn công nghiệp hiện đại** cho game engine Unity. Cánh tay hạ nghiêng 45 độ giữ cho cơ vai và cơ ngực ở trạng thái thư giãn trung tính nhất, giúp việc nướng texture và chia trọng số xương (Weight Painting) đạt độ chính xác tối ưu.

### Hợp nhất các khối bằng Voxel Remesh
Sau khi ghép các khối con thành một dáng người hoàn chỉnh với tỷ lệ chuẩn xác:
1. Chọn tất cả các khối con ở Object Mode, nhấn `[Ctrl + J]` để gộp chung thành một đối tượng (Join).
2. Chuyển sang Sculpt Mode, nhấn `[R]` chọn kích thước ô lưới vừa phải (`0.03m - 0.04m`), nhấn `[Ctrl + R]` để Voxel Remesh.
3. Toàn bộ các khối cầu, hình trụ rời rạc sẽ tức thì được hàn liền da thịt thành một cơ thể liền mạch duy nhất!

---

## 3. Giai Đoạn 2: Giải Phẫu Cốt Lõi (Core Anatomy)

Khi bước vào nặn khối trung, bạn cần ghi nhớ các mốc giải phẫu bất biến trên cơ thể người:

### Tỷ lệ chuẩn của Khuôn Mặt:
* **Vị trí mắt:** Nằm chính xác ở đường kẻ ngang chia đôi chiều cao của toàn bộ hộp sọ (tính từ đỉnh đầu đến cằm).
* **Khoảng cách giữa hai mắt:** Bằng đúng chiều rộng của một con mắt.
* **Đáy mũi:** Nằm ở khoảng 1/2 khoảng cách từ đường lông mày đến đáy cằm.
* **Miệng:** Đáy môi dưới nằm ở 1/2 khoảng cách từ đáy mũi đến đáy cằm.
* **Chiều cao của Tai:** Đỉnh trên của vành tai ngang bằng chân mày, đáy dưới của dái tai ngang bằng đáy mũi.

### Tỷ lệ Cơ Thể (7.5 đến 8 Đầu Thân):
* Chiều cao toàn thân bằng khoảng 7.5 đến 8 lần chiều cao của đầu.
* Khớp háng (đáy xương chậu) nằm ở chính giữa chiều cao cơ thể (chia đôi nửa thân trên và nửa thân dưới).
* Khi thả lỏng tay, cổ tay ngang bằng khớp háng, đầu ngón tay chạm đến giữa đùi.

### Dùng cọ Clay Strips đắp theo thớ cơ:
Hãy đưa nét cọ uốn lượn theo đúng hướng của dây chằng và cơ bắp ngoài đời thực:
* Cơ ức đòn chũm (cơ cổ) chạy chéo từ sau mang tai hội tụ về hõm xương ức.
* Cơ ngực lớn (Pectoralis Major) bắt nguồn từ xương ức và tỏa hình nan quạt cắm thẳng vào xương cánh tay.
* Dùng cọ **Flatten** để gọt các mặt phẳng chuyển tiếp dứt khoát trên gò má, cằm và trán.

---

## 4. Giai Đoạn 3: Tinh Chỉnh Chi Tiết Cao Cấp (High-Poly Detailing)

Để thêm chi tiết nếp nhăn và mí mắt mà không làm hỏng lưới gốc, bạn có thể áp dụng hai phương pháp:

### Phương pháp 1: Voxel Remesh chi tiết cao
* Nhấn `[R]` hạ nhỏ kích thước lưới xuống `0.008m` hoặc `0.005m` và nhấn `[Ctrl + R]`. Lưới sẽ tăng lên khoảng 1 đến 3 triệu đỉnh. Dùng cọ **Crease `[Shift + C]`** và **Pinch `[P]`** để khắc mí mắt, rãnh môi và nếp gấp vành tai.

### Phương pháp 2: Bộ điều chỉnh Đa Phân Giải (Multiresolution Modifier)
* Đây là công cụ điêu khắc chuẩn Hollywood: Cho phép bạn lưu trữ nhiều cấp độ phân giải đa giác trên cùng một mô hình. Bạn có thể chuyển về cấp độ 1 để chỉnh sửa dáng lớn, rồi chuyển lên cấp độ 4 để vẽ lỗ chân lông chi tiết.

---

## Bài tập thực hành

**Mục tiêu:** Điêu khắc phần đầu nhân vật hoạt hình Stylized (Stylized Head) có cấu trúc mắt mũi rõ ràng trong 15 phút.

1. Tạo một khối cầu **UV Sphere**, nhấn `[Tab]` sang Sculpt Mode, bật đối xứng trục X bằng phím `[X]`.
2. Dùng cọ **Grab `[G]`** kéo cằm nhọn xuống và ép dẹp hai bên thái dương để tạo phom dáng hộp sọ quả trứng.
3. Kéo mặt phẳng ngang chia đôi đầu, dùng cọ **Clay** giữ phím `[Ctrl]` khoét lõm sâu hai hốc mắt tròn.
4. Đặt 3D Cursor vào giữa hốc mắt, nhấn `[Shift + A]` (ở Object Mode) thêm một khối cầu nhỏ UV Sphere làm tròng mắt. Thêm Mirror Modifier cho tròng mắt để có đủ cả hai bên.
5. Quay lại khối đầu ở Sculpt Mode: Dùng cọ **Clay Strips** đắp sống mũi nhô ra phía trước, đắp gò má cao tròn.
6. Dùng cọ **Snake Hook `[K]`** kéo nhẹ phần dái tai hai bên ngang tầm mắt.
7. Nhấn `[R]` đặt Voxel Size `0.02m`, nhấn `[Ctrl + R]` để làm mới lưới.
8. Dùng cọ **Crease `[Shift + C]`** khắc nếp mí mắt ôm quanh khối cầu tròng mắt và khắc đường phân cách giữa hai cánh môi.
9. Dùng cọ **Smooth `[Shift + Click]`** vuốt nhẹ da mặt cho mịn màng tròn trịa, tạo nên một khuôn mặt nhân vật hoạt hình biểu cảm.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/sculpt_paint/sculpting/index.html
- https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/multiresolution.html
- https://docs.blender.org/manual/en/5.2/sculpt_paint/sculpting/tools/clay_strips.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
