# Bài 03: Khai Thác Hệ Thống Bộ Điều Chỉnh (Modifiers) Cốt Lõi trong Blender 5.2

> **Danh mục:** Bộ Điều Chỉnh & Modifiers
> **Tags:** modifiers, subdivision, mirror, solidify, bevel, array, boolean, blender52

---

## 1. Triết lý Thiết kế Phi Phá Hủy (Non-Destructive Modeling)

Trong môi trường phát triển game chuyên nghiệp, khả năng chỉnh sửa linh hoạt theo phản hồi của đạo diễn hình ảnh là yếu tố sống còn. **Bộ Điều Chỉnh (Modifiers)** trong Blender 5.2 là hệ thống các thuật toán tính toán tự động tác động lên hình học của vật thể nhưng **không làm thay đổi cấu trúc lưới gốc** cho đến khi bạn quyết định Áp Dụng (Apply) chúng.

Ví dụ: Bạn có thể dựng một chiếc giáp vai nhân vật chỉ bằng 20 mặt đa giác thô sơ, sau đó dùng các Modifier để tự động làm dày lên 5mm, bo tròn các góc nhọn và phân mịn bề mặt thành hàng ngàn đa giác. Bất kỳ lúc nào, bạn vẫn có thể quay lại sửa đổi 20 mặt đa giác gốc mà không phải nắn sửa hàng ngàn đỉnh phức tạp.

---

## 2. Quy tắc Ngăn Xếp Bộ Điều Chỉnh (Modifier Stack Order)

Toàn bộ các bộ điều chỉnh được quản lý trong tab hình chiếc cờ lê (**Modifier Properties**) ở bảng điều khiển Properties bên phải.
* **Nguyên lý dòng chảy dữ liệu:** Các modifier hoạt động theo thứ tự **từ trên xuống dưới**. Kết quả hình học được tính toán ở modifier phía trên sẽ trở thành dữ liệu đầu vào cho modifier nằm ngay bên dưới.
* **Tác động của việc tráo đổi vị trí:**
  * Nếu đặt **Bevel** trước **Subdivision Surface**: Cạnh sẽ được bo góc trước, sau đó thuật toán Subsurf làm mịn toàn bộ khối $\rightarrow$ cho ra góc bo mượt mà tự nhiên.
  * Nếu đặt **Subdivision Surface** trước **Bevel**: Lưới bị chia dày đặc trước, sau đó lệnh Bevel cố gắng vát trên hàng triệu cạnh nhỏ $\rightarrow$ gây nặng máy và tạo lỗi co rút bề mặt.

```text
┌──────────────────────────────────────────────┐
│ Modifier Stack: Dòng tính toán từ TRÊN xuống │
├──────────────────────────────────────────────┤
│ 1. Mirror (Đối xứng nửa người trái sang phải)│
│    ↓ Dữ liệu lưới được nhân bản              │
│ 2. Solidify (Tạo độ dày cho giáp ngực)       │
│    ↓ Dữ liệu lưới có thêm mặt trong          │
│ 3. Bevel (Bo tròn các đường mép giáp)        │
│    ↓ Dữ liệu mép được vát cong               │
│ 4. Subdivision Surface (Làm mịn toàn bộ)     │
└──────────────────────────────────────────────┘
```

---

## 3. Sáu Bộ Điều Chỉnh Cốt Lõi cho Nhân Vật & Đạo Cụ Game

### 1. Bề Mặt Phân Mịn (Subdivision Surface - Phím tắt nhanh `[Ctrl + 1/2/3]`)
Thuật toán chia nhỏ từng mặt đa giác thành 4 mặt con đồng thời làm tròn các góc cạnh dựa trên phương pháp Catmull-Clark:
* **Levels Viewport:** Mức độ chia nhỏ hiển thị trong viewport khi làm việc (thường để mức `1` hoặc `2` để giữ khung hình mượt mà).
* **Render:** Mức độ phân mịn khi kết xuất ảnh hoặc nướng texture (có thể đặt `3` hoặc `4`).
* **Độ gập nếp cạnh (Mean Crease - `[Shift + E]`):** Trong Edit Mode, bạn chọn các cạnh và nhấn `[Shift + E]` để kéo giá trị Crease từ `0.0` đến `1.0`. Cạnh có Crease cao sẽ giữ nguyên độ sắc nhọn mà không bị làm tròn cong bởi Subsurf.

