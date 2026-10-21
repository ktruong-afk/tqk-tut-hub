# Bài 16: Đưa Nhân Vật Vào Game: Quy Trình Xuất File Chuẩn Sang Unity (glTF 2.0 & FBX)

> **Danh mục:** Tích Hợp Game Engine
> **Tags:** unity, export, gltf, fbx, humanoid, scale, transforms, animation

---

## 1. Đích Đến Cuối Cùng: Đưa Nhân Vật Sống Động Vào Thế Giới Game

Chúc mừng bạn đã đi qua một hành trình phi thường: Từ việc làm quen với những phím tắt đầu tiên, nặn từng khối giải phẫu trong Sculpt Mode, tối ưu lưới với Retopology, trải UV, nướng chất cảm vật liệu PBR, đến việc dựng khung xương và thổi hồn vào từng chuyển động hoạt họa.

Giai đoạn cuối cùng là **Xuất mô hình sang Game Engine Unity (Export to Unity)**. Đây là lúc tác phẩm của bạn bước ra khỏi phần mềm dựng hình để trở thành một nhân vật game thực thụ có thể di chuyển bằng phím `W-A-S-D` hoặc tay cầm chơi game!

```text
  [Blender 5.2]                               [Unity Game Engine]
  • Mesh Low-Poly (15k Quads)                 • Unity Humanoid Rig
  • Armature (.L / .R bones)  ───────────→    • Mecanim Animator Controller
  • PBR Textures (Normal, Albedo)             • Universal Render Pipeline (URP)
  • Action Clips (Idle, Walk)                 • Player Controller C# Script
```

---

## 2. So Sánh Hai Định Dạng Xuất File Chủ Lực: glTF 2.0 vs FBX

| Tiêu Chí | Định dạng glTF 2.0 (.glb) | Định dạng Autodesk FBX (.fbx) |
| :--- | :--- | :--- |
| **Bản quyền & Chuẩn hóa** | Mã nguồn mở quốc tế (Khronos Group) | Định dạng độc quyền của Autodesk |
| **Xử lý trục tọa độ** | Tự động chuyển đổi sang chuẩn Y-up hoàn hảo | Dễ bị lỗi lộn ngược góc xoay X = -90° |
| **Vật liệu PBR** | Đóng gói sẵn vật liệu PBR nguyên bản | Cần trích xuất và gán lại texture thủ công |
| **Tương thích Unity** | Cực kỳ mượt mà qua package glTFast | Là tiêu chuẩn mặc định lâu đời của Unity |
| **Khuyến nghị** | **Lựa chọn hàng đầu cho game hiện đại** | Lựa chọn bắt buộc cho hệ thống Ragdoll cũ |

---

## 3. Bản Kiểm Tra Trước Khi Xuất (Pre-Export Checklist)

> **CẢNH BÁO:** Hơn 90% lỗi biến dạng nhân vật khi nhập vào Unity xuất phát từ việc người học bỏ qua bản kiểm tra 4 bước này trước khi xuất file!

### Bước 1: Khóa sạch biến đổi (Apply All Transforms)
* Trong 3D Viewport ở Object Mode, nhấn phím `[A]` để chọn toàn bộ mô hình Mesh và bộ khung xương Armature.
* Nhấn tổ hợp phím **`[Ctrl + A]`**, chọn mục **All Transforms**.
* Kiểm tra thanh Sidebar `[N] > Item`: Tọa độ Location phải là `(0, 0, 0)`, Rotation phải là `(0°, 0°, 0°)` và quan trọng nhất là **Scale phải bằng đúng `(1.000, 1.000, 1.000)`**.

### Bước 2: Kiểm tra hướng nhìn chính diện (Front View Orientation)
* Nhấn phím `[Numpad 1]` (Front Orthographic). Nhân vật phải đang đứng thẳng và **nhìn thẳng vào mặt bạn** (quay mặt về hướng âm trục Y: `-Y`).
* Nếu nhân vật đang quay mặt sang ngang, hãy xoay lại trong Edit Mode và Apply Rotation.

### Bước 3: Kiểm tra cấu trúc tên xương
* Đảm bảo các xương chân tay đều mang hậu tố `.L` và `.R` chuẩn xác như đã học ở Bài 12 để Unity nhận diện tự động.

### Bước 4: Xóa sạch rác trong cảnh
* Ẩn hoặc xóa bỏ đối tượng Camera, bóng đèn chiếu sáng và khối tượng High-poly điêu khắc. Chỉ giữ lại đúng 2 thành phần: **Mô hình nhân vật (Mesh)** và **Bộ khung xương (Armature)**.

---

## 4. Thiết Lập Xuất File FBX Chuẩn Xác Trong Blender 5.2

Vào menu **File > Export > FBX (.fbx)**. Ở bảng thiết lập bên phải màn hình:

1. **Mục Include:**
   * Tích chọn ô **Selected Objects** (Chỉ xuất những đối tượng đang chọn).
   * Tại mục **Object Types**: Bấm chọn hai biểu tượng **Armature** và **Mesh** (giữ phím Shift để chọn cả hai).
2. **Mục Transform:**
   * Scale: `1.0`.
   * Apply Scalings: Chọn **FBX All**.
   * **BÍ QUYẾT SỐNG CÒN:** Tích chọn ô **! Apply Transform** (dấu chấm than ở đầu). Tùy chọn này sẽ ép góc xoay của Blender tương thích hoàn toàn với hệ trục Y-up của Unity, xóa bỏ triệt để lỗi nhân vật bị ngã ngửa -90 độ!
