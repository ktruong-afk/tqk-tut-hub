# Bài 12: Kỹ Thuật Gắn Xương Hoạt Họa (Rigging Cơ Bản) Cho Nhân Vật Game

> **Danh mục:** Gắn Xương & Hoạt Họa
> **Tags:** rigging, armature, bones, hierarchy, naming, roll, ik, unity

---

## 1. Bản Chất của Quá Trình Rigging Nhân Vật

Sau khi bạn đã hoàn thành mô hình lưới Low-poly và nướng chất cảm vật liệu, nhân vật hiện tại vẫn chỉ là một bức tượng bất động. **Gắn Xương (Rigging)** là công đoạn cấy một hệ thống khung xương kỹ thuật số (**Armature**) vào bên trong cơ thể nhân vật, thiết lập quan hệ phân cấp gia đình (Parent - Child) và các khớp xoay cơ học để người làm hoạt họa có thể điều khiển nhân vật chạy, nhảy, múa kiếm một cách linh hoạt.

Bộ khung xương dựng trong Blender sẽ được xuất sang Unity và tự động ánh xạ (Map) vào hệ thống **Unity Humanoid Avatar**, cho phép nhân vật sử dụng chung hàng ngàn animation có sẵn trên Unity Asset Store!

---

## 2. Giải Phẫu Cấu Trúc Khung Xương (Bone Anatomy)

Một đối tượng Armature trong Blender được tạo thành từ nhiều đoạn xương (**Bones**). Mỗi chiếc xương bao gồm ba bộ phận hình học:
* **Gốc xương (Head / Root):** Điểm cầu tròn to ở đáy, đóng vai trò là tâm điểm xoay của khớp nối.
* **Thân xương (Body):** Khối bát diện thể hiện chiều dài và hướng của xương.
* **Ngọn xương (Tail / Tip):** Điểm nhọn ở đầu, là điểm cắm nối để sinh ra khớp xương tiếp theo.

```text
       Ngọn xương (Tail)
             ▲
            / \
           /   \  Thân xương (Body)
          /     \
         /       \
        /_________\
             ●
       Gốc xương (Head / Điểm xoay khớp)
```

### Ba chế độ làm việc với Armature:
1. **Object Mode:** Thao tác trên toàn bộ khung xương như một đối tượng thống nhất (di chuyển, phóng to).
2. **Edit Mode (Phím `[Tab]`):** Dựng xương, kéo dài khớp, đổi tên, sắp xếp phân cấp cha con và căn chỉnh vị trí khớp xương cho khớp với mô hình da thịt.
3. **Pose Mode (Tổ hợp `[Ctrl + Tab]`):** Chế độ tạo dáng và gắn keyframe hoạt họa. Ở chế độ này, bạn xoay xương để nhân vật cử động thực tế mà không làm thay đổi hình dáng khung xương gốc ban đầu.

---

## 3. Quy Ước Đặt Tên Chuẩn Quốc Tế Cho Unity Humanoid

Game engine Unity nhận diện khung xương người thông qua chuẩn **Humanoid Avatar**. Để Blender và Unity hiểu nhau 100% tự động, bạn **BẮT BUỘC phải đặt tên xương theo đúng chuẩn tiếng Anh kết hợp hậu tố đối xứng**:

### Quy ước hậu tố Trái / Phải (`.L` và `.R`):
* Các xương nằm ở bên trái cơ thể nhân vật BẮT BUỘC kết thúc bằng đuôi **`.L`** (Left).
* Các xương nằm ở bên phải cơ thể nhân vật BẮT BUỘC kết thúc bằng đuôi **`.R`** (Right).

```text
┌─────────────────────────────────────────────────────────────┐
│ BẢNG DANH MỤC TÊN XƯƠNG CHUẨN UNITY HUMANOID                │
├──────────────────────┬──────────────────────────────────────┤
│ Xương Trục Giữa      │ Hips (Xương chậu / Root điều khiển)  │
│                      │ Spine (Cột sống thắt lưng)           │
│                      │ Chest (Lồng ngực)                    │
│                      │ Neck (Khớp cổ)                       │
│                      │ Head (Hộp sọ / Đầu)                  │
├──────────────────────┼──────────────────────────────────────┤
│ Xương Tay (Trái)     │ Shoulder.L (Xương quai xanh / bả vai)│
│                      │ UpperArm.L (Bắp tay trên)            │
│                      │ Forearm.L (Cẳng tay dưới)            │
│                      │ Hand.L (Bàn tay)                     │
├──────────────────────┼──────────────────────────────────────┤
│ Xương Chân (Trái)    │ Thigh.L (Xương đùi)                  │
│                      │ Shin.L (Xương cẳng chân / ống đồng)  │
│                      │ Foot.L (Bàn chân)                    │
│                      │ Toe.L (Ngón chân)                    │
└──────────────────────┴──────────────────────────────────────┘
```

### Phép thuật Tự Động Đối Xứng (Symmetrize):
Khi bạn đặt tên đúng quy ước `.L` cho toàn bộ nửa người bên trái:
1. Trong Edit Mode của Armature, nhấn `[A]` chọn toàn bộ các xương bên trái.
2. Vào menu **Armature > Symmetrize**.
3. Blender sẽ tự động sao chép toàn bộ hệ thống xương sang nửa bên phải, lật ngược trục tọa độ chính xác từng milimét và tự động đổi toàn bộ đuôi `.L` thành **`.R`** trong chớp mắt!

