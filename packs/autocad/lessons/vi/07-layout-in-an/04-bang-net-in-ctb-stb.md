---
id: ac-07-04
title: Quản lý độ dày và màu sắc nét in với bảng Plot Style (CTB)
category: Layout và In ấn
tags: [ctb, plot-style, lineweight, in-an, stylesmanager]
level: intermediate
minutes: 25
needs: [ac-07-02]
appVersions: ['2024', '2025']
edition: all
---
# Quản lý độ dày và màu sắc nét in với bảng Plot Style (CTB)

> **Mục tiêu:**
> - Hiểu nguyên lý ánh xạ màu sắc màn hình sang nét in của bảng phong cách in [[Plot Style]] dạng CTB.
> - Thiết lập bảng nét in chuyên nghiệp: đổi toàn bộ nét sang màu đen (Black) và gán độ dày lineweight theo màu.
> - Mở thư mục quản lý file nét in với lệnh `STYLESMANAGER` để sao lưu và chia sẻ trong công ty.

## Nét in: Linh hồn của một bản vẽ kỹ thuật chuẩn mực

Khi nhìn vào một bản vẽ xây dựng hoặc cơ khí cầm trên tay:
- Nét thấy, nét cắt cột bê tông phải **đậm và rõ** (ví dụ dày 0.50mm) để người đọc nhìn thấy ngay khung kết cấu chính.
- Nét tường xây, nét cửa ở mức **vừa phải** (ví dụ dày 0.25mm - 0.35mm).
- Nét tim trục, nét kích thước, nét hoa văn gạch sàn phải **mảnh và thanh thoát** (ví dụ dày 0.13mm - 0.18mm) để không lấn át đối tượng chính.

Nếu một bản vẽ in ra mà tất cả các nét đều dày bằng nhau như một mớ dây thép, bản vẽ đó sẽ bị đánh giá là nghiệp dư và rất khó thi công.

Trong AutoCAD, màu sắc trên màn hình làm việc (Đỏ, Vàng, Xanh lá, Xanh lơ...) chỉ để giúp người vẽ dễ phân biệt đối tượng. Khi in ra giấy hoặc xuất file PDF, toàn bộ màu sắc này sẽ được quy đổi sang màu đen và độ dày nét in thông qua **Bảng phong cách in ([[Plot Style]] - Đuôi file `.ctb`)**.

![Nguyên lý quy đổi nét in CTB](media/ac-07-04-ctb-plot-styles.svg)

```hotspots
image: media/ac-07-04-ctb-plot-styles.svg
alt: Sơ đồ nguyên lý quy đổi màu sắc sang độ dày nét in của bảng CTB
layout: central
points:
  - id: spot-1
    x: 23
    y: 35
    title: Màu sắc trên màn hình CAD
    text: "Màu Color 1 (Red), Color 2 (Yellow)... dùng để phân biệt trực quan khi thiết kế."
  - id: spot-2
    x: 50
    y: 45
    title: Bảng quy đổi CTB
    text: "Bộ lọc trung gian: Chỉ định màu màn hình khi in ra sẽ mang màu gì và nét dày bao nhiêu mm."
  - id: spot-3
    x: 77
    y: 35
    title: Bản in thật ra giấy / PDF
    text: "Toàn bộ chuyển thành màu đen sắc nét với các cấp độ dày nét phân cấp rõ ràng."
  - id: spot-4
    x: 77
    y: 75
    title: Nét cắt cột / dầm (0.50mm)
    text: "Nét đậm nhất thể hiện mặt cắt chịu lực chính của công trình."
```

## Bảng quy chuẩn nét in kinh điển (TCVN)

Dưới đây là bảng phân bổ nét in chuẩn màu `Index Color` (Color 1 đến Color 7) được hơn 90% các công ty tư vấn thiết kế tại Việt Nam sử dụng:

