# Bài 02: Kỹ Thuật Modeling Đa Giác Cơ Bản và Cấu Trúc Lưới trong Blender 5.2

> **Danh mục:** Dựng Hình & Modeling
> **Tags:** modeling, editmode, extrude, inset, bevel, loopcut, topology, unity

---

## 1. Cấu trúc hình học đa giác (Mesh Topology) và Tiêu chuẩn Game 3D

Mọi nhân vật, vũ khí hay đạo cụ 3D trong game đều được cấu tạo từ ba thành phần hình học nguyên tử:
* **Đỉnh (Vertex):** Điểm tọa độ không gian `(X, Y, Z)`.
* **Cạnh (Edge):** Đoạn thẳng nối liền hai đỉnh.
* **Mặt (Face / Polygon):** Bề mặt kín tạo bởi ba hoặc nhiều cạnh liên kết nhau.

```text
       Đỉnh (Vertex)
           ●
          / \
Cạnh     /   \
(Edge)  /     \
       ●───────●
     Mặt (Face) - 3 đỉnh (Triangle)
```

### Phân loại các dạng mặt đa giác
1. **Mặt 4 cạnh (Quad - Quadrilateral):** Bề mặt có đúng 4 đỉnh và 4 cạnh. Đây là **tiêu chuẩn vàng** khi dựng mô hình nhân vật vì lưới quad có hướng dòng chảy cạnh (Edge Flow) rõ ràng, giúp biến dạng mượt mà khi uốn cong cơ bắp và dễ dàng kiểm soát khi trải UV.
2. **Mặt 3 cạnh (Tri - Triangle):** Bề mặt có 3 đỉnh. Tất cả các game engine (bao gồm Unity và Unreal Engine) về bản chất phần cứng đồ họa (GPU) đều chỉ vẽ các mặt tam giác. Các mặt quad khi nạp vào Unity sẽ tự động được chia đôi thành 2 mặt tam giác.
3. **Mặt đa giác nhiều cạnh (N-gon):** Bề mặt có từ 5 đỉnh trở lên. **Cần tuyệt đối tránh N-gon trên nhân vật cử động** vì engine game sẽ tự động chém đa giác này theo hướng ngẫu nhiên, gây ra hiện tượng rách lưới, bóng đổ méo mó và biến dạng dị thường khi gắn xương hoạt họa.

---

## 2. Không gian chỉnh sửa Lưới: Object Mode và Edit Mode

* Nhấn phím `[Tab]` để chuyển đổi nhanh giữa:
  * **Chế độ Đối Tượng (Object Mode):** Thao tác trên toàn bộ vật thể như một khối thống nhất (di chuyển, xoay, gắn liên kết cha con).
  * **Chế độ Chỉnh Sửa Lưới (Edit Mode):** Tương tác chi tiết với từng đỉnh, cạnh và mặt của vật thể.
* Trong Edit Mode, bạn chuyển đổi linh hoạt 3 kiểu chọn bằng các phím số hàng trên:
  * Phím `[1]`: Chọn Đỉnh (Vertex Select).
  * Phím `[2]`: Chọn Cạnh (Edge Select).
  * Phím `[3]`: Chọn Mặt (Face Select).
* **Chế độ X-Ray `[Alt + Z]`:** Cho phép nhìn xuyên thấu qua các bề mặt để quét chọn cả những đỉnh và mặt nằm ở phía sau lưng vật thể.

---

## 3. Bộ 5 công cụ quyền năng nhất để biến đổi hình học

### 1. Đẩy Trồi Vùng (Extrude Region - Phím `[E]`)
Lệnh Extrude nhân bản vùng chọn và kéo đùn ra ngoài theo hướng pháp tuyến mặt (Normal) để tạo thêm thể tích mới:
* Chọn một mặt, nhấn `[E]`, rê chuột để kéo dài khối rồi click chuột trái để xác nhận.
* **Đùn nâng cao `[Alt + E]`:**
  * *Extrude Faces Along Normals (Đẩy trồi mặt dọc theo pháp tuyến):* Nở đều các mặt ra xung quanh theo phương vuông góc với từng bề mặt riêng.
  * *Extrude Individual Faces (Đẩy trồi từng mặt riêng lẻ):* Mỗi mặt được đùn tách rời nhau thay vì dính liền thành một khối chung.

