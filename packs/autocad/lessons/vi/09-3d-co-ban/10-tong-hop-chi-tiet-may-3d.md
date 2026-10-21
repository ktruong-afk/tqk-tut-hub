---
id: ac-09-10
title: Bài tập tổng hợp mô hình hoá chi tiết gối đỡ cơ khí 3D
category: Mô hình hoá 3D
tags: [tong-hop, 3d-solid, co-khi, boolean, flatshot, bai-tap]
level: intermediate
minutes: 30
needs: [ac-09-05, ac-09-07, ac-09-08]
appVersions: ['2024', '2025']
edition: full-only
---
# Bài tập tổng hợp mô hình hoá chi tiết gối đỡ cơ khí 3D

> **Mục tiêu:**
> - Áp dụng quy trình phối hợp các khối sơ khai, đùn khối và phép toán Boolean để dựng gối đỡ trục hoàn chỉnh.
> - Gia công mép cạnh với `FILLETEDGE` và `CHAMFEREDGE` đạt độ thẩm mỹ cơ khí chính xác cao.
> - Trích xuất các hình chiếu 2D kỹ thuật bằng `FLATSHOT` và kiểm tra thể tích khối lượng với `MASSPROP`.

## Dự án thực hành: Chế tạo gối đỡ trục đỡ vòng bi

Trong bài học tổng kết chặng 3D này, bạn sẽ vào vai một kỹ sư thiết kế chế tạo máy hoàn thiện trọn vẹn chi tiết gối đỡ trục (Bearing Pillow Block) từ bản phác thảo ý tưởng ban đầu đến hồ sơ sản xuất 2D.

Một chi tiết máy 3D đạt chuẩn cần đáp ứng 3 tiêu chuẩn cốt lõi:
1. **Tính liền khối (Solid Integrity):** Toàn bộ các bộ phận (bích đáy, thân gối, tai bắt bu lông) phải được liên kết thành một khối Solid duy nhất qua lệnh `UNION`, không có các mặt phẳng giao nhau ngầm bên trong.
2. **Gia công mép cạnh chuẩn mực:** Các cạnh tiếp xúc chịu tải được bo tròn với bán kính lượn đúc, các miệng lỗ ren được vát mép dẫn hướng cho bu lông.
3. **Trích xuất hồ sơ gia công:** Mô hình 3D sẵn sàng xuất bản vẽ 2D qua lệnh `FLATSHOT` và kiểm tra khối lượng phôi thép qua `MASSPROP`.

![Tổng hợp chi tiết máy 3D gối đỡ trục](media/ac-09-10-tong-hop-3d-part.svg)

```hotspots
image: media/ac-09-10-tong-hop-3d-part.svg
alt: Quy trình dựng hình chi tiết gối đỡ trục cơ khí 3D hoàn chỉnh
layout: central
points:
  - id: spot-1
    x: 50
    y: 20
    title: Thân gối trụ đỡ và lỗ trục chính
    text: "Tạo bằng CYLINDER và khoét rỗng bằng SUBTRACT đường kính Ø50mm."
  - id: spot-2
    x: 25
    y: 45
    title: Bo tròn góc đế (FILLETEDGE R10)
    text: "Bo tròn 4 góc sắc nhọn của tấm bích đế để tăng độ an toàn và thẩm mỹ."
  - id: spot-3
    x: 23
    y: 80
    title: 1. Dựng khối đế & thân trụ
    text: "Kết hợp khối hộp chữ nhật BOX và khối hình trụ CYLINDER."
  - id: spot-4
    x: 50
    y: 80
    title: 2. Boolean & Khoét lỗ
    text: "Hợp nhất bằng UNION và đục khoét 2 lỗ bu lông tai bích bằng SUBTRACT."
```

## Quy trình 4 bước dựng hình chi tiết máy hoàn chỉnh

