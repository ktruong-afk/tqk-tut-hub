# Bài 09: Trải Tọa Độ UV (UV Unwrapping) và Tối Ưu Mật Độ Điểm Ảnh (Texel Density)

> **Danh mục:** Trải UV & Vật Liệu
> **Tags:** uvediting, unwrap, seam, texeldensity, islands, packing, unity

---

## 1. Bản Chất của Bản Đồ Tọa Độ UV (UV Mapping)

Card đồ họa không thể dán trực tiếp một bức ảnh phẳng 2D lên một khối nhân vật 3D cong queo nếu không có một "bản đồ chỉ dẫn". **Trải UV (UV Unwrapping)** là quá trình cắt rạch và mở phẳng toàn bộ bề mặt hình học 3D ra một không gian phẳng 2D có hệ trục tọa độ mang tên `U` (ngang) và `V` (dọc).

Hãy liên tưởng UV như việc một người thợ may cắt rời các mảnh vải của một chiếc áo rồi trải phẳng trên bàn:
* Bề mặt 3D được cắt tách thành các mảnh độc lập gọi là **Đảo UV (UV Islands)**.
* Các đường ranh giới cắt rời được gọi là **Đường Khâu (Seams)**.
* Toàn bộ các đảo UV phải được gói ghém ngăn nắp vào bên trong một ô vuông giới hạn từ `(0, 0)` đến `(1, 1)` đại diện cho file ảnh Texture hoàn chỉnh.

```text
       Mô Hình 3D                              Bản Đồ UV 2D (0.0 đến 1.0)
     ┌────────────┐                            ┌─────────────────────────┐
     │  (Đầu gối, │     Trải phẳng theo Seam   │ [Mặt Trước]   [Mặt Sau] │
     │  cánh tay) │   ───────────────────────→ │                         │
     │            │                            │ [Cánh Tay]    [Bàn Tay] │
     └────────────┘                            └─────────────────────────┘
```

---

## 2. Nghệ Thuật Đặt Đường Khâu (Marking Seams)

Nếu bạn không đánh dấu đường khâu mà nhấn lệnh Unwrap ngay lập tức, Blender sẽ cố gắng ép bẹp khối 3D như giẫm nát một quả bóng cao su, khiến các mặt bị co rúm và méo mó thảm hại.

### Thao tác tạo và xóa Seam trong Edit Mode:
* Chuyển sang chế độ chọn cạnh bằng phím `[2]`.
* Chọn các cạnh muốn làm đường cắt, nhấn chuột phải (hoặc nhấn `[Ctrl + E]`) chọn **Mark Seam**. Các cạnh được chọn sẽ đổi sang màu đỏ rực rỡ báo hiệu đường cắt.
* Nếu muốn hủy đường cắt: Chọn cạnh, nhấn chuột phải chọn **Clear Seam**.

### Ba nguyên tắc vàng khi chọn vị trí đặt Seam cho nhân vật:
1. **Luôn giấu Seam vào góc khuất thị giác:**
   * Cánh tay: Đặt đường Seam chạy dọc theo mặt dưới cánh tay (hướng úp vào trong nách).
   * Chân: Đặt đường Seam chạy dọc theo mặt trong của đùi kéo xuống mắt cá chân.
   * Thân người: Đặt đường Seam chạy dọc theo hai bên hông sườn và đũng quần.
2. **Quy tắc cắt phần Đầu Nhân Vật (The Baseball Stitch):**
   * Cắt một đường vòng tròn khép kín quanh vành tai để tách rời đôi tai ra thành 2 đảo UV riêng.
   * Cắt một đường rạch từ hõm sau gáy chạy thẳng lên đỉnh đầu (vùng này về sau sẽ được tóc che khuất hoàn toàn).
   * Cắt mở đường viền dưới đáy cằm.
3. **Tách rời các vật liệu khác biệt:** Những vị trí ranh giới giữa kim loại và vải, giữa giáp và da thịt nên được tách thành các đảo UV riêng biệt để việc nướng chất cảm vật liệu không bị lem màu.

---

## 3. Lệnh Trải UV và Kiểm Tra Độ Biến Dạng (UV Distortion)

Sau khi đã đánh dấu đầy đủ các đường Seam:
1. Nhấn phím `[A]` để chọn toàn bộ lưới trong Edit Mode.
2. Nhấn phím **`[U]`** để mở menu Unwrap, chọn mục đầu tiên: **Unwrap**.
3. Chuyển sang không gian làm việc **UV Editing** ở thanh trên cùng để quan sát các đảo UV bên cửa sổ UV Editor.