---

## 4. Hướng Xoay Khớp (Bone Roll) – Ngăn Ngừa Lỗi Bẻ Ngược Khớp

Một trong những lỗi kinh hoàng nhất khi mới làm Rigging: Bạn gắn xương xong, thử co chân nhân vật thì đầu gối bị bẻ ngoặt 180 độ ra phía sau hoặc khuỷu tay bị xoay ngang như gãy xương!

### Nguyên nhân và Giải pháp:
Mỗi chiếc xương ngoài vị trí tọa độ còn có một góc xoay quanh trục dọc của chính nó gọi là **Bone Roll**:
* Trước khi dựng khớp, luôn tạo một **góc cong nhẹ tự nhiên (Pre-bend)**:
  * Khớp khuỷu tay phải hơi cong lùi về phía sau một góc nhỏ 5 độ.
  * Khớp đầu gối phải hơi cong nhô về phía trước một góc nhỏ 5 độ.
* **Chuẩn hóa góc xoay:** Trong Edit Mode, chọn toàn bộ xương chân và tay, vào menu **Armature > Bone Roll > Recalculate Roll**, chọn trục chiếu phù hợp (thường là *Global +Z Axis* hoặc *View Axis*) để đảm bảo trục uốn cong của khớp luôn vuông góc với hướng cử động.

---

## 5. Thiết Lập Hiển Thị Khung Xương Tối Ưu

Để xương không bị da thịt che khuất trong quá trình dựng:
1. Chọn Armature, vào bảng thuộc tính **Object Data Properties** (biểu tượng hình người que màu xanh lá bên phải).
2. Mở mục **Viewport Display**:
   * Tích chọn ô **In Front**: Bộ xương sẽ luôn hiển thị nổi rõ ràng lên trên cùng.
   * Tích chọn ô **Names**: Hiển thị tên từng đoạn xương ngay trên màn hình để tránh nhầm lẫn.
   * Tích chọn ô **Axes**: Hiển thị ba trục tọa độ `(X, Y, Z)` của từng khớp xương.

---

## 6. Phân Cấp Cha Con (Parenting with Connected vs Keep Offset)

Khi di chuyển xương Chậu (`Hips`), toàn bộ cơ thể bên trên và hai chân phải di chuyển theo. Đó là quan hệ **Cha - Con (Parent - Child)**:
* Chọn xương con trước, giữ `[Shift]` chọn xương cha sau, nhấn tổ hợp **`[Ctrl + P]`**:
  * **Connected (Gắn liền dính khớp):** Điểm gốc của xương con dính chặt cơ học vào ngọn của xương cha (dùng cho các đốt xương sống, cánh tay, cẳng chân).
  * **Keep Offset (Giữ khoảng cách độc lập):** Xương con vẫn di chuyển và xoay theo xương cha nhưng duy trì một khoảng cách không gian riêng (dùng để nối xương đùi `Thigh.L` vào xương chậu `Hips`).

---

## Bài tập thực hành

**Mục tiêu:** Tạo bộ khung xương người hoàn chỉnh chuẩn Unity Humanoid cho nhân vật và thực hiện thao tác Symmetrize trong 15 phút.

1. Bật mô hình nhân vật Low-poly đang đứng ở tư thế A-Pose.
2. Nhấn `[Shift + A]` > **Armature > Single Bone** đặt tại giữa tâm háng nhân vật. Bật tính năng **In Front**.
3. Vào Edit Mode, đổi tên đoạn xương này là `Hips`. Kéo đỉnh xương lên ngang rốn.
4. Chọn đỉnh của xương `Hips`, nhấn `[E] + [Z]` đùn lên đoạn xương thứ hai đặt tên là `Spine`.
5. Đùn tiếp đoạn thứ ba đặt tên là `Chest`, đùn đoạn thứ tư làm `Neck`, đùn đoạn cuối cùng lên đỉnh đầu đặt tên là `Head`.
6. Từ xương `Chest`, nhấn `[E] + [X]` đùn ngang sang vai trái đặt tên là `Shoulder.L`.
7. Từ `Shoulder.L`, đùn xuôi chéo 45 độ xuống khuỷu tay trái đặt tên là `UpperArm.L`. Đùn tiếp xuống cổ tay đặt tên là `Forearm.L`, đùn ra bàn tay đặt tên là `Hand.L`. (Nhớ tạo góc khuỷu tay hơi lùi nhẹ ra sau).
8. Chọn đầu dưới của xương `Hips`, nhấn `[E]` đùn xuống khớp háng trái, rồi đùn thẳng xuống đầu gối đặt tên là `Thigh.L` (xóa xương nối tạm hoặc dùng Keep Offset).
9. Từ đầu gối đùn xuống mắt cá chân đặt tên là `Shin.L`, đùn ra mũi chân đặt tên là `Foot.L`.
10. Nhấn `[A]` chọn toàn bộ các xương bên trái có đuôi `.L`.
11. Vào menu **Armature > Symmetrize**. Chiêm ngưỡng bộ khung xương bên phải `.R` xuất hiện hoàn chỉnh đối xứng 100%, sẵn sàng cho công đoạn gán da thịt Weight Paint!

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/animation/armatures/bones/index.html
- https://docs.blender.org/manual/en/5.2/animation/armatures/editing/symmetrize.html
- https://docs.blender.org/manual/en/5.2/animation/armatures/properties/display.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
