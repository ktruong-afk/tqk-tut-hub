# Bài 11: Nghệ Thuật Nướng Texture (Texture Baking) và Vẽ Vân Trực Tiếp (Texture Painting)

> **Danh mục:** Chất Cảm & Nướng Texture
> **Tags:** baking, normalmap, texturepainting, cycles, highpoly, lowpoly, unity

---

## 1. Phép Thuật của Kỹ Thuật Nướng Texture (Baking)

Làm thế nào một nhân vật trong game nhập vai hành động trên di động hay máy tính chỉ có vài ngàn mặt đa giác nhưng lại sở hữu từng thớ cơ bắp cuồn cuộn, nếp nhăn đuôi mắt chân thực như một bức tượng điêu khắc triệu đa giác?

Bí mật nằm ở kỹ thuật **Nướng Texture (Baking)**:
* Quá trình đặt mô hình chi tiết cao (**High-Poly**) lồng khít bên trong mô hình lưới thấp (**Low-Poly** đã trải UV).
* Blender sẽ phóng ra hàng triệu tia quét ảo (Bake Rays) từ bề mặt Low-poly bắn vào High-poly để đo đạc độ lồi lõm, sau đó "nướng" toàn bộ thông tin hình học ba chiều đó vào một bức ảnh phẳng hai chiều mang tên **Normal Map (Bản đồ pháp tuyến)**.
* Khi đưa vào game engine Unity, card đồ họa chỉ cần tính toán chuyển động của mô hình nhẹ Low-poly, trong khi ánh sáng chiếu vào sẽ bị đánh lừa bởi tấm Normal Map, tạo nên hiệu ứng thị giác nổi khối 3D sống động như thật mà không hề làm tụt khung hình!

```text
  [Tượng High-Poly]           [Tia quét Baking]           [Lưới Low-Poly + Normal Map]
  3,000,000 Polygons    ──→   Bắn tia thu thập   ──→      12,000 Polygons
  (Chi tiết tối đa)           độ gồ ghề bề mặt            (Nhìn giống hệt High-Poly!)
```

---

## 2. Bản Đồ Pháp Tuyến (Normal Map) Chuẩn Game

Khác với ảnh màu thông thường hay ảnh đen trắng Bump Map, file ảnh Normal Map luôn có một màu **Tím - Xanh ngọc (Purple / Cyan)** đặc trưng:
* Kênh màu **Đỏ (Red):** Đại diện cho độ nghiêng theo phương ngang (Trục X).
* Kênh màu **Xanh lá (Green):** Đại diện cho độ nghiêng theo phương dọc (Trục Y).
* Kênh màu **Xanh lam (Blue):** Đại diện cho độ lồi thẳng góc với bề mặt (Trục Z).

### Tiêu chuẩn OpenGL vs DirectX:
* **OpenGL (Blender & Unity):** Kênh Green quy định chiều dương hướng lên trên (`+Y`).
* **DirectX (Unreal Engine):** Kênh Green quy định chiều dương hướng xuống dưới (`-Y`).
* *Thuận lợi tuyệt vời:* Vì cả Blender và Unity đều cùng dùng chuẩn **OpenGL**, Normal Map nướng từ Blender sẽ tương thích 100% khi đưa thẳng vào Unity mà không cần đảo ngược kênh màu!

---

## 3. Quy Trình Nướng Normal Map Từng Bước Bằng Cycles trong Blender 5.2

> **Ghi nhớ cốt lõi:** Bộ máy EEVEE chỉ chuyên dùng để hiển thị thời gian thực và không hỗ trợ tính năng nướng Texture. Mọi thao tác Bake bắt buộc phải thực hiện trên bộ máy **Cycles**.

### Bước 1: Chuẩn bị hai mô hình
* Đặt mô hình `Character_HighPoly` và `Character_LowPoly` nằm trùng khít lên nhau tại đúng tọa độ gốc `(0, 0, 0)`.
* Đảm bảo mô hình Low-poly đã được trải UV hoàn chỉnh, không có đảo UV nào bị đè chồng lấn lên nhau.

### Bước 2: Tạo ảnh đích trong Shader Editor
1. Chọn mô hình Low-poly, mở không gian làm việc **Shading**.
2. Nhấn `[Shift + A]` thêm node **Texture > Image Texture**.
3. Bấm nút **New**, đặt tên ảnh là `Character_Normal_Bake`:
   * Width & Height: Đặt `2048 x 2048`.
   * Bỏ tích ô *32-bit Float* (để ảnh nhẹ tối ưu cho game).
   * **BẮT BUỘC:** Chuyển mục **Color Space** từ *sRGB* sang **Non-Color**!
4. Nhấp chuột vào node Image Texture này để nó có viền màu trắng sáng xung quanh (trạng thái Active Node). Không cần nối dây node này vào bất kỳ đâu!

### Bước 3: Thiết lập thông số Bake
1. Vào bảng thuộc tính **Render Properties**, đổi **Render Engine** từ *EEVEE* sang **Cycles** (chọn Device: *GPU Compute* nếu máy có card đồ họa rời).
2. Cuộn chuột xuống tìm mục **Bake**:
   * **Bake Type:** Chọn **Normal**.
   * Tích chọn ô **Selected to Active** (Nướng từ đối tượng chọn trước sang đối tượng chọn sau).
   * Mở rộng mục *Selected to Active*, tìm thông số **Extrusion**: Đặt khoảng `0.01m` đến `0.02m` (đây là khoảng cách đẩy phồng lớp vỏ quét để bao bọc trọn vẹn các đỉnh lồi lõm của High-poly).
   * Thông số **Max Ray Distance:** Đặt `0.02m`.

