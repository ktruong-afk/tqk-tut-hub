# Bài 01: Giao Diện Người Dùng và Kỹ Năng Điều Hướng Viewport trong Blender 5.2

> **Danh mục:** Căn Bản & Giao Diện
> **Tags:** interface, navigation, viewport, blender52, shortcuts, basics

---

## 1. Tổng quan kiến trúc giao diện Blender 5.2

Blender 5.2 LTS sở hữu giao diện đồ họa trực quan, hiệu năng cao và có khả năng tùy biến mạnh mẽ. Khác với nhiều phần mềm truyền thống chia nhiều cửa sổ con độc lập, Blender tổ chức toàn bộ không gian làm việc trên một cửa sổ duy nhất được chia thành các **Biên Mục (Editors)**.

Khi khởi động Blender 5.2, bạn sẽ tiếp cận các khu vực chính sau:
* **Khung Nhìn 3D (3D Viewport):** Vùng làm việc trung tâm, nơi bạn tương tác trực tiếp với vật thể 3D, camera và nguồn sáng.
* **Biên Mục Thuộc Tính (Properties Editor):** Nằm ở cạnh phải màn hình, chứa các thẻ cấu hình cốt lõi: Thiết lập Kết xuất (Render Properties), Đầu ra (Output), Bộ điều chỉnh (Modifiers), Dữ liệu Lưới (Mesh Data), Vật liệu (Material Properties)...
* **Mục Lục Đối Tượng (Outliner):** Góc trên bên phải, hiển thị cấu trúc phân cấp dạng cây của toàn bộ các Bộ Sưu Tập (Collections) và Đối Tượng (Objects) trong cảnh.
* **Thanh Dòng Thời Gian (Timeline):** Nằm ở mép dưới, quản lý khung hình (frames), điểm khóa (keyframes) và điều khiển phát chuyển động.
* **Thanh Đầu Trang (Top Bar):** Chứa các trình đơn hệ thống (File, Edit, Render, Window, Help) và hàng tab Không Gian Làm Việc (Workspaces).