### Kiểm tra co dãn bề mặt (Display Stretch):
Trong cửa sổ UV Editor, bấm vào biểu tượng mũi tên cạnh **Overlays** góc trên bên phải, tích chọn ô **Display Stretch**:
* **Màu Xanh Dương Đậm (Dark Blue):** Hoàn hảo! Tỷ lệ diện tích trên 2D hoàn toàn tương đồng với 3D, không bị co dãn.
* **Màu Xanh Lá Cây (Green):** Chấp nhận được đối với các vùng cong phức tạp.
* **Màu Vàng / Đỏ (Yellow / Red):** Bị kéo dãn hoặc nén ép nghiêm trọng! Cần thêm đường Seam giải tỏa áp lực ở khu vực đó.

---

## 4. Mật Độ Điểm Ảnh (Texel Density) – Yếu Tố Quyết Định Độ Nét

**Texel Density (TD)** là số lượng điểm ảnh (pixels) của texture được phân bổ trên một đơn vị chiều dài thực tế của vật thể 3D (thường đo bằng `Pixels/Meter` hoặc `Pixels/Centimeter`).

### Quy tắc Texel Density cho Game:
* Nếu một nhân vật sử dụng chung một tấm ảnh Texture kích thước `2048 x 2048`:
  * Khuôn mặt nhân vật phải chiếm **tối thiểu 30% đến 40%** diện tích tấm ảnh vì camera trong game thường xuyên quay cận cảnh hội thoại.
  * Lưng áo, đế giày hoặc lòng bàn tay có thể thu nhỏ tỷ lệ đảo UV để nhường diện tích điểm ảnh cho khuôn mặt.
* Không bao giờ để một bộ phận có hạt texture to thô lỗ (vỡ hạt) nằm ngay cạnh một bộ phận có hạt texture siêu mịn. Mọi đảo UV cùng nhóm vật liệu phải có Texel Density tương đối đồng đều.

---

## 5. Sắp Xếp Đảo UV (UV Packing) và Khoảng Đệm (Margin)

Khi các đảo UV đã được trải phẳng, bạn phải sắp xếp chúng gọn gàng khít khao vào trong khung vuông `(0 đến 1)`:
* Trong UV Editor, nhấn `[A]` chọn tất cả các đảo UV.
* Vào menu **UV > Pack Islands** (hoặc nhấn `[Ctrl + P]`).
* **Thông số Margin (Khoảng cách an toàn giữa các đảo):**
  * Tuyệt đối không để hai đảo UV chạm sát dính vào nhau!
  * Khi xuất vào game engine Unity, engine sẽ tự động sinh ra các mức phân giải nhỏ hơn gọi là **Mipmaps**. Nếu không có khoảng đệm, màu của áo sẽ bị lem sang da mặt khi người chơi đứng ở khoảng cách xa (hiện tượng *Texture Bleeding*).
  * Đối với texture `2048 x 2048`, hãy đặt **Margin = 0.008** đến **0.01** (tương đương khoảng cách tối thiểu 16 pixels giữa các đảo).

---

## Bài tập thực hành

**Mục tiêu:** Đánh dấu Seam và trải phẳng hoàn chỉnh một chiếc mũ sắt chiến binh (Helmet) không bị méo hạt trong 15 phút.

1. Tạo một khối lập phương **Cube**, thêm **Subdivision Surface Modifier** cấp độ 2, nhấn `[Ctrl + A]` để Apply thành khối cầu tròn có cấu trúc Quad sạch.
2. Vào Edit Mode, nhấn `[3]` chọn các mặt ở nửa dưới phía trước xóa đi để tạo hốc mở mặt cho mũ bảo hiểm.
3. Thêm **Solidify Modifier** tạo độ dày vỏ mũ `0.02m`, sau đó Apply modifier.
4. Đánh dấu đường Seam:
   * Chọn vòng cạnh viền hốc mặt, nhấp chuột phải chọn **Mark Seam** (để tách mặt ngoài và mặt trong).
   * Chọn dải cạnh chạy dọc sống đầu từ trán qua đỉnh đầu ra sau gáy, chọn **Mark Seam** (để giải phóng áp lực làm cong của vòm mũ).
5. Nhấn `[A]` chọn toàn bộ mũ, nhấn phím `[U] > Unwrap`.
6. Sang không gian **UV Editing**: Bật tính năng **Display Stretch**, kiểm tra thấy các đảo UV hiển thị màu xanh dương thư thái.
7. Nhấn `[Ctrl + P]` chọn **Pack Islands**, đặt `Margin = 0.01` và tích chọn `Rotate` để máy tự động xoay và tối ưu hóa diện tích khung hình chữ nhật.
8. Gán một vật liệu mới với hoa văn caro **Checker Texture** để chiêm ngưỡng các ô vuông bàn cờ trải đều đặn sắc nét trên thân mũ.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/editors/uv/index.html
- https://docs.blender.org/manual/en/5.2/modeling/meshes/uv/unwrapping/seams.html
- https://docs.blender.org/manual/en/5.2/editors/uv/uv_settings.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