### Bước 1: Dựng các khối sơ khai (Base Primitives)
1. Chuyển sang góc nhìn `SW Isometric` và đổi kiểu hiển thị sang `Shaded with Edges`.
2. Tạo tấm bích đế: Gõ `BOX`, vẽ khối hộp kích thước dài 160mm, rộng 80mm, dày 20mm.
3. Tạo thân trụ gối đỡ: Gõ `CYLINDER`, đặt tâm tại chính giữa mặt trên của bích đế, bán kính 40mm, chiều cao 70mm.
4. Gõ `UNION` (UNI), quét chọn cả khối hộp và khối trụ để hợp nhất thành một thân máy liền khối.

### Bước 2: Khoét lỗ trục và lỗ bu lông bắt sàn
1. Khoét lỗ trục chính:
   - Dùng lệnh `UCS` chọn tuỳ chọn `Face`, áp mặt phẳng vẽ lên mặt phẳng ngang của thân trụ.
   - Gõ `CYLINDER`, bắt đúng tâm của thân trụ, bán kính 25mm (đường kính Ø50mm), chiều cao 80mm đâm xuyên xuống đáy.
2. Tạo 2 lỗ bắt bu lông bích đáy:
   - Dùng `CYLINDER` vẽ 2 hình trụ bán kính 7mm (đường kính Ø14mm), cao 30mm đặt cách đều 2 mép ngoài 25mm.
3. Gõ `SUBTRACT` (SU):
   - Bấm chọn thân máy chính, nhấn [Enter].
   - Quét chọn lỗ trục chính và 2 hình trụ bu lông, nhấn [Enter].
   - Ba lỗ khoan thông suốt xuất hiện sắc nét trên thân chi tiết!

### Bước 3: Gia công mép cạnh (Fillet & Chamfer)
1. Bo tròn 4 góc sắc của tấm bích đế:
   - Gõ `FILLETEDGE`, nhập `R` đặt bán kính `10` mm.
   - Bấm chọn 4 cạnh đứng ở 4 góc của bích đế, nhấn Enter hai lần.
2. Vát mép miệng lỗ trục chính để dễ lắp bạc đạn:
   - Gõ `CHAMFEREDGE`, nhập `D` đặt khoảng cách vát `2` mm cho cả hai cạnh.
   - Bấm chọn đường chu vi miệng lỗ tròn trên đỉnh, nhấn Enter hai lần.

### Bước 4: Kiểm tra khối lượng và trích xuất hình chiếu 2D
1. Gõ `MASSPROP`, bấm chọn chi tiết máy:
   - Ghi nhận thông số thể tích thể tích thép: $Volume \approx 385,420\text{ mm}^3$.
   - Tính toán nhanh: Với khối lượng riêng của thép là $7.85\text{ g/cm}^3$, chi tiết nặng khoảng $3.02\text{ kg}$.
2. Gõ `FLATSHOT`:
   - Tick chọn *Show Obscured lines* (nét khuất màu đỏ nét đứt).
   - Bấm Create và đặt hình chiếu 2D trục đo ra mặt phẳng vẽ để phục vụ in ấn thuyết minh kỹ thuật.

> [!TIP]
> Sử dụng lệnh `3DROTATE` xoay chi tiết quanh trục X một góc 90 độ nếu bạn muốn đặt gối đỡ nằm ngang theo phương của trục truyền động trước khi xuất bản vẽ chiếu đứng.

## Tự kiểm tra

```quiz
id: q-ac-09-10-1
type: single
question: "Trong quy trình dựng hình cơ khí 3D tiêu chuẩn, bước nào nên được thực hiện ở giai đoạn cuối cùng sau khi đã hoàn tất các phép toán Boolean?"
options:
  - text: "Gia công mép cạnh với FILLETEDGE và CHAMFEREDGE"
    correct: true
    why: "Bo viền và vát mép ở bước cuối cùng giúp tránh làm hỏng các đường biên cạnh trong quá trình cộng trừ khối Boolean."
  - text: "Dựng khối hộp chữ nhật bích đế"
    correct: false
    why: "Khối đế là bước tạo hình sơ khai ban đầu."
  - text: "Tạo các lỗ khoan trụ tròn"
    correct: false
    why: "Khoét lỗ được thực hiện trước khi bo mép."
  - text: "Đổi màu màn hình sang màu xanh"
    correct: false
    why: "Không liên quan đến quy trình mô hình hóa."
explain: "Nguyên tắc vàng của mô hình hóa 3D Solid: Dựng khối thô $\to$ Boolean khoét đắp $\to$ Gia công tinh bo vát mép cạnh ở bước cuối cùng."
```