3. **Mục Armature:**
   * **BẮT BUỘC BỎ TÍCH** ô **Add Leaf Bones**! Nếu bạn quên bỏ tích ô này, Blender sẽ tự ý tạo thêm một đốt xương con thừa thãi cắm ở đầu mỗi ngón tay và ngón chân, làm hỏng cấu trúc khung xương chuẩn của Unity.
4. **Mục Bake Animation:**
   * Tích chọn **Bake Animation**.
   * Tích chọn ô **Key All Bones** và **NLA Strips / All Actions**.
5. Đặt tên file là `Warrior_Hero.fbx` và bấm nút **Export FBX**.

---

## 5. Thiết Lập Xuất File glTF 2.0 (Khuyên Dùng)

Vào menu **File > Export > glTF 2.0 (.glb/.gltf)**:
* **Format:** Chọn **glTF Binary (.glb)** (toàn bộ lưới, xương, texture và hoạt họa sẽ được nén gọn gàng thành một file duy nhất).
* **Include:** Tích chọn **Selected Objects**.
* **Animation:** Mở mục Animation, tích chọn **Group by NLA Track**.
* Bấm **Export glTF 2.0**.

---

## 6. Thiết Lập và Kích Hoạt Nhân Vật Trong Unity

Khởi động dự án Unity Engine của bạn:

```text
┌────────────────────────────────────────────────────────┐
│ BẢNG CẤU HÌNH UNITY INSPECTOR (Tab Rig)                │
├────────────────────────────────────────────────────────┤
│ Animation Type: [Humanoid         ▾]                   │
│ Avatar Definition: [Create From This Model ▾]          │
│                                                        │
│ [Apply]                                                │
│                                                        │
│ Configure... ──→ Mở giao diện kiểm tra xương xanh lá   │
└────────────────────────────────────────────────────────┘
```

1. **Nhập tài nguyên (Import Assets):** Kéo file `Warrior_Hero.fbx` (hoặc `.glb`) và thư mục ảnh texture vào khung cửa sổ `Project > Assets` của Unity.
2. **Cấu hình Xương Humanoid:**
   * Click chọn file mô hình trong cửa sổ Project.
   * Sang bảng **Inspector** bên phải, nhấp vào tab **Rig**.
   * Tại mục **Animation Type**, đổi từ *Generic* sang **Humanoid**.
   * Bấm nút **Apply** ở dưới cùng.
   * Bấm nút **Configure...**: Unity sẽ mở khung kiểm tra hình nộm người que màu xanh lá cây. Nếu các xương đều hiển thị màu xanh lá cây rực rỡ, nghĩa là hệ thống nhận diện xương đạt độ chính xác 100%! Bấm **Done** để quay lại.
3. **Cấu hình Hoạt Họa (Animation Tab):**
   * Chuyển sang tab **Animation** trong Inspector.
   * Chọn clip hành động `Char_Idle_Loop`.
   * Tích chọn ô **Loop Time** (và tích cả *Loop Pose*) để hoạt họa tự động lặp vô tận. Bấm **Apply**.
4. **Cấu hình Vật Liệu (Materials Tab):**
   * Nếu dùng file FBX: Bấm nút **Extract Textures** và **Extract Materials** để Unity giải nén vật liệu ra thư mục con.
   * Chọn file ảnh Normal Map, trong Inspector đổi mục **Texture Type** sang **Normal map**, rồi bấm **Apply** (hoặc nút *Fix Now*).
5. **Kéo nhân vật vào Thế giới Game:**
   * Kéo file nhân vật từ cửa sổ Project thả vào cửa sổ **Scene** hoặc **Hierarchy**.
   * Nhân vật của bạn sẽ xuất hiện sừng sững, bề mặt kim loại phản chiếu ánh sáng lấp lánh, nếp nhăn cơ bắp sắc nét và cử động đứng thở uyển chuyển dưới ánh nắng của thế giới game Unity!

---

## Bài tập thực hành

**Mục tiêu:** Thực hiện toàn bộ quy trình kiểm tra, xuất file và cấu hình nhân vật hoạt họa hoàn chỉnh trong Unity trong 15 phút.

1. Mở file nhân vật hoàn thiện từ các bài học trước trong Blender 5.2.
2. Thực hiện đầy đủ 4 bước của **Pre-Export Checklist**:
   * Nhấn `[A]` chọn tất cả > `[Ctrl + A] > All Transforms`.
   * Nhấn `[Numpad 1]` kiểm tra hướng nhìn chính diện `-Y`.
   * Kiểm tra tên xương đuôi `.L` và `.R`.
3. Vào **File > Export > FBX**:
   * Tích chọn *Selected Objects* (Mesh + Armature).
   * Tích chọn **! Apply Transform**.
   * Bỏ tích **Add Leaf Bones**.
   * Tích chọn *Bake Animation*. Xuất file đặt tên `Hero_GameReady.fbx`.
4. Mở Unity Editor, kéo file `Hero_GameReady.fbx` và các file Texture (`BaseColor.png`, `Normal.png`) vào thư mục `Assets`.
5. Chọn file trong Unity, vào tab **Rig** đổi thành **Humanoid** > Bấm **Apply** > Bấm **Configure** kiểm tra Avatar màu xanh lá cây.
6. Sang tab **Animation**, tích chọn **Loop Time** cho clip Idle > Bấm **Apply**.
7. Kéo nhân vật vào khung cảnh Scene. Nhấn nút **Play ▶️** ở trên đỉnh Unity: Chiêm ngưỡng nhân vật của bạn tự thở và cử động mượt mà bên trong game engine!

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/addons/import_export/scene_gltf2.html
- https://docs.blender.org/manual/en/5.2/addons/import_export/scene_fbx.html
- https://docs.blender.org/manual/en/5.2/scene_layout/object/editing/apply.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