### 2. Chèn Mặt Vào Trong (Inset Faces - Phím `[I]`)
Lệnh Inset tạo ra một viền mặt phẳng đồng dạng thụt vào phía trong lòng mặt được chọn:
* Chọn mặt, nhấn `[I]`, đẩy nhẹ chuột vào trong.
* **Tác dụng cốt lõi:** Luôn dùng lệnh Inset trước khi khoét lỗ hoặc bo viền để tạo ra **Đường viền hỗ trợ (Support Edge / Holding Loop)**. Vòng viền này giúp giữ vững cấu trúc bề mặt, chống hiện tượng nhăn nheo khi áp dụng các bộ điều chỉnh làm mịn.

### 3. Bo Tròn Cạnh và Đỉnh (Bevel - Tổ hợp `[Ctrl + B]`)
Bevel loại bỏ các mép sắc nhọn bằng cách vát nghiêng hoặc bo tròn các cạnh giao nhau:
* Chọn các cạnh muốn vát, nhấn `[Ctrl + B]`, di chuyển chuột ra xa để mở rộng góc vát.
* **Lăn con lăn chuột giữa (MMB):** Tăng hoặc giảm số phân đoạn (Segments) để bề mặt cong tròn mịn màng.
* Bo tròn đỉnh nhọn: Chọn đỉnh, nhấn tổ hợp `[Ctrl + Shift + B]`.

### 4. Cắt Vòng Lặp và Trượt (Loop Cut and Slide - Tổ hợp `[Ctrl + R]`)
Loop Cut tạo thêm một vòng dây cạnh khép kín bao quanh toàn bộ mô hình:
* Rê chuột qua cạnh của vật thể, một đường chỉ dẫn màu vàng sẽ xuất hiện báo trước hướng cắt.
* Lăn con lăn chuột giữa để tăng số lượng đường cắt song song.
* Click chuột trái 1 lần để xác nhận số đường, sau đó trượt chuột để chọn vị trí dừng, hoặc click chuột phải để đặt đường cắt vào ngay chính giữa.
* **Trượt cạnh (Edge Slide):** Chọn cạnh bất kỳ, nhấn phím `[G]` hai lần liên tiếp `[G + G]` để trượt cạnh dọc theo bề mặt mà không làm biến dạng hình khối.

### 5. Dao Cắt Tự Do (Knife Tool - Phím `[K]`)
Cho phép bạn dùng dao vẽ tự do các đường cắt topology trên bề mặt lưới:
* Nhấn `[K]`, click chuột trái lên các đỉnh hoặc cạnh cần nối đường cắt.
* Nhấn phím `[C]` để kích hoạt chế độ cắt xuyên thấu qua cả mặt đối diện phía sau.
* Nhấn phím `[A]` để khóa góc cắt theo bội số 45 độ hoặc 90 độ.
* Nhấn `[Space]` hoặc `[Enter]` để xác nhận hoàn tất đường cắt.
* **Nối hai đỉnh xuyên mặt (Connect Vertex Path - Phím `[J]`):** Chọn 2 đỉnh trên cùng một mặt, nhấn `[J]` để chém đôi mặt đó thành hai mặt quad ngăn nắp (khác với phím `[F]` chỉ tạo một cạnh nổi mà không chia mặt).

---

## 4. Kỹ thuật Lựa Chọn Lưới Nâng Cao

Dựng hình nhân vật đòi hỏi thao tác chọn nhanh hàng trăm phần tử:
* **Chọn Vòng Cạnh (Loop Select):** Nhấn giữ `[Alt + Click Chuột trái]` lên một cạnh. Toàn bộ vòng cạnh nối tiếp liên tục sẽ được chọn.
* **Chọn Vòng Mặt (Face Loop Select):** Nhấn giữ `[Alt + Click]` gần mép ranh giới giữa hai mặt.
* **Chọn Vòng Song Song (Ring Select):** Nhấn giữ `[Ctrl + Alt + Click]` lên một cạnh để chọn các cạnh song song nằm cạnh nhau.
* **Mở rộng vùng chọn (Grow Selection):** Nhấn `[Ctrl + Numpad +]` để mở rộng vùng chọn lan sang các đỉnh lân cận.
* **Thu hẹp vùng chọn (Shrink Selection):** Nhấn `[Ctrl + Numpad -]`.
* **Chọn đường đi ngắn nhất (Shortest Path):** Chọn điểm đầu, giữ `[Ctrl + Click]` lên điểm đích. Blender sẽ tự động tìm và chọn đường đi ngắn nhất giữa hai điểm.

