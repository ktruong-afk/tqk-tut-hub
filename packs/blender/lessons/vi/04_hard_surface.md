# Bài 04: Kỹ Thuật Dựng Hình Bề Mặt Cứng (Hard Surface Modeling) Cho Phụ Kiện & Giáp Trụ

> **Danh mục:** Dựng Hình Chuyên Sâu
> **Tags:** hardsurface, bevel, boolean, looptools, armor, weapon, topology

---

## 1. Khái niệm Hard Surface và Tầm quan trọng trong Thiết kế Nhân vật Game

Trong quy trình tạo hình nhân vật 3D cho video game, bạn sẽ phải đối mặt với hai trường phái dựng hình đối lập:
* **Organic Modeling (Bề mặt hữu cơ):** Da thịt, cơ bắp, khuôn mặt, nếp gấp vải vóc mềm mại – thường được xử lý tối ưu bằng phương pháp Điêu Khắc (Sculpting).
* **Hard Surface Modeling (Bề mặt cứng):** Các bộ phận nhân tạo có bề mặt phẳng lì, gờ cạnh kim loại sắc nét, đường cắt cơ khí chính xác như giáp trụ (Armor), nón bảo hiểm (Helmet), vũ khí (Weapons), khớp nối robot (Cyborg/Mecha) và phụ kiện trang sức.

Hard Surface đòi hỏi tư duy kiểm soát **Dòng chảy cạnh (Edge Flow)** và **Pháp tuyến bề mặt (Normals)** cực kỳ khắt khe để đảm bảo ánh sáng phản chiếu trên kim loại không bị gợn sóng (Waviness) hay bóng tối loang lổ (Shading Artifacts).

---

## 2. Kỹ thuật Cạnh Hỗ Trợ (Support Loops / Control Loops)

Khi áp dụng bộ điều chỉnh Subdivision Surface lên một khối hộp vuông thô, thuật toán sẽ bo tròn toàn bộ các góc khiến khối lập phương biến thành một hình cầu méo mó. Để duy trì góc cạnh sắc sảo theo ý muốn, bạn phải dùng kỹ thuật **Cạnh Hỗ Trợ (Support Loops)**:

* **Nguyên lý khoảng cách:** Càng đặt hai cạnh nằm sát gần nhau, thuật toán Subsurf càng bị giới hạn không gian làm cong, tạo ra một đường vát cạnh siêu sắc nét. Ngược lại, hai cạnh nằm xa nhau sẽ tạo ra độ chuyển tiếp cong mềm.
* **Quy tắc 3 Cạnh (The Rule of Three):** Mỗi đường gờ cứng cáp trong Hard Surface lý tưởng nhất nên được tạo bởi một cạnh trung tâm và hai cạnh hỗ trợ kẹp hai bên.

```text
  [Support Loop 1] ───┐
  [Cạnh Chính]     ───┼──→ Góc bo siêu sắc nét, bóng đổ hoàn hảo
  [Support Loop 2] ───┘
```

---

## 3. Ba Kỹ Thuật Hard Surface Đỉnh Cao

### 1. Kỹ thuật Khoét Lỗ Tròn Hoàn Hảo (Perfect Circular Holes)
Khoét một chiếc ốc vít hoặc lỗ thông gió tròn trịa trên một tấm giáp phẳng mà không làm nát lưới Quad là một trong những bài test kinh điển của nghệ sĩ 3D:
1. Trong Edit Mode, tạo một lưới vuông tối thiểu 3x3 hoặc 4x4 ô bằng Loop Cut `[Ctrl + R]`.
2. Chọn 4 mặt vuông nằm ở tâm vị trí muốn khoét lỗ.
3. Nhấn `[I]` (Inset) lùi vào một khoảng nhỏ 10% để làm **Vòng viền bảo vệ (Holding Edge)**. Bước này bắt buộc phải có để ngăn hiện tượng méo mặt phẳng xung quanh khi uốn cong.
4. Kích hoạt Add-on tích hợp sẵn: Vào **Edit > Preferences > Add-ons**, gõ `LoopTools` và tích chọn bật.
5. Nhấp chuột phải lên vùng mặt đang chọn, vào menu **LoopTools > Circle**. 4 mặt vuông sẽ tức thì biến đổi thành một đường tròn đa giác hoàn hảo!
6. Nhấn `[E]` đùn lỗ lõm sâu vào trong thân giáp.

### 2. Quy trình Boolean Sạch Sẽ (Clean Boolean Workflow)
Đục khoét các khe rãnh cơ khí tinh xảo bằng Modifier Boolean:
1. Luôn nhấn `[Ctrl + A] > Apply Scale` trên cả vật thể chính và khối dùng để cắt trước khi thực hiện Boolean.
2. Thêm **Boolean Modifier** lên tấm giáp, chọn chế độ **Difference**, chỉ định vật thể cắt và chọn bộ giải **Exact**.
3. Để dễ quan sát nhát cắt trong không gian 3D: Chọn vật thể dùng để cắt, vào thẻ **Object Properties** (biểu tượng hình vuông màu cam) > **Viewport Display** > mục **Display As** đổi từ *Textured* sang **Wire** (khung dây trong suốt).
4. Sau khi áp dụng (Apply) modifier Boolean, các đỉnh nối tại vết cắt thường sinh ra mặt N-gon. Dùng ngay dao cắt **Knife `[K]`** hoặc phím **Connect `[J]`** để kéo các đỉnh này nối về các góc cạnh chính gần nhất, giải phóng lưới về toàn bộ mặt Quad 4 cạnh.