### Bước 4: Thứ tự chọn đối tượng chuẩn xác
1. Trong 3D Viewport hoặc Outliner: Click chuột trái chọn khối `Character_HighPoly` trước.
2. Nhấn giữ phím `[Shift]`, click chọn tiếp khối `Character_LowPoly` sau cùng (lúc này Low-poly sẽ có đường viền màu cam vàng sáng hơn High-poly).
3. Bấm nút **Bake** to lớn trên bảng thuộc tính.
4. Một thanh tiến trình màu xanh sẽ chạy ở mép dưới màn hình. Chờ vài giây đến vài phút tùy độ phân giải.

### Bước 5: Cứu sinh - Lưu ảnh ra đĩa cứng!
* Sau khi nướng xong, mở cửa sổ **Image Editor**, bạn sẽ thấy bức ảnh màu tím hiện lên với đầy đủ chi tiết nếp nhăn.
* **CỰC KỲ QUAN TRỌNG:** Ảnh nướng xong chỉ tạm thời lưu trong bộ nhớ RAM! Bạn BẮT BUỘC phải bấm vào menu **Image > Save As** (hoặc `[Alt + S]`) để lưu file `Character_Normal.png` vào thư mục dự án. Nếu bạn tắt Blender mà quên lưu, bức ảnh sẽ biến mất vĩnh viễn!

---

## 4. Nghệ Thuật Nướng Bản Đồ Che Khuất (Ambient Occlusion - AO Map)

Bản đồ AO là một bức ảnh trắng đen thể hiện độ tối tự nhiên tại các vùng kẹt hẹp nơi ánh sáng khó len lỏi vào (như khóe nách, kẽ ngón tay, nếp gấp cổ áo):
* Vẫn giữ nguyên thiết lập chọn ở trên, chỉ cần đổi **Bake Type** từ *Normal* sang **Ambient Occlusion**.
* Bấm **Bake** để sinh ra một tấm ảnh AO trắng đen.
* Tấm ảnh này khi nạp vào Unity sẽ được nhân (Multiply) với màu da, tạo nên chiều sâu bóng đổ sống động kể cả trên các máy điện thoại cấu hình yếu không bật được bóng đổ thời gian thực.

---

## 5. Vẽ Vân Trực Tiếp Trên Mô Hình 3D (Texture Painting)

Sau khi có lưới và texture nền, bạn có thể tự tay vẽ thêm má hồng, hình xăm, vết sẹo hoặc vết rỉ sét trực tiếp lên mô hình bằng tab **Texture Paint**:
* **Paint Slots:** Chọn gán cọ vẽ trực tiếp vào kênh *Base Color*.
* Phím `[F]`: Đổi kích thước cọ vẽ.
* Phím `[Shift + F]`: Đổi lực đậm nhạt của nét cọ.
* Phím `[X]`: Đổi qua lại giữa màu vẽ chính và màu vẽ phụ.
* Công cụ **Soften Brush / Smear Brush:** Dùng để miết và làm nhòe chuyển sắc (tuyệt vời để vẽ chuyển màu son môi và má hồng nhân vật).

---

## Bài tập thực hành

**Mục tiêu:** Nướng một tấm Normal Map từ một khối đá điêu khắc chi tiết cao sang một khối hộp Low-poly phẳng lì trong 15 phút.

1. Tạo khối Cube, nhấn `[Ctrl + 3]` thêm Subdivision Surface rồi Apply thành khối cầu. Điêu khắc các vết rạch sâu nứt nẻ bằng cọ Crease trong Sculpt Mode. Đặt tên là `Rock_HighPoly`.
2. Tạo một khối lập phương **Cube** mới đặt trùng tọa độ với khối đá, nhấn `[Tab]` trải nhanh UV bằng lệnh `[U] > Smart UV Project`. Đặt tên là `Rock_LowPoly`.
3. Mở Shader Editor cho `Rock_LowPoly`, tạo một node **Image Texture** mới kích thước `1024 x 1024`, Color Space chọn `Non-Color`, đặt tên `Rock_Normal_Map`.
4. Đổi Render Engine sang **Cycles**, mở mục Bake, chọn Bake Type là **Normal**, tích bật **Selected to Active**, chỉnh `Extrusion = 0.03m`.
5. Chọn `Rock_HighPoly` trước, giữ Shift chọn `Rock_LowPoly` sau. Bấm nút **Bake**.
6. Sau khi nướng xong, trong Shader Editor của Low-poly: Nối cổng *Color* của node ảnh vào cổng *Color* của node **Normal Map**, rồi nối cổng *Normal* của node Normal Map vào cổng *Normal* của **Principled BSDF**.
7. Ẩn khối High-poly đi: Thưởng thức khối hộp Low-poly phẳng lì bỗng chốc hiện lên toàn bộ các vết nứt đá nẻ lồi lõm chân thực đến kinh ngạc! Lưu ảnh bằng **Image > Save As**.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/render/cycles/baking.html
- https://docs.blender.org/manual/en/5.2/sculpt_paint/painting/texture_paint/index.html
- https://docs.blender.org/manual/en/5.2/render/shader_nodes/vector/normal_map.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