---

## 5. Dọn dẹp hình học (Mesh Cleanup) và Tối ưu hóa

Trước khi đưa mô hình sang giai đoạn điêu khắc hoặc xuất game, việc dọn dẹp lưới là bắt buộc:
1. **Xóa đỉnh trùng lặp (Merge by Distance):** Nhấn `[A]` để chọn toàn bộ lưới trong Edit Mode, nhấn `[M]` chọn **By Distance**. Blender sẽ tự động quét và hàn gắn các đỉnh nằm sát nhau trong khoảng dung sai `0.0001m`.
2. **Hòa tan phần tử (Dissolve Elements):** Khi muốn xóa bớt cạnh hoặc đỉnh thừa mà không làm thủng rách mặt lưới, nhấn `[X]` chọn **Dissolve Edges** hoặc **Dissolve Vertices** (thay vì Delete).
3. **Tính toán lại hướng mặt (Recalculate Normals):** Nhấn `[A]` chọn toàn bộ, nhấn `[Shift + N]` để đảm bảo 100% các mặt polygon đều quay mặt chính ra ngoài.

---

## Bài tập thực hành

**Mục tiêu:** Dựng một thanh đoản kiếm hiệp sĩ phong cách Low-poly hoàn chỉnh trong 10-15 phút chỉ bằng các công cụ cơ bản.

1. Mở cảnh mới, giữ lại khối lập phương **Cube** mặc định.
2. Chọn Cube, nhấn `[Tab]` để chuyển sang **Edit Mode**.
3. Nhấn `[S] + [X]` thu hẹp khối lại theo trục X còn một thanh dẹt (độ dày khoảng 0.1m).
4. Nhấn `[3]` chuyển sang chọn mặt, click chọn mặt trên cùng của thanh. Nhấn `[E]` và kéo chuột lên cao khoảng 2 mét để tạo thân lưỡi kiếm.
5. Nhấn `[Ctrl + R]` trên thân kiếm, cuộn chuột giữa tạo 3 đường cắt ngang chia đều thân kiếm.
6. Chọn mặt đỉnh trên cùng của lưỡi kiếm, nhấn `[E]` đùn lên một đoạn ngắn 0.3m. Nhấn `[S] + [Y]` thu hẹp bề ngang lại thành mũi nhọn hình tam giác.
7. Chọn mặt đáy dưới cùng của khối lập phương ban đầu, nhấn `[E]` đùn xuống 0.2m. Nhấn `[I]` (Inset) đẩy nhẹ viền vào trong để làm chuôi kiếm.
8. Chọn mặt đáy của chuôi kiếm vừa thu nhỏ, tiếp tục nhấn `[E]` đùn dài xuống 0.8m để làm tay cầm.
9. Nhấn `[Ctrl + R]` cắt đôi tay cầm, nhấn `[Alt + S]` (Shrink/Fatten) phồng nhẹ ra để tạo điểm gờ cầm nắm.
10. Tại khu vực thanh chắn tay (Crossguard), chọn hai mặt hông bên cạnh, nhấn `[Alt + E]` chọn **Extrude Individual Faces**, đùn ngang sang hai bên trái phải mỗi bên 0.5m.
11. Nhấn `[A]` chọn toàn bộ thanh kiếm, nhấn `[M]` chọn **By Distance** để kiểm tra sạch sẽ. Nhấn `[Tab]` trở về Object Mode để chiêm ngưỡng tác phẩm.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/modeling/meshes/editing/index.html
- https://docs.blender.org/manual/en/5.2/modeling/meshes/structure.html
- https://docs.blender.org/manual/en/5.2/modeling/meshes/editing/vertex/merge.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