### 3. Điều Khiển Bo Góc Bằng Trọng Số (Edge Bevel Weight)
Thay vì bo góc tất cả các cạnh theo một góc độ chung chung, bạn có thể chỉ định chính xác cạnh nào bo to, cạnh nào bo nhỏ:
1. Vào Edit Mode, chọn các đường gờ chính muốn tạo điểm nhấn sắc sảo.
2. Mở thanh Sidebar `[N]`, trong thẻ **Item**, tìm thông số **Edge Bevel Weight** và kéo lên giá trị `1.0` (cạnh được chọn sẽ chuyển sang màu xanh dương nổi bật).
3. Quay lại bảng Modifiers, thêm **Bevel Modifier**:
   * Tại mục **Limit Method**: Chuyển từ *Angle* sang **Weight**.
   * Bây giờ, Bevel Modifier sẽ chỉ tập trung bo tròn chính xác những cạnh có trọng số xanh dương, bỏ qua toàn bộ các cạnh còn lại của mô hình.

---

## 4. Pháp Tuyến Trọng Số (Weighted Normal Modifier) – Bí quyết của Game AAA

Khi bạn bật chế độ làm mượt bề mặt (Shade Smooth by Angle) trên các bề mặt vát cạnh của giáp trụ, ánh sáng thường bị kéo nghiêng từ mặt phẳng lớn sang góc bo hẹp, tạo ra các quầng bóng đổ đen xì nhăn nhó ở tâm mặt phẳng (Shading Gradient Error).

* **Giải pháp cứu cánh:** Thêm bộ điều chỉnh **Weighted Normal Modifier** vào cuối ngăn xếp modifier.
* **Nguyên lý hoạt động:** Thuật toán tính toán lại hướng pháp tuyến bề mặt (Normals) dựa trên diện tích của từng mặt đa giác. Mặt phẳng có diện tích lớn sẽ chiếm trọng số áp đảo, ép hướng chiếu sáng của mặt phẳng luôn vuông góc tuyệt đối, đồng thời dồn toàn bộ độ cong chuyển tiếp về dải vát cạnh Bevel nhỏ xíu.
* **Kết quả:** Tấm giáp trông phẳng lỳ bóng loáng như render hàng triệu đa giác, trong khi số lượng mặt thực tế cực kỳ thấp, đạt chuẩn tối ưu hiệu năng cho game engine Unity!

---

## Bài tập thực hành

**Mục tiêu:** Dựng một miếng giáp vai cơ khí phong cách Sci-Fi có rãnh viền bo góc sắc bén và 2 cổng thông hơi tròn trong 15 phút.

1. Tạo một khối lập phương **Cube**, chuyển sang Edit Mode, thu nhỏ chiều dày trục X để tạo thành một tấm giáp phẳng kích thước `0.05m x 0.6m x 0.8m`.
2. Dùng `[Ctrl + R]` cắt đôi giáp theo chiều dọc, nhấn `[G] + [X]` đẩy nhẹ đường sống giữa nhô cao lên để tạo sống giáp chữ V góc cạnh.
3. Chuyển sang Object Mode, nhấn `[Ctrl + A] > Apply Scale`.
4. Tạo cổng thoát khí tròn: Chọn 4 mặt ở góc trên tấm giáp, nhấn `[I]` chèn mặt bảo vệ, nhấp chuột phải chọn **LoopTools > Circle**.
5. Nhấn `[E]` đùn lỗ tròn thụt sâu vào trong `0.03m`. Nhấn `[I]` lùi thêm một nấc nhỏ ở đáy lỗ rồi nhấn `[E]` đùn xuyên thủng ra phía sau.
6. Quay lại Object Mode, thêm **Bevel Modifier**:
   * Chỉnh `Amount = 0.01m`, `Segments = 3`.
   * Mục *Limit Method* chọn **Angle** (`30°`).
   * Mục *Geometry > Miter Outer* chọn **Arc**.
   * Trong mục *Shading*: Tích chọn **Harden Normals**.
7. Thêm tiếp **Weighted Normal Modifier** ngay phía dưới Bevel, tích chọn ô **Keep Sharp**.
8. Nhấp chuột phải lên tấm giáp chọn **Shade Smooth by Angle**. Quan sát bề mặt kim loại phẳng lỳ sắc sảo không còn một gợn bóng lỗi nào.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/modeling/modifiers/modify/weighted_normal.html
- https://docs.blender.org/manual/en/5.2/modeling/modifiers/generate/bevel.html
- https://docs.blender.org/manual/en/5.2/modeling/meshes/editing/edge/edge_data.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
