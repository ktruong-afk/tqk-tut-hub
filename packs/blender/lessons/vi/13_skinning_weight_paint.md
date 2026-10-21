# Bài 13: Gán Trọng Số Da Thịt (Skinning & Weight Painting) Chuyên Nghiệp Cho Game

> **Danh mục:** Gắn Xương & Hoạt Họa
> **Tags:** skinning, weightpaint, vertexgroups, automaticweights, normalize, armature, unity

---

## 1. Bản Chất của Quá Trình Skinning và Hệ Thống Trọng Số (Weights)

Sau khi dựng xong bộ khung xương Armature, làm thế nào để da thịt của nhân vật biết phải co giãn theo chiếc xương nào?

**Skinning (Gán da thịt)** là kỹ thuật liên kết hình học của lưới đa giác (Mesh) vào các khớp xương thông qua bộ điều chỉnh **Armature Modifier**. Mỗi đỉnh (Vertex) trên cơ thể nhân vật sẽ được phân bổ một hệ số lực kéo gọi là **Trọng Số (Weight)**:
* Giá trị Weight nằm trong khoảng từ **`0.0`** (hoàn toàn không bị xương đó tác động) đến **`1.0`** (bị xương đó kéo đi 100%).
* **Định luật Chuẩn Hóa Bắt Buộc (Weight Normalization):** Đối với bất kỳ một đỉnh nào trên cơ thể, **tổng trọng số của tất cả các xương tác động lên đỉnh đó luôn luôn phải bằng đúng 1.0 (100%)**. Ví dụ: Một đỉnh ở giữa khuỷu tay chịu ảnh hưởng `0.5` bởi bắp tay trên và `0.5` bởi cẳng tay dưới.
* **Giới hạn kỹ thuật của Unity:** Các game engine tối ưu thường chỉ cho phép tối đa **4 xương cùng điều khiển 1 đỉnh** (4 Bones per Vertex). Nếu vượt quá con số này, hiệu năng xử lý hoạt họa trên điện thoại sẽ bị suy giảm.

```text
       Thang Đo Nhiệt Kế Trọng Số (Weight Heatmap)
  ┌──────────────────────────────────────────────────────────┐
  │ Xanh Dương (0.0)  →  Xanh Lá (0.5)  →  Đỏ Rực (1.0)      │
  │ Không ảnh hưởng        Uốn cong 50%       Dính chặt 100% │
  └──────────────────────────────────────────────────────────┘
```

---

## 2. Bước Khởi Đầu: Gán Tự Động (With Automatic Weights)

Blender tích hợp sẵn một thuật toán tính toán nhiệt lượng phỏng đoán cực kỳ thông minh:
1. Đảm bảo nhân vật và khung xương đều đã được **`[Ctrl + A] > Apply All Transforms`**.
2. Thứ tự chọn cực kỳ quan trọng:
   * Click chuột trái chọn mô hình **Mesh** trước.
   * Nhấn giữ phím `[Shift]`, click chọn bộ khung xương **Armature** sau cùng.
3. Nhấn tổ hợp phím **`[Ctrl + P]`** để mở menu Parenting.
4. Chọn mục **With Automatic Weights**.

### Điều gì vừa diễn ra ngầm bên trong?
* Một **Armature Modifier** tự động được thêm vào mô hình Mesh.
* Trong bảng thuộc tính **Object Data Properties > Vertex Groups**, Blender tự động sinh ra hàng loạt **Nhóm Đỉnh** có tên trùng khớp 100% với tên của từng chiếc xương (`UpperArm.L`, `Spine`, `Head`...).
* Máy sẽ tự động tính toán khoảng cách từ xương đến các vùng thịt lân cận để tô màu trọng số sơ bộ.

---

## 3. Không Gian Làm Việc Tô Trọng Số (Weight Paint Mode)

Sau khi gán tự động, chắc chắn sẽ có những vùng bị lỗi lem màu (như nhấc tay thì thịt nách bị kéo méo, bước chân thì đũng quần bị dính). Bạn phải tự tay tinh chỉnh lại bằng chế độ **Weight Paint**.

### Cách mở chế độ Weight Paint tương tác thông minh nhất:
1. Ở Object Mode, click chọn bộ xương **Armature**, nhấn `[Ctrl + Tab]` chuyển sang **Pose Mode**.
2. Nhấn giữ phím `[Shift]`, click chọn tiếp phần da thịt **Mesh**.
3. Bấm vào menu chế độ góc trên bên trái đổi sang **Weight Paint**.
4. **Phím tắt vàng:** Bây giờ, bạn chỉ cần nhấn giữ **`[Ctrl] + Click chuột trái`** vào bất kỳ chiếc xương nào, mô hình sẽ lập tức đổi màu nhiệt kế hiển thị chính xác vùng ảnh hưởng của xương đó! Bạn có thể nhấn phím `[R]` xoay xương để thử nghiệm cử động ngay tại chỗ!

---

## 4. Bộ Cọ Vẽ Trọng Số và Kỹ Thuật Làm Mịn Khớp Gập