| Màu màn hình | Tên màu | Độ dày nét in (Lineweight) | Đối tượng tương ứng |
|---|---|---|---|
| **Color 1** | Red (Đỏ) | **0.13 mm** (Rất mảnh) | Tim trục, nét đứt, ký hiệu cao độ |
| **Color 8 / 9** | Gray (Xám) | **0.09 - 0.13 mm** (Mảnh) | Hoa văn gạch Hatch, nền chỉ dẫn |
| **Color 2** | Yellow (Vàng) | **0.18 mm** (Mảnh) | Đường kích thước (Dimension), chữ ghi chú |
| **Color 3** | Green (Xanh lá) | **0.25 mm** (Vừa) | Nét thấy thiết bị, nội thất, cửa đi |
| **Color 4** | Cyan (Xanh lơ) | **0.35 mm** (Khá đậm) | Nét bao tường xây, dầm phụ |
| **Color 7** | White/Black (Trắng) | **0.40 mm** (Đậm) | Khung tên bản vẽ, tiêu đề chính |
| **Color 5 / 6** | Blue / Magenta | **0.50 mm** (Rất đậm) | Mặt cắt cột, dầm chịu lực chính |

## Cách dùng từng bước: Tạo bảng nét in riêng cho bạn

### 1. Mở trình biên tập Plot Style Table Editor
1. Gõ `PLOT` (hoặc mở `PAGESETUP`), tại ô **Plot style table** ở góc trên bên phải.
2. Chọn dòng `monochrome.ctb` (in đen trắng mặc định) hoặc chọn `New...` để tạo bảng mới.
3. Bấm vào biểu tượng **Chiếc bút chì vẽ** (Edit) ngay bên cạnh tên bảng.

### 2. Thiết lập quy chuẩn màu đen và gán độ dày nét
1. Hộp thoại **Plot Style Table Editor** xuất hiện. Chuyển sang thẻ **Form View**.
2. Cột bên trái *Plot styles* liệt kê toàn bộ 255 màu từ `Color 1` đến `Color 255`.
3. Bấm chọn `Color 1`, giữ phím [Shift] và bấm chọn đến `Color 255` (chọn toàn bộ 255 màu).
4. Tại cột bên phải mục **Properties**:
   - Dòng **Color:** Chọn màu **Black** (Tất cả các màu trên màn hình khi in ra đều thành mực đen sắc nét).
5. Giờ ta phân cấp độ dày:
   - Bấm chọn riêng `Color 1`: Tại dòng **Lineweight**, chọn `0.13 mm`.
   - Bấm chọn `Color 2`: Dòng **Lineweight**, chọn `0.18 mm`.
   - Bấm chọn `Color 3`: Dòng **Lineweight**, chọn `0.25 mm`.
   - Bấm chọn `Color 4`: Dòng **Lineweight**, chọn `0.35 mm`.
   - Bấm chọn `Color 5`: Dòng **Lineweight**, chọn `0.50 mm`.
   - Bấm chọn `Color 7`: Dòng **Lineweight**, chọn `0.35 mm`.
   - Bấm chọn `Color 8` và `Color 9`: Dòng **Lineweight**, chọn `0.09 mm`.
6. Bấm nút **Save As...**, đặt tên file là `CTB-CONG-TY.ctb`.
7. Bấm **Save & Close** để hoàn tất.

### 3. Sao lưu và chia sẻ file nét in với lệnh STYLESMANAGER
Để gửi file `.ctb` này cho đồng nghiệp hoặc copy sang máy tính khác:
1. Gõ lệnh `STYLESMANAGER` rồi nhấn [Enter].
2. Một cửa sổ thư mục Windows Explorer sẽ mở ra ngay lập tức tại vị trí:
   `...\AppData\Roaming\Autodesk\AutoCAD ...\Plotters\Plot Styles`.
3. Bạn chỉ việc copy file `CTB-CONG-TY.ctb` gửi cho bạn bè, hoặc dán file nét in của đối tác vào thư mục này để AutoCAD nhận diện ngay!

## Phân biệt CTB và STB

- **CTB (Color-dependent Plot Style):** Phổ biến nhất. Độ đậm nhạt nét in phụ thuộc vào màu sắc của nét vẽ trên màn hình. Rất trực quan và dễ quản lý.
- **STB (Named Plot Style):** Nét in được đặt tên (ví dụ: Style 1, Style 2) và gán thủ công vào từng layer bất kể layer đó màu gì. Ít phổ biến hơn ở Việt Nam.

> [!TIP]
> Nếu bạn muốn giữ lại một số nét có màu sắc thực (ví dụ logo công ty in màu đỏ, hoặc đường ống nước in màu xanh dương), trong bảng CTB chỉ cần chọn màu tương ứng đó và đổi dòng **Color** thành `Use object color` thay vì `Black`!