### 2. Đối Xứng Gương (Mirror Modifier)
Cho phép bạn chỉ cần dựng một nửa khuôn mặt hoặc nửa thân nhân vật, nửa còn lại sẽ tự động được sinh ra đối xứng qua trục:
* **Axis (Trục đối xứng):** Mặc định là trục `X` (Trái - Phải).
* **Clipping (Khóa dính ranh giới):** Luôn bật tính năng này! Nó ngăn các đỉnh nằm ở đường sống giữa (trục đối xứng) không bị kéo tách rời sang hai bên hoặc lấn đè chéo qua nhau.
* **Merge:** Tự động hàn gắn các đỉnh ở ranh giới giữa hai nửa đối xứng nếu khoảng cách nhỏ hơn ngưỡng dung sai.

### 3. Tạo Độ Dày Vỏ (Solidify Modifier)
Biến một bề mặt 2D mỏng dính thành một tấm giáp hoặc lớp áo có độ dày vật lý:
* **Thickness (Độ dày):** Khoảng cách đùn bề mặt (ví dụ `0.02m` cho áo vải, `0.05m` cho giáp kim loại).
* **Even Thickness (Độ dày đồng đều):** Giúp duy trì độ dày cố định ở các góc nhọn gấp khúc, tránh bị móp méo mép.
* **Offset:** `-1.0` để đùn độ dày vào phía trong, `1.0` để đùn nở ra phía ngoài bề mặt gốc.

### 4. Bo Tròn Tự Động (Bevel Modifier)
Tự động làm mềm các góc sắc nhọn trên toàn bộ mô hình mà không cần chém lưới thủ công:
* **Amount:** Bề rộng của vát mép.
* **Segments:** Số phân đoạn tròn (thường dùng `2` hoặc `3` phân đoạn).
* **Limit Method (Phương pháp giới hạn mép vát):**
  * `Angle (Theo góc):` Chỉ vát những cạnh có góc gấp lớn hơn góc chỉ định (mặc định là `30°`).
  * `Weight (Theo trọng số):` Trong Edit Mode, bạn tự tay đánh dấu thông số **Bevel Weight** trên những cạnh muốn bo tròn.
* **Harden Normals (Làm cứng pháp tuyến):** Nằm trong mục *Shading*. Khi bật tính năng này, mặt phẳng sẽ giữ nguyên bóng phẳng tuyệt đối, tránh hiện tượng bóng tối loang lổ quanh mép bo.

### 5. Mảng Lặp (Array Modifier)
Tạo ra chuỗi các bản sao lặp lại liên tiếp theo quy luật:
* **Count:** Số lượng đối tượng sinh ra.
* **Relative Offset (Độ dịch chuyển tương đối):** Đặt theo tỷ lệ kích thước của vật thể (ví dụ `X = 1.0` nghĩa là bản sao tiếp theo nằm ngay sát mép bản sao trước).
* **Object Offset:** Dùng vị trí và góc xoay của một đối tượng phụ (thường là một Empty) để điều khiển. Khi xoay Empty 30 độ, các bản sao của Array sẽ tự động uốn thành một vòng tròn hoàn hảo (rất hữu ích để xếp ổ đạn, vòng gai, hoa văn đai giáp).

### 6. Hàn Ghép & Đục Khối Giao Nhau (Boolean Modifier)
Sử dụng hình học của vật thể này để cắt gọt hoặc hợp nhất với vật thể khác:
* **Difference (Hiệu - Đục lỗ):** Lấy vật thể chính trừ đi phần thể tích giao nhau với vật thể cắt.
* **Union (Hợp):** Nối hai vật thể lại thành một khối liền mạch duy nhất và tự động loại bỏ các mặt nằm bên trong.
* **Intersect (Giao):** Chỉ giữ lại phần thể tích giao nhau chung giữa hai vật thể.
* **Solver (Bộ giải toán):**
  * `Exact:` Độ chính xác toán học cực cao, xử lý được các bề mặt phức tạp nhưng tính toán chậm hơn.
  * `Fast:` Xử lý chớp nhoáng, thích hợp cho các khối hình học đơn giản.

---

## 4. Bộ điều chỉnh Làm Mượt Theo Góc (Smooth by Angle) trong Blender 5.2

