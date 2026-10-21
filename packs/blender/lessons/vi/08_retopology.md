# Bài 08: Kỹ Thuật Đi Lại Lưới (Retopology) - Cầu Nối Giữa Sculpting và Game Engine

> **Danh mục:** Dựng Hình & Tối Ưu Hóa Game
> **Tags:** retopology, snap, shrinkwrap, lowpoly, polybuild, edgeflow, unity

---

## 1. Vì Sao Phải Đi Lại Lưới (Retopology)?

Sau khi hoàn tất giai đoạn điêu khắc (Sculpting), bạn sở hữu một tác phẩm tuyệt đẹp với đầy đủ cơ bắp và biểu cảm. Tuy nhiên, mô hình này có tới **2 đến 5 triệu đa giác**, các mặt lộn xộn không theo quy luật.
* Nếu đưa trực tiếp khối High-poly này vào Unity, card đồ họa của điện thoại hoặc máy tính sẽ bị quá tải, gây tụt khung hình (FPS drop) nghiêm trọng.
* Các đỉnh lưới phân bố hỗn loạn khiến việc gắn xương cử động (Rigging) và điều khiển cơ mặt biến dạng (Facial Animation) bị nhăn nhúm, biến dạng méo mó.

👉 **Giải pháp sống còn:** **Retopology (Đi lại lưới)** là quy trình xây dựng một lớp lưới đa giác thấp (**Low-Poly**, thường từ 10.000 đến 35.000 Quads cho nhân vật game chính) bọc khít sát bên ngoài mô hình High-Poly, với các đường viền cạnh uốn lượn chính xác theo các cơ quan cử động.

```text
  [High-Poly Sculpt]          [Retopology Low-Poly]
  2,000,000 Polygons    ───→  15,000 Quads (Lưới sạch)
  (Nặng, không thể rig)       (Nhẹ, sẵn sàng cho Unity & Rigging)
```

---

## 2. Tiêu Chuẩn Dòng Chảy Cạnh (Edge Flow) Cho Nhân Vật Game

Dòng chảy cạnh (Edge Flow) là hướng sắp xếp liên tục của các vòng cạnh (Edge Loops). Khi nhân vật chớp mắt hoặc há miệng, các cạnh phải co giãn tự nhiên theo thớ cơ giải phẫu:

### 1. Ba Vòng Lặp Sống Còn Trên Khuôn Mặt (Facial Loops):
* **Vòng lặp Mắt (Orbicularis Oculi):** Các vòng cạnh chạy tròn đồng tâm quanh hốc mắt như gọng kính. Giúp mí mắt khép lại mượt mà khi chớp mắt.
* **Vòng lặp Miệng (Orbicularis Oris):** Các vòng cạnh chạy tròn đồng tâm quanh viền môi. Cần thiết để nhân vật phát âm các nguyên âm A, O, U và cười mở miệng.
* **Vòng rãnh Mũi Má (Nasolabial Loop):** Vòng cạnh chạy từ cánh mũi vòng qua khóe miệng xuống cằm, giữ ranh giới rõ ràng khi nhân vật cười biểu cảm.

### 2. Quy Tắc Ba Cạnh Tại Các Khớp Cử Động (Joint Topology):
Tại các vùng gập như **khuỷu tay, đầu gối và khớp ngón tay**:
* Tuyệt đối không dùng 1 cạnh đơn lẻ ở khớp gập! Khi uốn cong 90 độ, mặt lưới sẽ bị xẹp lép như ống cao su bị bẹp.
* Luôn bố trí **tối thiểu 3 vòng cạnh (Triple Edge Loops)** kẹp sát vùng khớp: 1 cạnh nằm ngay rãnh gập chính giữa, 2 cạnh nằm ở hai bên để phân bổ độ căng, giữ nguyên thể tích khối thịt khi co duỗi.

---

## 3. Thiết Lập Môi Trường Retopology Tối Ưu trong Blender 5.2

Để thao tác nhanh và không bị phân tâm, hãy chuẩn bị môi trường làm việc theo các bước sau:

### 1. Bật công cụ Hít Bắt Dính Bề Mặt (Face Snapping)
Trên thanh công cụ phía trên đỉnh 3D Viewport:
1. Bấm vào biểu tượng hình chiếc nam châm `[Shift + Tab]` để bật tính năng **Snap**.
2. Bấm vào menu thả xuống cạnh nam châm, chọn mục **Face Project** (Chiếu lên mặt).
3. Tích chọn ô **Project Individual Elements** (Chiếu từng đỉnh riêng lẻ).
* *Tác dụng:* Mỗi khi bạn di chuyển một đỉnh mới, đỉnh đó sẽ tự động "hít dính" chặt chẽ vào bề mặt của khối tượng điêu khắc High-poly phía dưới như nam châm hút sắt!

