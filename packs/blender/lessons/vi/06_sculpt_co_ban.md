# Bài 06: Nhập Môn Điêu Khắc Kỹ Thuật Số (Digital Sculpting) trong Blender 5.2

> **Danh mục:** Điêu Khắc & Sculpting
> **Tags:** sculpt, brushes, dyntopo, remesh, mask, faceset, meshfilter

---

## 1. Bản chất của Điêu Khắc 3D (Digital Sculpting)

Nếu như quy trình Modeling đa giác truyền thống giống như kỹ thuật hàn các thanh sắt và tấm tôn lại với nhau, thì **Điêu Khắc (Sculpting)** mang lại trải nghiệm hoàn toàn tự nhiên như đang nhào nặn một khối đất sét ngoài đời thực. Bạn không cần bận tâm về việc nối từng đỉnh hay chia từng mặt đa giác, mà chỉ tập trung vào hình khối (Form), tỷ lệ (Proportion), giải phẫu (Anatomy) và đường nét cảm xúc của nhân vật.

Trong quy trình sản xuất nhân vật game hiện đại, Sculpting là giai đoạn tạo ra mô hình chi tiết cao độ (**High-Poly Model**) chứa hàng triệu đa giác, làm cơ sở để nướng chi tiết nếp nhăn, lỗ chân lông và cơ bắp sang mô hình game gọn nhẹ.

---

## 2. Hệ Thống Cọ Điêu Khắc (Sculpt Brushes) Chủ Đạo

Blender 5.2 sở hữu kho cọ điêu khắc phong phú được phân nhóm logic theo chức năng:

### 1. Nhóm cọ Định Hình & Kéo Khối (Shape & Silhouette)
* **Grab Brush (Phím `[G]`):** Cọ kéo thể tích. Dùng đầu cọ kích thước lớn để kéo dài chân tay, nắn cằm, nâng mũi, điều chỉnh phom dáng tổng thể.
* **Snake Hook (Phím `[K]`):** Cọ móc kéo dải. Giống như kéo một sợi đất sét dài ra khỏi khối chính, cực kỳ hữu dụng để kéo sừng quái vật, lọn tóc, ngón tay hoặc xúc tu.
* **Elastic Deform:** Biến dạng đàn hồi, giữ nguyên thể tích xung quanh khi bạn kéo dãn một bộ phận.

### 2. Nhóm cọ Đắp Đất & Xây Dựng Khối (Volume & Buildup)
* **Clay Brush (Phím `[C]`):** Cọ đắp đất tròn. Đắp thêm từng lớp đất sét mỏng dần lên bề mặt.
* **Clay Strips:** Cọ đắp đất bản dẹt. Đắp các dải cơ bắp hình chữ nhật xếp chồng lên nhau rất chắc chắn và dứt khoát. Đây là cọ được các họa sĩ chuyên nghiệp sử dụng nhiều nhất ở giai đoạn phác thảo cơ thể.
* **Draw:** Đắp hoặc khắc rãnh theo nét vẽ tự nhiên.
* **Inflate (Phím `[I]`):** Cọ bơm phồng. Làm nở tròn đều vùng hình học được quét qua như thổi bong bóng.

### 3. Nhóm cọ Chạm Khắc & Tạo Đường Gờ Sắc (Crease & Detail)
* **Crease (Tổ hợp `[Shift + C]`):** Khắc các đường rãnh sâu sắc nhọn (như nếp nhăn khóe mắt, khe rãnh múi bụng, nếp gấp áo quần).
* **Pinch (Phím `[P]`):** Cọ véo. Gom các đỉnh lại gần nhau để làm mép gờ trở nên bén ngót.
* **Flatten / Scrape:** Cọ mài phẳng. Gọt giũa bề mặt lồi lõm thành các mặt phẳng dứt khoát, thường dùng để chặn mảng gương mặt hoặc giáp trụ Stylized.