> **Cập nhật quan trọng trong Blender 5.2:** Tính năng "Auto Smooth" cũ trong thẻ Mesh Data đã được thay thế hoàn toàn bằng phương pháp hiện đại: Bộ điều chỉnh **Smooth by Angle** (được đóng gói dưới dạng Geometry Nodes Modifier thông minh).

* Khi bạn nhấp chuột phải vào vật thể ở Object Mode và chọn **Shade Smooth by Angle**, Blender 5.2 sẽ tự động gắn bộ điều chỉnh **Smooth by Angle** vào ngăn xếp.
* **Nguyên lý:** Thuật toán đo góc giữa pháp tuyến của hai mặt láng giềng. Nếu góc nhỏ hơn ngưỡng quy định (mặc định `30°`), bề mặt sẽ được làm mượt mềm mại. Nếu góc lớn hơn `30°`, cạnh sẽ hiển thị sắc nét (Sharp Edge).
* Bạn có thể điều chỉnh thanh trượt **Angle** trong bảng Modifiers bất kỳ lúc nào để quyết định độ sắc của các đường gân nhân vật.

---

## 5. Khi nào nên Áp Dụng (Apply) Modifier?

* **NÊN GIỮ NGUYÊN (Không Apply):** Khi đang trong quá trình thử nghiệm ý tưởng, nặn dáng nhân vật hoặc cần giữ file nhẹ nhàng.
* **BẮT BUỘC APPLY `[Ctrl + A]`:**
  1. Trước khi chuyển sang chế độ **Sculpt Mode** (vì cọ điêu khắc cần cấu trúc đa giác thực để tác động trực tiếp).
  2. Trước khi tiến hành **Trải UV (UV Unwrapping)** và **Gắn Xương (Rigging)**.
  3. Trước khi xuất file định dạng `.fbx` sang Unity nếu các modifier làm thay đổi phân cấp khung xương.

---

## Bài tập thực hành

**Mục tiêu:** Ứng dụng kết hợp Mirror, Solidify, Bevel và Array để dựng một tấm khiên tròn phong cách chiến binh giả tưởng trong 15 phút.

1. Xóa khối Cube mặc định. Nhấn `[Shift + A]` > **Mesh > Circle** (đặt số cạnh `Vertices = 16`).
2. Nhấn `[Tab]` vào Edit Mode. Nhấn `[F]` để lấp đầy hình tròn thành một mặt phẳng.
3. Nhấn `[I]` (Inset) lùi vào trong một vòng nhỏ, nhấn `[G] + [Y]` (hoặc Z) đẩy lồi nhẹ tâm hình tròn ra ngoài để tạo mặt khiên cong hình vòm.
4. Chuyển sang Object Mode. Thêm **Solidify Modifier**, chỉnh `Thickness = 0.04m` để tạo độ dày cho thân khiên.
5. Thêm tiếp **Bevel Modifier** ngay phía dưới Solidify: Đặt `Amount = 0.008m`, `Segments = 2`, Limit Method chọn `Angle (30°)`.
6. Nhấp chuột phải lên khiên chọn **Shade Smooth by Angle** để bề mặt cong mịn nhưng mép viền sắc nét.
7. Tạo đinh tán trang trí cho vành khiên: Nhấn `[Shift + A]` tạo một khối cầu **Icosphere**, thu nhỏ kích thước xuống `0.03m` và đặt ở mép trên cùng của vành khiên.
8. Nhấn `[Shift + A]` > **Empty > Plain Axes** đặt ngay tại tâm tấm khiên `(0, 0, 0)`.
9. Chọn khối đinh tán, thêm **Array Modifier**:
   * Tắt ô *Relative Offset*.
   * Tích chọn ô **Object Offset**, bấm bút nhỏ chỉ định vào đối tượng *Empty* vừa tạo.
   * Chỉnh số lượng `Count = 8`.
10. Chọn đối tượng *Empty*, nhấn `[R] + [Z]`, gõ `45` độ và nhấn `Enter` `(360° / 8 = 45°)`. Quan sát 8 chiếc đinh tán tự động tỏa đều quanh vành khiên một cách hoàn hảo.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/modeling/modifiers/index.html
- https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/subdivision_surface.html
- https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/mirror.html
- https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/smooth_by_angle.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
