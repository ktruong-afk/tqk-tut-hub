# Bài 15: Thiết Lập Ánh Sáng và Kết Xuất (Lighting & Rendering) Đẳng Cấp với EEVEE và Cycles trong Blender 5.2

> **Danh mục:** Ánh Sáng & Kết Xuất
> **Tags:** lighting, rendering, eevee, cycles, three-point-lighting, hdri, raytracing, blender52

---

## 1. Hai Bộ Máy Kết Xuất Hùng Mạnh trong Blender 5.2

Để giới thiệu nhân vật trên ArtStation, danh mục Portfolio cá nhân hay làm ảnh bìa cho game trên Steam, bạn cần biến mô hình 3D thành những tác phẩm hình ảnh mãn nhãn. Blender 5.2 trang bị hai bộ máy kết xuất (Render Engines) đẳng cấp thế giới:

```text
┌─────────────────────────────────────────────────────────────┐
│ EEVEE (EEVEE-Next)          vs       CYCLES (Path Tracing)  │
├──────────────────────────────────────┼──────────────────────┤
│ • Thời gian thực (Real-time)         │ • Dò tia vật lý chân thực    │
│ • Tốc độ: Vài mili-giây / khung hình │ • Tốc độ: Vài giây đến phút  │
│ • Hoạt động giống hệt game engine    │ • Nảy sáng toàn cục (GI)     │
│ • Dùng kiểm tra game & render nhanh  │ • Dùng làm Poster & Bake map │
└──────────────────────────────────────┴──────────────────────┘
```

---

## 2. Hệ Thống Chiếu Sáng 3 Điểm Chuẩn Studio (Three-Point Lighting)

Đừng bao giờ chỉ đặt duy nhất một bóng đèn rọi thẳng mặt nhân vật – điều đó sẽ làm mô hình trông bẹp dúm và thiếu sức sống. Quy chuẩn nghệ thuật kinh điển của Hollywood và ngành game là **Hệ Thống Chiếu Sáng 3 Điểm**:

```text
                           [Rim Light - Đèn Viền Lưng]
                                      ▲
                                      │
                                [Nhân Vật 3D]
                                  /       \
                                 /         \
                                ▼           ▼
           [Key Light - Đèn Chính]         [Fill Light - Đèn Phụ]
           (Góc 45 độ, Công suất 100%)     (Góc đối diện, Công suất 30%)
```

### 1. Đèn Chính (Key Light):
* **Vị trí:** Đặt lệch một góc 45 độ so với trục nhìn của camera, chếch cao hơn đầu nhân vật 45 độ.
* **Vai trò:** Cung cấp nguồn sáng chủ đạo mạnh mẽ nhất (100% công suất), tạo ra các mảng khối sáng tối tương phản rõ rệt trên cơ bắp và khuôn mặt.

### 2. Đèn Phụ Bù Sáng (Fill Light):
* **Vị trí:** Đặt ở phía đối diện với đèn chính (góc -45 độ), ngang tầm mắt nhân vật.
* **Vai trò:** Đặt công suất mềm hơn (khoảng 30% đến 50% so với đèn chính). Nhiệm vụ của nó là chiếu sáng nhẹ nhàng vào các hốc mắt và vùng bóng tối do đèn chính tạo ra, ngăn không cho bóng tối bị đen kịt mất chi tiết.

### 3. Đèn Viền Tách Nền (Rim Light / Back Light):
* **Vị trí:** Đặt ở phía sau lưng nhân vật, rọi ngược trở lại hướng camera.
* **Vai trò:** Chiếu một vệt sáng mỏng sắc bén ôm dọc theo vành tai, bờ vai và mái tóc của nhân vật. Vệt sáng viền này tạo ra độ tương phản mạnh mẽ, giúp tách biệt nhân vật nổi bật hẳn lên phía trên phông nền tối.

---

## 4. Các Loại Nguồn Sáng Thông Dụng trong Blender

Nhấn `[Shift + A] > Light` để thêm nguồn sáng:
* **Area Light (Đèn tấm tản sáng):** Nguồn sáng được khuyên dùng nhiều nhất trong studio chân dung. Bạn có thể kéo kích thước tấm đèn to ra (ví dụ `1m x 1m`) để tạo bóng đổ siêu mềm mại, mịn màng tự nhiên.
* **Point Light (Đèn điểm tỏa tròn):** Tỏa ánh sáng hình cầu 360 độ từ một điểm (thích hợp cho đuốc ma thuật, bóng đèn dây tóc).
* **Spot Light (Đèn rọi sân khấu):** Gom ánh sáng thành một hình nón có góc mở (dùng tạo luồng sáng bí ẩn).
* **Sun Light (Đèn mặt trời):** Nguồn sáng vô tận với các tia sáng song song, công suất chỉ phụ thuộc vào góc xoay chứ không phụ thuộc vào vị trí xa gần.