### 1. Cọ Vẽ Draw (Cộng / Trừ trọng số)
* Trong bảng điều khiển cọ bên trái, thông số **Weight**:
  * Đặt `Weight = 1.0`: Tô thêm màu đỏ (tăng lực kéo).
  * Đặt `Weight = 0.0`: Tương đương với việc tẩy xóa màu đỏ thành màu xanh dương (loại bỏ lực kéo khỏi vùng thịt thừa).
* Thông số **Strength (Lực cọ):** Nên đặt khoảng `0.2` đến `0.3` để phủ từng lớp màu mỏng mềm mại, không nên để 1.0 sẽ bị gắt màu.

### 2. Cọ Làm Mịn Smooth (Làm mượt dải chuyển màu)
* Khi nhấn giữ phím **`[Shift] + quét chuột trái`**, cọ sẽ chuyển sang chế độ làm mịn.
* Hãy quét cọ Smooth dọc theo đường rãnh khuỷu tay và đầu gối. Dải màu chuyển tiếp từ Đỏ sang Vàng $\rightarrow$ Xanh lá $\rightarrow$ Xanh dương sẽ trải đều mượt mà, giúp khớp khi co gập 90 độ giữ nguyên hình trụ tròn trịa, không bị móp dẹt hay gãy gập nhọn hoắt.

---

## 5. Khắc Phục Các Cạm Bẫy Trọng Số Khó Nhằn Nhất

### 1. Lỗi kẽ ngón tay bị lem màu sang nhau:
Khi các ngón tay nằm sát cạnh nhau, nét cọ vẽ ngón trỏ rất dễ bị lem xuyên sang ngón giữa:
* **Khắc phục:** Nhấn phím **`[V]`** để kích hoạt chế độ **Vertex Selection Masking** (Mặt nạ chọn đỉnh). Chỉ những đỉnh đang được chọn sáng lên mới nhận được nét cọ, các ngón tay xung quanh sẽ được bảo vệ tuyệt đối 100%!

### 2. Lỗi cử động chân làm méo mông hoặc chân đối diện:
* Nhấn `[Ctrl + Click]` vào xương đùi `Thigh.L`.
* Nếu thấy vùng háng bên phải hoặc đùi bên phải dính đốm màu xanh lá: Chuyển cọ sang `Weight = 0.0`, quét sạch toàn bộ màu trên nửa người bên phải về màu xanh dương đậm hoàn toàn.

### 3. Lệnh Chuẩn Hóa Thần Thánh (Normalize All):
Sau khi tô vẽ thủ công, tổng trọng số trên các đỉnh có thể bị lệch (lớn hơn 1.0 hoặc nhỏ hơn 1.0):
1. Trên thanh menu trên cùng của Viewport, vào **Weights > Normalize All**.
2. Trong hộp thoại nhỏ góc dưới, chọn mục *Lock Groups: None*, bỏ tích ô *Lock Active*.
3. Blender sẽ tự động cân bằng tỷ lệ toán học trên toàn bộ các đỉnh, đảm bảo tính tương thích tuyệt đối khi xuất mô hình sang Unity!

---

## Bài tập thực hành

**Mục tiêu:** Gán khung xương vào nhân vật và tinh chỉnh hoàn hảo vùng trọng số cho khớp khuỷu tay trái trong 15 phút.

1. Mở file nhân vật đã có khung xương Armature từ Bài 12.
2. Chọn Mesh nhân vật, giữ Shift chọn Armature, nhấn `[Ctrl + P] > With Automatic Weights`.
3. Chọn Armature vào Pose Mode, giữ Shift chọn Mesh chuyển sang **Weight Paint Mode**.
4. Giữ `[Ctrl] + Click` vào xương cẳng tay `Forearm.L`.
5. Nhấn phím `[R]` xoay xương `Forearm.L` gập lên 90 độ (nhân vật co khuỷu tay). Quan sát thấy da thịt vùng khuỷu tay bị méo mó, có thể phần bắp tay bị lẹm hoặc nhọn hoắt.
6. Giữ phím `[Shift]`, dùng cọ quét nhẹ dọc theo vùng rãnh khuỷu tay cả mặt trước lẫn mặt sau để làm mượt dải màu nhiệt kế xanh lá.
7. Đổi cọ sang `Weight = 1.0`, quét dặm nhẹ vào phần cẳng tay gần cổ tay để đảm bảo toàn bộ cẳng tay di chuyển dứt khoát 100% theo xương.
8. Giữ `[Ctrl] + Click` vào xương cánh tay trên `UpperArm.L`, tiếp tục dùng `[Shift] + quét chuột` làm mịn vùng nách và bả vai.
9. Vào menu **Weights > Normalize All**.
10. Nhấn `[Alt + R]` để trả xương về tư thế nghỉ ban đầu. Thử xoay lại lần nữa để kiểm tra chuyển động co duỗi mượt mà không tì vết.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/sculpt_paint/weight_paint/index.html
- https://docs.blender.org/manual/en/5.2/sculpt_paint/weight_paint/tools.html
- https://docs.blender.org/manual/en/5.2/sculpt_paint/weight_paint/editing.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