### 2. Hiển thị nổi lên trên cùng (In Front)
Chọn mô hình Low-poly đang dựng:
* Vào bảng thuộc tính **Object Properties** (biểu tượng hình vuông màu cam bên phải).
* Mở mục **Viewport Display**, tích chọn ô **In Front**. Lưới Low-poly của bạn sẽ luôn hiển thị nổi rõ ràng phía trên khối điêu khắc mà không bị chìm khuất vào bên trong thịt.

### 3. Kết hợp Bộ Điều Chỉnh Bọc Dính (Shrinkwrap Modifier)
Thêm **Shrinkwrap Modifier** vào mô hình Low-poly:
* Tại ô **Target**: Dùng bút chấm chỉ định vào khối tượng High-poly.
* Tại ô **Offset**: Đặt `0.002m` để đẩy nhẹ lưới Low-poly nổi hẳn lên bề mặt một khoảng 2 milimét cực kỳ dễ nhìn.

---

## 4. Hai Phương Pháp Đi Lưới Thực Chiến

### Phương pháp 1: Dùng Công Cụ Chuyên Dụng Poly Build
1. Chọn công cụ **Poly Build** trên thanh Toolbar bên trái.
2. Click chuột trái kéo một cạnh ra ngoài: Một mặt Quad 4 đỉnh mới sẽ lập tức được sinh ra và dính chặt vào bề mặt tượng.
3. Giữ phím `[Ctrl] + Click chuột trái`: Tạo đỉnh mới.
4. Giữ phím `[Shift] + Click cạnh`: Trượt dịch chuyển vị trí cạnh.
5. Đây là công cụ cực nhanh để đi các dải vòng lặp quanh mắt và miệng.

### Phương pháp 2: Phương pháp Extrude Truyền Thống
1. Chọn một cạnh, nhấn phím `[E]` đùn ra nấc tiếp theo.
2. Khi hai mép cạnh tiến lại gần nhau, chọn 2 cạnh đối diện và nhấn phím `[F]` để đan kín thành mặt Quad.
3. Kết hợp bật tính năng **Auto Merge** (biểu tượng hai mũi tên chạm nhau góc trên bên phải Viewport): Khi kéo hai đỉnh chạm sát nhau, chúng sẽ tự động hàn liền làm một.

---

## Bài tập thực hành

**Mục tiêu:** Dựng lưới Retopology cho nửa khuôn mặt nhân vật từ khối tượng tròn trong 15 phút.

1. Đặt tên khối tượng điêu khắc là `Character_HighPoly`.
2. Nhấn `[Shift + A]` tạo một mặt phẳng **Mesh > Plane**, đặt tên là `Character_LowPoly`.
3. Chuyển sang Edit Mode, nhấn `[1]` chọn 3 đỉnh xóa đi, chỉ giữ lại đúng 1 đỉnh duy nhất đặt ngay sát khóe mắt của khối tượng.
4. Bật chế độ **Snap to Face Project** và bật **In Front**.
5. Thêm **Mirror Modifier** (tích chọn trục `X` và bật ô **Clipping**) để làm một bên tự sinh bên đối diện.
6. Thêm **Shrinkwrap Modifier**, chọn Target là `Character_HighPoly`.
7. Dùng phím `[E]` đùn đỉnh đi một vòng tròn khép kín bao quanh hốc mắt (khoảng 8 đến 10 cạnh). Chọn hai đỉnh cuối nhấn `[F]` nối lại.
8. Chọn toàn bộ vòng cạnh quanh mắt, nhấn `[E]` đùn nở rộng ra ngoài theo hướng gò má và trán.
9. Đùn một dải cạnh dọc theo sống mũi chạy thẳng xuống nhân trung và cằm (chạm vào đường ranh giới Mirror sẽ tự dính chặt).
10. Nối các khoảng trống giữa trán và gò má thành các mặt quad 4 cạnh đều đặn. Kiểm tra lưới sạch sẽ, sẵn sàng cho công đoạn trải UV.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/editors/3dview/controls/snapping.html
- https://docs.blender.org/manual/en/5.2/modeling/modifiers/deform/shrinkwrap.html
- https://docs.blender.org/manual/en/5.2/modeling/meshes/tools/poly_build.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