```quiz
id: q-ac-09-10-2
type: single
question: "Lệnh nào cho phép trích xuất nhanh hình ảnh phối cảnh trục đo 3D thành một khối Block 2D có đầy đủ nét thấy và nét khuất?"
options:
  - text: "FLATSHOT"
    correct: true
    why: "FLATSHOT ép góc nhìn 3D hiện hành thành đối tượng 2D phẳng phục vụ in ấn bản vẽ kỹ thuật."
  - text: "MASSPROP"
    correct: false
    why: "MASSPROP dùng để tra cứu khối lượng thể tích."
  - text: "EXPLODE"
    correct: false
    why: "EXPLODE làm nổ tung đối tượng."
  - text: "PURGE"
    correct: false
    why: "PURGE dùng dọn dẹp rác tệp tin."
explain: "Lệnh FLATSHOT là công cụ hoàn hảo để chuyển giao dữ liệu từ mô hình 3D sang hồ sơ in ấn 2D."
```

```quiz
id: q-ac-09-10-3
type: truefalse
question: "Thông số thể tích Volume tính bằng lệnh MASSPROP có thể dùng để nhân với khối lượng riêng của vật liệu nhằm dự toán chính xác trọng lượng của chi tiết gia công."
answer: true
explain: "Khối lượng $M = V \times D$. Tính năng tính thể tích chính xác của 3D Solid giúp kỹ sư dự toán nguyên vật liệu đúc phôi cực kỳ chính xác."
```

## Lỗi thường gặp

- **Bo mép cạnh FILLETEDGE bị vỡ bề mặt:** Do bán kính bo R quá lớn lấn vào mép của lỗ khoan bu lông lân cận. Khắc phục: Giảm bán kính bo tròn nhỏ hơn khoảng cách từ cạnh tới mép lỗ khoan.
- **Không Flatshot được:** Do đang mở góc nhìn trong không gian giấy Layout. Lệnh `FLATSHOT` chỉ chạy được trong không gian mô hình `Model Space`.

## Bài tập thực hành

- [ ] Dùng `BOX` vẽ khối đế 160 x 80 x 20 mm. <!-- expect: BOX -->
- [ ] Dùng `CYLINDER` vẽ thân trụ gối đỡ bán kính 40mm, cao 70mm ở giữa mặt trên khối đế. <!-- expect: CYLINDER -->
- [ ] Gõ `UNION` (hoặc `UNI`), gộp khối đế và khối trụ thành một thể thống nhất. <!-- expect: UNION -->
- [ ] Dùng `CYLINDER` vẽ trụ tâm bán kính 25mm, cao 80mm và dùng `SUBTRACT` khoét lỗ trục chính. <!-- expect: SUBTRACT -->
- [ ] Dùng `FILLETEDGE` bo tròn 4 cạnh góc đế với bán kính 10mm. <!-- expect: FILLETEDGE -->
- [ ] Gõ lệnh `MASSPROP`, kiểm tra thể tích và khối lượng của chi tiết vừa hoàn thiện. <!-- expect: MASSPROP -->
- [ ] Gõ lệnh `FLATSHOT`, xuất khối hình chiếu 2D trục đo ra màn hình bản vẽ. <!-- expect: FLATSHOT -->

## Nguồn tham khảo

```links
- title: "Quy trình thiết kế mô hình 3D Solid từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=3D+Solid+Design"
  kind: official
- title: "Lệnh FLATSHOT tạo hình chiếu 2D từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=FLATSHOT"
  kind: official
```
