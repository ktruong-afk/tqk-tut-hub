# Bài 10: Vật Liệu PBR và Làm Chủ Node Principled BSDF Chuẩn Blender 5.2

> **Danh mục:** Vật Liệu & Shading
> **Tags:** pbr, shading, principledbsdf, material, roughness, metallic, normalmap, eevee, cycles

---

## 1. Bản Chất của Hệ Thống Vật Liệu PBR (Physically Based Rendering)

Trong kỷ nguyên game 3D hiện đại, tiêu chuẩn đồ họa thống trị từ Blender, Substance Painter đến Unity Engine chính là **PBR (Physically Based Rendering - Kết xuất dựa trên vật lý)**. 

Khác với các kỹ thuật tô màu truyền thống vẽ sẵn bóng đổ (Baked Lighting) lên ảnh, quy trình PBR mô phỏng chính xác các định luật quang học ngoài đời thực:
1. **Định luật bảo toàn năng lượng (Conservation of Energy):** Một bề mặt không thể phản xạ lượng ánh sáng nhiều hơn lượng ánh sáng nó nhận được.
2. **Hiệu ứng phản xạ đổi góc (Fresnel Effect):** Mọi vật thể khi nhìn ở góc nghiêng tiếp xúc (Grazing Angle) đều phản xạ ánh sáng mạnh hơn nhiều so với khi nhìn trực diện.
3. **Tính tương thích xuyên nền tảng:** Một vật thể được tạo chất cảm chuẩn PBR trong Blender sẽ giữ nguyên vẹn độ bóng bẩy, độ nhám kim loại khi nạp vào Unity dưới bất kỳ điều kiện nguồn sáng nào (trời nắng gắt, hoàng hôn hay hang tối).

---

## 2. Giải Mã Node "Vạn Năng" Principled BSDF trong Blender 5.2

Trong không gian làm việc **Shading**, trung tâm của mọi vật liệu là node **Principled BSDF** (được nâng cấp toàn diện dựa trên mô hình OpenPBR tiêu chuẩn công nghiệp). Hầu như 98% mọi chất liệu trong thế giới thực đều có thể thiết lập từ node duy nhất này.

```text
┌────────────────────────────────────────────────────────┐
│             NODE PRINCIPLED BSDF (v2 / OpenPBR)        │
├────────────────────────────────────────────────────────┤
│ • Base Color          ──────→ Màu sắc gốc (Albedo)     │
│ • Metallic (0.0 / 1.0)──────→ Kim loại hay Phi kim     │
│ • Roughness           ──────→ Độ nhám mịn bề mặt       │
│ • IOR                 ──────→ Chiết suất bẻ cong sáng  │
│ • Subsurface          ──────→ Độ tán xạ da thịt        │
│ • Coat                ──────→ Lớp sơn bóng phủ ngoài   │
│ • Sheen               ──────→ Độ óng ánh lông tơ vải   │
│ • Emission            ──────→ Tự phát sáng quang năng   │
│ • Normal              ──────→ Bản đồ gồ ghề giả lập    │
└────────────────────────────────────────────────────────┘
```

### Các thông số cốt lõi:

#### 1. Base Color (Màu Sắc Gốc - Albedo)
Màu sắc thực tế của bề mặt dưới ánh sáng trắng trung tính, **hoàn toàn không được chứa bóng đổ (Shadows) hay đốm sáng phản chiếu (Highlights)**.

#### 2. Metallic (Độ Dẫn Kim Loại)
* Đặt bằng `0.0`: Vật liệu **Phi kim / Cách điện (Dielectric)** như Da người, Vải vóc, Gỗ, Nhựa, Bê tông, Đá.
* Đặt bằng `1.0`: Vật liệu **Kim loại nguyên chất (Conductor)** như Sắt, Thép, Vàng, Bạc, Đồng.
* *Lưu ý sống còn:* Trong PBR, Metallic gần như chỉ nhận giá trị nhị phân `0.0` hoặc `1.0`. Rất hiếm khi đặt giá trị lưng chừng `0.5` (trừ khi là bề mặt kim loại bị bám lớp bụi bẩn hay rỉ sét chuyển tiếp).