```text
┌────────────────────────────────────────────────────────────────────────┐
│ Top Bar: File | Edit | Render | Window | Workspaces (Layout, Sculpt...) │
├──────────────────────────────────────────┬─────────────────────────────┤
│                                          │ Outliner (Cây phân cấp)     │
│                                          ├─────────────────────────────┤
│ 3D Viewport (Khung nhìn tương tác 3D)    │ Properties (Bảng cấu hình)  │
│ [T] Toolbar (Trái)     [N] Sidebar (Phải)│  - Render, Modifiers,       │
│                                          │    Materials, Data...       │
├──────────────────────────────────────────┴─────────────────────────────┤
│ Timeline (Khung hình & Hoạt họa)                                       │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Hệ thống Không Gian Làm Việc (Workspaces) chuyên biệt

Để phục vụ quy trình xây dựng nhân vật game chuyên nghiệp, Blender 5.2 phân chia sẵn các không gian làm việc tối ưu cho từng công đoạn:
1. **Layout / Modeling:** Thiết lập bố cục chung, dựng hình khối cơ bản (Blockout) và chỉnh sửa cấu trúc lưới đa giác.
2. **Sculpting:** Giao diện tối ưu hóa cho điêu khắc giải phẫu, hỗ trợ cọ vẽ cảm ứng lực, tự động ẩn các thanh công cụ không cần thiết để mở rộng vùng nhìn.
3. **UV Editing:** Chia đôi màn hình giữa 3D Viewport và Trình biên tập ảnh UV (UV Editor) nhằm mở phẳng bề mặt 3D ra tọa độ 2D.
4. **Shading:** Tích hợp Trình biên tập Nút Vật Liệu (Shader Editor) để xây dựng vật liệu PBR (Physically Based Rendering) cho nhân vật.
5. **Animation:** Bố trí Bảng Ghi Dữ Liệu (Dope Sheet) và Trình biên tập Đồ Thị (Graph Editor) để tinh chỉnh nhịp điệu cử động của xương.

---

## 3. Kỹ năng làm chủ điều hướng chuột và bàn phím

Thao tác điều hướng mượt mà trong không gian ba chiều là điều kiện tiên quyết để tạo phản xạ dựng hình vững chắc. Chuột ba nút (3-Button Mouse) là công cụ bắt buộc khi làm việc với Blender.

### Thao tác chuột cơ bản
* **Xoay góc nhìn (Orbit):** Nhấn giữ `[Chuột giữa (MMB)]` và rê chuột xung quanh điểm xoay trung tâm.
* **Trượt góc nhìn (Pan):** Nhấn giữ tổ hợp `[Shift + Chuột giữa]` và di chuyển chuột để tịnh tiến vùng nhìn sang trái, phải, lên hoặc xuống.
* **Thu phóng góc nhìn (Zoom):** Lăn `[Con lăn chuột giữa]` hoặc nhấn giữ `[Ctrl + Chuột giữa]` kết hợp di chuột lên xuống để thu phóng siêu mượt.
* **Tập trung vào đối tượng (Frame Selected):** Nhấn phím `[Numpad .]` (dấu chấm trên bàn phím số) hoặc phím `[~]` (Tilde) chọn *View Selected*. Góc nhìn sẽ lập tức lấy nét phóng to vào đúng vật thể hoặc các đỉnh/cạnh đang được chọn.

### Góc nhìn chiếu trực giao (Orthographic) và Phối cảnh (Perspective)
* `[Numpad 5]`: Chuyển đổi qua lại giữa phối cảnh có điểm tụ (Perspective) và hình chiếu song song trục (Orthographic). Khi nắn tỷ lệ nhân vật, chế độ Orthographic giúp loại bỏ hoàn toàn hiện tượng méo góc do ống kính.
* `[Numpad 1]`: Góc nhìn Chính Diện (Front Orthographic) – hướng nhìn thẳng mặt nhân vật.
* `[Ctrl + Numpad 1]`: Góc nhìn Phía Sau (Back Orthographic).
* `[Numpad 3]`: Góc nhìn Bên Phải (Right Orthographic) – hướng nhìn ngang sườn nhân vật.
* `[Ctrl + Numpad 3]`: Góc nhìn Bên Trái (Left Orthographic).
* `[Numpad 7]`: Góc nhìn Từ Trên Xuống (Top Orthographic).
* `[Numpad 0]`: Nhìn xuyên qua ống kính Camera kết xuất cảnh.

> **Mẹo hữu ích:** Nếu bạn dùng laptop không có cụm bàn phím số (Numpad), hãy vào **Edit > Preferences > Input**, tích chọn mục **Emulate Numpad**. Khi đó các phím số hàng trên `[1]` đến `[0]` sẽ đóng vai trò như bàn phím số Numpad.

---

## 4. Hệ tọa độ 3D và Nguyên tắc Khóa Trục (Axis Locking)

Không gian ba chiều trong Blender được xác định bởi hệ tọa độ Descartes với ba trục màu chuẩn quốc tế:
* **Trục X (Đường kẻ màu Đỏ):** Hướng trục Ngang (Trái - Phải).
* **Trục Y (Đường kẻ màu Lục):** Hướng trục Chiều Sâu (Trước - Sau). Trong quy chuẩn của game engine Unity, hướng nhìn chính diện của nhân vật thường quay mặt về hướng `-Y` hoặc `+Z`.
* **Trục Z (Đường kẻ màu Lam):** Hướng trục Thẳng Đứng (Trên - Dưới).

### Ba thao tác biến đổi cốt lõi (Transformations)
1. **Di chuyển - Dịch chuyển (Grab / Move):** Nhấn phím `[G]`.
2. **Xoay (Rotate):** Nhấn phím `[R]`. Nhấn `[R]` hai lần liên tiếp `[R + R]` để kích hoạt chế độ xoay tự do con lăn cầu (Trackball Rotation).
3. **Thu phóng tỷ lệ (Scale):** Nhấn phím `[S]`.

### Phương pháp khóa trục chuẩn xác
Sau khi nhấn `[G]`, `[R]` hoặc `[S]`, bạn nhấn tiếp phím đại diện cho trục để khóa chuyển động:
* `[G] + [X]`: Chỉ di chuyển theo trục X.
* `[G] + [Z]`: Chỉ nâng cao hoặc hạ thấp theo phương thẳng đứng.
* `[G] + [Shift + Z]`: Khóa trục Z, cho phép dịch chuyển tự do trên mặt phẳng sàn (mặt phẳng tạo bởi trục X và Y).
* Nhập trực tiếp con số: Sau khi nhấn `[G] + [X]`, gõ trực tiếp `2.5` rồi nhấn `[Enter]`, vật thể sẽ di chuyển chính xác 2.5 đơn vị mét theo chiều dương trục X.

---

## 5. Các thanh công cụ và Trình đơn Bánh xe (Pie Menus)

* **Thanh công cụ Toolbar `[T]`:** Mở hoặc ẩn thanh công cụ cạnh trái chứa các công cụ: Chọn (Select), Con trỏ 3D (Cursor), Dịch chuyển (Move), Xoay (Rotate), Thu phóng (Scale), Đo đạc (Measure)...
* **Thanh thuộc tính Sidebar `[N]`:** Mở hoặc ẩn thanh cạnh phải chứa tab **Item** (tọa độ vị trí, góc xoay, tỷ lệ scale chính xác của vật thể), tab **Tool** và tab chứa các công cụ cài đặt mở rộng.
* **Bánh xe chế độ hiển thị Shading Pie `[Z]`:** Khi nhấn phím `[Z]`, một menu bánh xe trực quan xuất hiện:
  * **Khung Dây (Wireframe):** Xem cấu trúc khung lưới polygon xuyên thấu.
  * **Khối Đặc (Solid):** Chế độ mặc định để dựng hình khối.
  * **Xem Trước Vật Liệu (Material Preview):** Dùng EEVEE để hiển thị màu sắc, vân bề mặt và độ nhám kim loại.
  * **Kết Xuất Hoàn Thiện (Rendered):** Mô phỏng toàn diện ánh sáng, bóng đổ của cảnh.
* **Thanh tìm kiếm vạn năng `[F3]`:** Bất cứ khi nào bạn nhớ tên lệnh tiếng Anh hoặc tiếng Việt mà quên vị trí trong menu, nhấn `[F3]`, gõ từ khóa để gọi lệnh tức thì.

---

## 6. Điểm Neo Con Trỏ 3D (3D Cursor)

Con trỏ 3D (biểu tượng vòng tròn sọc đỏ trắng) là một trong những tính năng độc đáo nhất của Blender:
* Nhấn `[Shift + Chuột phải]` tại bất kỳ điểm nào trong viewport để đặt con trỏ 3D vào vị trí đó.
* Mọi vật thể mới tạo thông qua menu `[Shift + A]` sẽ xuất hiện ngay tại tọa độ của 3D Cursor.
* Nhấn `[Shift + C]` để đưa Con trỏ 3D quay trở lại chính giữa tâm thế giới `(0, 0, 0)` và đồng thời lấy nét lại toàn bộ khung cảnh.
* Nhấn `[Shift + S]` để mở menu **Snap Pie**: Cho phép dịch chuyển vật thể về tâm con trỏ (`Selection to Cursor`) hoặc đưa con trỏ nhảy về tâm vật thể (`Cursor to Selected`).

---

## 7. Các lỗi người mới hay gặp khi điều hướng
1. **Lỗi xoay màn hình bị kẹt (View clipping / Pan stuck):** Đôi khi bạn lăn chuột để phóng to nhưng camera di chuyển cực kỳ chậm và không thể tiến gần hơn. Nguyên nhân là điểm hội tụ xoay nằm quá xa vật thể. **Khắc phục:** Chọn một vật thể hoặc đỉnh gần đó rồi nhấn `[Numpad .]` để thiết lập lại tâm hội tụ.
2. **Vật thể bị cắt lẹm khi zoom lại gần (Near Clipping Plane):** Mặt lưới biến mất hoặc thủng lỗ khi camera áp sát. **Khắc phục:** Mở thanh Sidebar `[N]`, chọn tab **View**, chỉnh thông số **Clip Start** từ `0.1m` xuống `0.01m` (hoặc `0.001m`).

---

## Bài tập thực hành

**Mục tiêu:** Làm chủ các phím tắt điều hướng, chuyển đổi góc nhìn trực giao và định vị Con trỏ 3D trong 10-15 phút.

1. Khởi động Blender, xóa vật thể Cube mặc định bằng phím `[X]` hoặc `[Delete]`.
2. Nhấn `[Shift + C]` để đặt 3D Cursor về tâm thế giới `(0, 0, 0)`.
3. Nhấn `[Shift + A]` vào menu **Mesh > Monkey** để tạo mô hình đầu khỉ Suzanne.
4. Luyện tập xoay xung quanh đầu khỉ bằng `[Chuột giữa]`, trượt góc nhìn bằng `[Shift + Chuột giữa]`, và thu phóng bằng `[Ctrl + Chuột giữa]`.
5. Nhấn `[Numpad 1]` để quan sát thẳng mặt Suzanne ở góc nhìn Front Orthographic.
6. Nhấn `[G] + [Z]`, gõ `2` và nhấn `[Enter]` để nâng đầu khỉ lên cao 2m.
7. Nhấn `[Numpad 3]` để chuyển sang góc nhìn nghiêng Right Orthographic. Nhấn `[R]`, gõ `-45` và nhấn `[Enter]` để nghiêng đầu khỉ về phía sau 45 độ.
8. Nhấn `[Shift + Chuột phải]` lên trên đỉnh đầu khỉ để đặt 3D Cursor tại đó.
9. Nhấn `[Shift + A]` > **Mesh > UV Sphere** để tạo một khối cầu nhỏ làm phụ kiện mũ trên đỉnh đầu. Nhấn `[S]` để thu nhỏ khối cầu lại còn một nửa kích thước.
10. Nhấn `[Numpad .]` để tập trung phóng to vào khối cầu, sau đó nhấn phím `[Z]` chọn **Wireframe** để kiểm tra lưới khung dây.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/interface/index.html
- https://docs.blender.org/manual/en/5.2/editors/3dview/navigate/index.html
- https://docs.blender.org/manual/en/5.2/editors/3dview/3d_cursor.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