### 4. Cọ Làm Mịn Thần Thánh (Smooth Brush)
* Bất cứ khi nào đang dùng bất kỳ loại cọ nào, chỉ cần **nhấn giữ phím `[Shift] + quét chuột trái**, Blender sẽ tức thì kích hoạt cọ **Smooth** để làm phẳng và mượt mà mọi vết lồi lõm thô ráp.

---

## 3. Quản Lý Mật Độ Lưới: Voxel Remesh vs Dyntopo

Để điêu khắc được chi tiết, mô hình cần có đủ số lượng đỉnh (Vertices). Blender 5.2 cung cấp hai cơ chế tái cấu trúc lưới tối tân:

```text
┌────────────────────────────────────────────────────────┐
│ SO SÁNH HAI CƠ CHẾ QUẢN LÝ LƯỚI TRONG SCULPT MODE     │
├──────────────────────────┬─────────────────────────────┤
│ Voxel Remesh [Ctrl + R]  │ Dynamic Topology [Ctrl + D] │
├──────────────────────────┼─────────────────────────────┤
│ • Tính toán lại TOÀN BỘ  │ • Chỉ sinh đỉnh TẠI NƠI     │
│   lưới thành các khối ô  │   cọ vẽ quét qua            │
│   vuông đồng nhất        │ • Tự động co giãn mật độ    │
│ • Hàn liền các khối rời  │ • Không đều toàn thể        │
│ • Rất sạch sẽ, ổn định   │ • Xóa sạch UV và Color      │
│ • Dùng cho chặn dáng lớn │ • Dùng phác thảo nhanh      │
└──────────────────────────┴─────────────────────────────┘
```

### Cách dùng Voxel Remesh chuẩn xác
1. Trong Sculpt Mode, nhấn phím **`[R]`**. Một mạng lưới ô vuông biểu diễn trực quan sẽ xuất hiện trên bề mặt vật thể.
2. Rê chuột để phóng to ô lưới (khoảng `0.05m` cho giai đoạn thô) hoặc thu nhỏ (khoảng `0.01m` cho giai đoạn chi tiết vừa). Click chuột trái xác nhận.
3. Nhấn tổ hợp phím **`[Ctrl + R]`**. Toàn bộ cấu trúc lưới sẽ được tính toán lại tinh tươm thành các mặt quad đều chằn chặn.

---

## 4. Kiểm Soát Vùng Tác Động: Mặt Nạ (Mask) và Tập Hợp Mặt (Face Sets)

### Mặt Nạ (Masking)
Khi điêu khắc môi dưới, bạn không muốn cọ làm ảnh hưởng méo mó môi trên. Mặt nạ là giải pháp cô lập vùng:
* Phím `[M]`: Dùng cọ vẽ vùng màu đen xám (vùng được bảo vệ). Cọ điêu khắc sẽ không thể tác động lên vùng có mặt nạ.
* Phím `[Ctrl + Chuột trái]` với cọ Mask: Xóa bớt mặt nạ.
* Tổ hợp `[Ctrl + I]`: Đảo ngược vùng mặt nạ.
* Tổ hợp `[Alt + M]`: Xóa toàn bộ mặt nạ.
* Tổ hợp `[Shift + A]`: Mở menu rẻ quạt **Mask Pie** (Làm mờ mặt nạ *Smooth Mask*, Tăng độ sắc *Sharpen Mask*).

### Tập Hợp Mặt (Face Sets)
Phân chia nhân vật thành các vùng màu nhận diện trực quan:
* Phím `[Ctrl + W]`: Khởi tạo Face Set mới cho vùng đang hiển thị.
* Phím `[W]`: Mở menu rẻ quạt Face Sets.
* Phím `[H]`: Trỏ chuột vào một Face Set và nhấn `[H]` để ẩn giấu nó đi, giúp bạn dễ dàng điêu khắc vào những góc khuất như kẽ ngón tay, nách hoặc mặt trong vòm miệng. Nhấn `[Alt + H]` để hiện lại tất cả.

---

## 5. Bộ Lọc Toàn Thể (Mesh Filter) và Tính Năng Đối Xứng (Symmetry)

* **Mesh Filter:** Chọn công cụ Mesh Filter trên toolbar. Nhấp chuột trái lên khoảng trống màn hình và kéo chuột sang phải. Toàn bộ mô hình sẽ đồng loạt được Áp dụng bộ lọc:
  * *Smooth:* Làm mịn đều toàn thân nhân vật trong 1 giây.
  * *Inflate:* Bơm nở căng toàn bộ cơ thể.
  * *Relax:* Thư giãn các đỉnh lưới bị xô lệch mà không làm teo thể tích.
* **Tính năng đối xứng gương (Symmetry):** Nhấn phím `[X]` hoặc bấm vào biểu tượng chữ X trên thanh đầu trang. Khi bạn nặn mắt, tai, cơ bắp bên trái, Blender sẽ tự động điêu khắc đối xứng hoàn hảo sang bên phải.

---

## Bài tập thực hành

**Mục tiêu:** Điêu khắc một tảng thiên thạch ma thuật phong cách hoạt hình (Stylized Asteroid) có các hố thiên thạch và đường gờ đá sắc nét trong 15 phút.

1. Tạo một khối cầu **UV Sphere**, nhấn `[Tab]` chuyển sang Sculpt Mode.
2. Bật chế độ đối xứng trục `X` bằng phím `[X]`.
3. Chọn cọ **Grab `[G]`**, nhấn `[F]` kéo kích thước cọ thật lớn. Kéo khối cầu méo mó bất đối xứng theo hình dáng một tảng đá tự nhiên.
4. Nhấn `[R]` chỉnh Voxel Size về khoảng `0.03m`, nhấn `[Ctrl + R]` để Remesh lại bề mặt.
5. Chọn cọ **Clay Strips**, vẽ các vệt đất dẹt chồng chéo nhau tạo thành các khối cơ tầng địa chất trên thân đá.
6. Nhấn giữ `[Shift]` quét nhẹ chuột để làm mịn các vùng chuyển tiếp thô ráp.
7. Tạo các hố va chạm tròn: Nhấn giữ `[Ctrl]` kết hợp cọ **Clay** để đục lõm một vài hốc sâu trên thân đá.
8. Chọn cọ **Scrape / Flatten**, gọt phẳng các mặt lồi để tạo các diện cắt đá sắc nét (Chiseled edges).
9. Chọn cọ **Crease `[Shift + C]`**, nhấn `[F]` thu nhỏ bán kính cọ, khắc các đường nứt nẻ uốn lượn xung quanh các hố đá.
10. Dùng cọ **Pinch `[P]`** quét dọc theo các đường nứt để kéo mép nứt khép lại sắc lẹm, hoàn tất tảng đá Stylized tuyệt đẹp.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/sculpt_paint/sculpting/index.html
- https://docs.blender.org/manual/en/5.2/sculpt_paint/sculpting/tools/index.html
- https://docs.blender.org/manual/en/5.2/sculpt_paint/sculpting/editing/sculpt.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