#### 3. Roughness (Độ Nhám Bề Mặt Vi Mô)
Quyết định các cấu trúc gồ ghề hiển vi của bề mặt:
* Gần `0.0`: Bề mặt siêu phẳng nhẵn bóng, phản chiếu hình ảnh xung quanh sắc nét như gương soi hoặc kim loại mạ chrome.
* Gần `1.0`: Bề mặt thô ráp, tia sáng bị tán xạ hỗn loạn theo mọi hướng, tạo ra bóng đổ mờ nhạt (như đất nung, vải thô).

#### 4. IOR (Index of Refraction - Chiết Suất Khúc Xạ)
Đo lường mức độ bẻ cong của tia sáng khi đi từ không khí vào môi trường vật thể:
* Không khí: `1.000`
* Nước: `1.333`
* Thủy tinh / Nhựa thông dụng: `1.450` đến `1.520`
* Kim cương: `2.418`

---

## 3. Các Lớp Hiệu Ứng Nâng Cao Cho Nhân Vật Game

### 1. Tán Xạ Dưới Bề Mặt (Subsurface Scattering - SSS)
Da người, tai, ngón tay hay ngọc bích không phải là khối đặc cản sáng hoàn toàn. Khi có ánh đèn rọi từ sau tai, ánh sáng đỏ sẽ xuyên thấu qua lớp da thịt.
* **Subsurface Weight:** Tỷ lệ kích hoạt hiệu ứng tán xạ da thịt (khoảng `0.2 - 0.4` cho nhân vật người).
* **Subsurface Radius:** Bước sóng xuyên thấu của 3 kênh màu `(Đỏ, Xanh lá, Xanh lam)`. Đối với da người, kênh Đỏ luôn xuyên sâu nhất `(1.0, 0.2, 0.1)`, tạo nên quầng sáng đỏ ấm áp đặc trưng dưới ánh mặt trời.

### 2. Lớp Sơn Bóng Phủ Ngoài (Coat Layer)
Mô phỏng một lớp vecni trong suốt bóng bẩy tráng lên trên bề mặt nền:
* Ứng dụng: Giác mạc trong suốt phủ lên tròng đen của mắt nhân vật, giáp sơn bóng mạ nano, gỗ phủ bóng.
* Chỉnh **Coat Weight = 1.0** và **Coat Roughness = 0.03**.

### 3. Độ Óng Ánh Lông Tơ (Sheen)
Tạo ra một quầng sáng mềm mại bao quanh đường biên của áo quần ở góc nhìn xiên:
* Ứng dụng: Vải nhung, lụa, áo len, nỉ của trang phục nhân vật.

---

## 4. Thiết Lập Vật Liệu Kính Trong Suốt Chuẩn EEVEE 5.2

> **Cập nhật quan trọng trong Blender 5.2:** Tính năng "Screen Space Refraction" cũ của phiên bản Blender 4.1 trở về trước đã hoàn toàn bị loại bỏ. Trong EEVEE 5.2 (EEVEE-Next), hệ thống khúc xạ được vận hành hoàn toàn bởi công nghệ **Raytracing (Dò tia thời gian thực)**.

### Quy trình tạo kính / nước chuẩn Blender 5.2:
1. Gán vật liệu có node **Principled BSDF** cho khối thủy tinh.
2. Trong node Principled BSDF:
   * Kéo thông số **Transmission Weight = 1.0**.
   * Đặt **Roughness = 0.02** đến `0.05`.
   * Đặt **IOR = 1.45**.