---

## 5. Môi Trường Chiếu Sáng Thực Tế Bằng HDRI (High Dynamic Range Image)

Một bức ảnh HDRI chụp toàn cảnh 360 độ của một khu rừng, hoàng hôn hay đường phố sẽ mang lại hàng triệu thông tin màu sắc môi trường phản chiếu chân thực lên giáp sắt và mắt nhân vật:
1. Mở cửa sổ **Shader Editor**, ở góc trên bên trái, đổi chế độ từ *Object* sang **World**.
2. Nhấn `[Shift + A]` thêm node **Texture > Environment Texture**.
3. Bấm **Open**, chọn file ảnh định dạng `.hdr` hoặc `.exr`.
4. Nối cổng *Color* của node Environment Texture vào cổng *Color* của node **Background**.
5. Toàn bộ cảnh vật sẽ tức thì được chiếu sáng bởi ánh sáng tự nhiên tuyệt mỹ từ môi trường thực.

---

## 6. Cấu Hình Tối Ưu Render trong Blender 5.2

### 1. Bật Dò Tia trong EEVEE 5.2:
* Trong bảng **Render Properties**:
  * Đổi Render Engine sang **EEVEE**.
  * Tích chọn mục **Raytracing**.
  * Mở rộng mục Raytracing, tích chọn **Fast GI Approximation** (để mô phỏng ánh sáng nảy gián tiếp nhanh như game AAA).

### 2. Khử Nhiễu Thông Minh (Denoising) trong Cycles:
* Trong Cycles, thay vì tăng số mẫu (Samples) lên hàng ngàn làm máy chạy chậm như rùa, bạn chỉ cần đặt:
  * **Max Samples = 256** hoặc `512`.
  * Tích chọn ô **Denoise** (chọn thuật toán *OpenImageDenoise* hoặc *OptiX* nếu dùng card NVIDIA).
  * Bộ khử nhiễu trí tuệ nhân tạo sẽ quét sạch toàn bộ hạt sạn (Noise), cho ra bức ảnh mịn bóng chỉ sau vài giây tính toán!

### 3. Quản Lý Màu Sắc Điện Ảnh (AgX View Transform):
* Trong bảng **Render Properties > Color Management**:
  * Mục **View Transform**: Blender 5.2 mặc định sử dụng hệ màu **AgX** (thay thế cho Filmic cũ).
  * AgX xử lý cực kỳ xuất sắc các vùng ánh sáng quá gắt (High highlights), ngăn không cho da mặt nhân vật bị cháy màu vàng khè hay mất chi tiết.

---

## Bài tập thực hành

**Mục tiêu:** Thiết lập một studio ánh sáng 3 điểm hoàn chỉnh và kết xuất một bức ảnh chân dung nhân vật chuẩn Portfolio trong 15 phút.

1. Đặt mô hình nhân vật ở vị trí tâm cảnh `(0, 0, 0)`.
2. Nhấn `[Shift + A]` > **Camera**, nhấn `[Ctrl + Alt + Numpad 0]` để đưa góc nhìn hiện tại vào ống kính máy quay.
3. Trong bảng Camera, đổi tiêu cự **Focal Length = 85mm** (tiêu cự vàng chụp chân dung, loại bỏ hiện tượng méo góc của ống kính rộng).
4. Nhấn `[Shift + A]` > **Light > Area** đặt làm đèn Key Light ở góc trước bên phải, hướng rọi vào mặt, chỉnh công suất `Power = 150W`, kích thước `Size = 1.0m`.
5. Tạo Area Light thứ hai đặt làm Fill Light ở bên trái, `Power = 50W`, kích thước `Size = 1.5m`.
6. Tạo Point Light hoặc Area Light nhỏ thứ ba đặt sau gáy làm Rim Light, `Power = 200W`, màu hơi ánh xanh lam nhẹ.
7. Chuyển sang chế độ xem **Rendered `[Z]`**, tinh chỉnh vị trí các đèn sao cho có một đốm sáng nhỏ (Catchlight) phản chiếu long lanh trong tròng mắt nhân vật.
8. Nhấn phím **`[F12]`** để kết xuất bức ảnh chân dung hoàn thiện. Nhấn `[Alt + S]` trong cửa sổ Image để lưu ảnh kỷ niệm!

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/render/lights/light_object.html
- https://docs.blender.org/manual/en/5.2/render/eevee/index.html
- https://docs.blender.org/manual/en/5.2/render/cycles/index.html
- https://docs.blender.org/manual/en/5.2/render/color_management.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