## Tự kiểm tra

```quiz
id: q-ac-07-04-1
type: single
question: "Đuôi tệp tin cấu hình phong cách nét in theo màu (Color-dependent Plot Style) trong AutoCAD có định dạng là gì?"
options:
  - text: ".ctb"
    correct: true
    why: "CTB viết tắt của Color Table / Color-dependent Plot Style Table."
  - text: ".stb"
    why: "STB là định dạng Named Plot Style theo tên kiểu."
  - text: ".dwg"
    why: "DWG là định dạng tệp bản vẽ đồ họa chính."
  - text: ".dwt"
    why: "DWT là định dạng tệp mẫu Drawing Template."
explain: "Tệp đuôi .ctb là định dạng chuẩn mực quản lý toàn bộ hệ thống nét in theo màu sắc của các công ty thiết kế."
tags: [chang-07, plot-style]
```

```quiz
id: q-ac-07-04-2
type: single
question: "Lệnh nào trong AutoCAD mở ngay cửa sổ thư mục Windows chứa toàn bộ các tệp nét in .ctb và .stb của máy tính?"
options:
  - text: "STYLESMANAGER"
    correct: true
    why: "STYLESMANAGER mở trực tiếp đường dẫn thư mục Plot Styles trong ổ đĩa hệ thống."
  - text: "PLOTTERMANAGER"
    why: "PLOTTERMANAGER mở thư mục chứa các file driver máy in .pc3."
  - text: "LAYER"
    why: "LAYER mở trình quản lý lớp vẽ trong bản vẽ."
  - text: "EXPLORER"
    why: "EXPLORER không phải lệnh nội bộ chuẩn của AutoCAD."
explain: "Dùng STYLESMANAGER là cách nhanh nhất để chép thêm file nét in của đối tác vào máy hoặc sao lưu file CTB của mình."
tags: [chang-07, stylesmanager]
```

```quiz
id: q-ac-07-04-3
type: truefalse
question: "Trong bảng thiết lập CTB, bạn có thể chọn một màu cụ thể giữ nguyên 'Use object color' để in màu thực (như logo công ty) trong khi các nét khác vẫn in màu đen."
answer: true
explain: "AutoCAD cho phép cấu hình linh hoạt từng màu riêng biệt trong 255 màu, vừa đảm bảo bản vẽ in đen trắng vừa giữ lại màu nhận diện thương hiệu."
tags: [chang-07, ctb]
```

## Lỗi thường gặp

- **Bản vẽ in ra bị mờ căm hoặc có màu vàng chanh khó đọc:** Do chọn bảng nét in là `None` hoặc `acad.ctb`. Lúc này nét vàng trên màn hình sẽ in ra mực màu vàng lên giấy trắng, khiến mắt thường gần như không đọc được. Khắc phục: Đổi sang `monochrome.ctb` hoặc bảng CTB chuẩn đã quy định `Color = Black`.
- **Mở file người khác gửi không thấy bảng CTB của họ:** Do thiếu file `.ctb` đi kèm. Khắc phục: Yêu cầu đối tác gửi file `.ctb`, sau đó gõ `STYLESMANAGER` và dán file vào thư mục mở ra.

## Bài tập thực hành

- [ ] Gõ lệnh `STYLESMANAGER` để mở thư mục lưu trữ các file nét in trên máy tính. <!-- expect: STYLESMANAGER -->
- [ ] Quan sát sự có mặt của các file tiêu chuẩn như `monochrome.ctb` và `acad.ctb`.
- [ ] Gõ lệnh `PLOT` để mở hộp thoại Plot, bấm vào biểu tượng chỉnh sửa bảng nét in `monochrome.ctb`. <!-- expect: PLOT -->
- [ ] Quan sát thiết lập cột `Color` (đều gán thành Black) và bấm Cancel để đóng hộp thoại an toàn.

## Nguồn tham khảo

```links
- title: "Quản lý Plot Style Tables (CTB/STB) từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Plot+Style+Tables"
  kind: official
- title: "Lệnh STYLESMANAGER mở thư mục nét in từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=STYLESMANAGER"
  kind: official
```