3. **Kích hoạt trong EEVEE 5.2:**
   * Vào bảng thuộc tính **Render Properties** (hình mặt sau chiếc máy ảnh), tích chọn bật mục **Raytracing**.
   * Sang bảng **Material Properties**, cuộn xuống mục **Settings**, tích chọn bật ô **Raytraced Transmission**.
   * Mở mục **Thickness**, điều chỉnh độ dày tương ứng của vật thể để khúc xạ tính toán thể tích rỗng/đặc chính xác.

---

## 5. Quy Trình Cắm Dây Texture PBR Chuẩn Quốc Tế

Khi tải hoặc xuất các bộ texture PBR từ Substance Painter, hãy kết nối vào node Principled BSDF theo đúng quy tắc sau:

```text
┌─────────────────────────┐               ┌───────────────────────────┐
│ Image: Base_Color.png   │ ──(sRGB)────→ │ Base Color                │
├─────────────────────────┤               │                           │
│ Image: Metallic.png     │ ──(Non-Color)→│ Metallic                  │
├─────────────────────────┤               │                           │
│ Image: Roughness.png    │ ──(Non-Color)→│ Roughness                 │
├─────────────────────────┤               │                           │
│ Image: Normal.png       │ ──(Non-Color)→│ [Normal Map Node] → Normal│
└─────────────────────────┘               └───────────────────────────┘
```

> **Lưu ý tối quan trọng về Color Space:**
> * Chỉ duy nhất file ảnh chứa thông tin màu sắc hiển thị mắt người nhìn thấy (**Base Color / Albedo**) mới được để hệ màu **sRGB**.
> * Toàn bộ các file ảnh chứa dữ liệu toán học (**Metallic, Roughness, Normal, Ambient Occlusion, Displacement**) BẮT BUỘC phải chuyển Color Space sang **Non-Color**! Nếu quên bước này, độ bóng và độ lồi lõm của nhân vật sẽ bị tính toán sai lệch hoàn toàn.

---

## Bài tập thực hành

**Mục tiêu:** Tạo và tinh chỉnh 3 khối vật liệu PBR đặc trưng cho nhân vật game (Da người có Subsurface, Thép phay xước, và Viên ngọc phép thuật phát sáng) trong 15 phút.

1. Tạo 3 khối cầu UV Sphere đặt thẳng hàng nhau dọc theo trục X. Nhấp chuột phải chọn **Shade Smooth by Angle**.
2. **Khối cầu 1 (Vật liệu Da người Stylized):**
   * Tạo vật liệu mới đặt tên là `M_Skin`.
   * Base Color: Màu da đào nhẹ `#E8B898`.
   * Metallic: `0.0`. Roughness: `0.45`.
   * Cuộn đến mục *Subsurface*: Kéo `Subsurface Weight = 0.35`, Radius chỉnh kênh Đỏ cao hơn. Quan sát rìa khối cầu ửng hồng ấm áp tự nhiên.
3. **Khối cầu 2 (Giáp thép phay xước):**
   * Tạo vật liệu mới đặt tên là `M_Steel`.
   * Base Color: Xám nhạt `#D0D0D0`.
   * Metallic: Kéo kịch kim `1.0`. Roughness: `0.25`.
   * Trong Shader Editor, nhấn `[Shift + A]` thêm node **Noise Texture**, nối cổng *Fac* vào cổng *Roughness* của Principled BSDF để tạo các vết loang lổ cọ xát cơ khí.
4. **Khối cầu 3 (Ngọc thần phát sáng):**
   * Tạo vật liệu mới đặt tên là `M_MagicCrystal`.
   * Base Color: Xanh lam dạ quang `#00E5FF`.
   * Cuộn xuống mục *Emission*: Đổi **Emission Color** sang màu xanh lam, tăng **Emission Strength = 5.0**.
   * Nhấn phím `[Z]` chọn chế độ **Rendered** để thưởng thức khối ngọc tỏa ánh hào quang rực rỡ trong bóng tối.

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/render/shader_nodes/shader/principled.html
- https://docs.blender.org/manual/en/5.2/render/eevee/materials/settings.html
- https://docs.blender.org/manual/en/5.2/render/materials/components/index.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
