---
id: ac-07-02
title: Cấu hình trang in chuyên nghiệp với Page Setup (PAGESETUP)
category: Layout và In ấn
tags: [pagesetup, layout, kho-giay, pdf, in-an]
level: intermediate
minutes: 20
needs: [ac-07-01]
appVersions: ['2024', '2025']
edition: all
---
# Cấu hình trang in chuyên nghiệp với Page Setup (PAGESETUP)

> **Mục tiêu:**
> - Sử dụng lệnh `PAGESETUP` để cấu hình khổ giấy, máy in ảo và bảng nét in cho từng trang Layout.
> - Phân biệt khổ giấy ISO tiêu chuẩn và khổ giấy ISO Full Bleed để không bị xén lề trắng.
> - Thiết lập tỉ lệ in cố định 1:1 trong không gian giấy để đảm bảo độ chính xác tuyệt đối của bản vẽ.

## Vai trò của Page Setup trong không gian Layout

Khi bạn mới bấm vào tab Layout, AutoCAD thường mặc định gán cho nó khổ giấy bé tí A4 hoặc Letter của Mỹ. Nếu bạn cứ thế vẽ khung tên A3 vào, khung tên sẽ bị tràn ra khỏi trang giấy trắng rất lộn xộn.

Mỗi tab Layout cần phải được "định hình" kích thước rõ ràng:
- Tờ này in ra máy in nào (máy in giấy văn phòng, máy in khổ lớn A0 hay xuất file PDF)?
- Khổ giấy là A4, A3, A2 hay A1?
- Chiều giấy in nằm ngang (Landscape) hay đứng (Portrait)?

Lệnh **`PAGESETUP`** là trung tâm cấu hình toàn bộ các thông số này. Khi bạn cài đặt Page Setup chuẩn một lần duy nhất, mỗi lần sau bạn chỉ việc bấm `Ctrl + P` rồi nhấn [Enter] là bản vẽ in ra lập tức, không bao giờ phải ngồi chọn lại máy in hay căn chỉnh lề thủ công!

![Hộp thoại thiết lập Page Setup](media/ac-07-02-pagesetup.svg)

```hotspots
image: media/ac-07-02-pagesetup.svg
alt: Hộp thoại thiết lập Page Setup cho không gian Layout
layout: central
points:
  - id: spot-1
    x: 23
    y: 30
    title: Máy in / Xuất file (Printer)
    text: "Chọn AutoCAD PDF hoặc DWG To PDF.pc3 để xuất file PDF vector sắc nét."
  - id: spot-2
    x: 68
    y: 30
    title: Khổ giấy in (Paper size)
    text: "Chọn ISO full bleed A3 (420x297 mm) để tận dụng tối đa diện tích in sát mép giấy."
  - id: spot-3
    x: 23
    y: 65
    title: Tỉ lệ in giấy (Plot scale)
    text: "Luôn đặt 1:1 (1 mm = 1 unit). Tuyệt đối không tick chọn Fit to paper."
  - id: spot-4
    x: 68
    y: 65
    title: Bảng nét in (Plot style)
    text: "Chọn monochrome.ctb để toàn bộ nét vẽ in ra màu đen theo đúng độ đậm Lineweight."
```

## Cách dùng từng bước

### 1. Mở Page Setup Manager
1. Chuyển sang tab `Layout` cần cấu hình.
2. Gõ `PAGESETUP` rồi nhấn [Enter] (hoặc nhấp chuột phải vào tên tab Layout ở góc dưới > chọn **Page Setup Manager...**).
3. Hộp thoại hiện ra: Tên trang hiện tại đang được bôi sáng. Bấm nút **Modify...** bên phải.

### 2. Thiết lập 4 thông số cốt lõi
1. **Printer/Plotter (Máy in):**
   - Tại ô *Name*, chọn máy in ảo **`AutoCAD PDF (General Documentation).pc3`** (hoặc `DWG To PDF.pc3`). Đây là driver xuất file PDF tích hợp sẵn tốt nhất của AutoCAD, tạo ra file PDF nhẹ, hỗ trợ tìm kiếm chữ tiếng Việt và bật/tắt được layer khi xem bằng Foxit Reader hoặc Adobe Acrobat.
2. **Paper Size (Khổ giấy):**
   - Xổ danh sách và tìm đến dòng **`ISO full bleed A3 (420.00 x 297.00 mm)`** (nếu giấy ngang) hoặc `297.00 x 420.00 mm` (nếu giấy đứng).
   - *Khuyên dùng Full Bleed:* Khổ ISO thường sẽ trừ lề trắng mép giấy 5mm khiến khung tên bị xén mất viền ngoài. Dòng `Full Bleed` có lề in bằng 0, cho phép in tràn viền hoàn hảo.
3. **Plot Area & Plot Scale (Vùng in và tỉ lệ in):**
   - *What to plot:* Chọn **Layout** (In toàn bộ bề mặt tờ giấy).
   - *Plot scale:* Chọn **1:1** và đơn vị là **mm** (`1 mm = 1 unit`).
   - *CẢNH BÁO:* Không bao giờ đánh dấu tick vào ô **Fit to paper**! Nếu tick ô này, bản vẽ sẽ bị co lại một tỉ lệ lẻ (ví dụ 1:103.2), khi thợ dùng thước đo trên giấy in sẽ bị sai hoàn toàn!
4. **Plot style table (Bảng nét in):**
   - Chọn **`monochrome.ctb`** (in đen trắng cơ bản) hoặc bảng nét in riêng của công ty bạn (sẽ học chi tiết ở bài 4).
5. Bấm **OK**, sau đó bấm **Close**. Tờ giấy trắng trên màn hình sẽ lập tức co giãn thành đúng kích thước A3 420x297 mm chuẩn xác!

## Tuỳ chọn và mẹo tái sử dụng Page Setup

> [!TIP]
> Thay vì cài đặt từng Layout một cách thủ công, bạn có thể tạo một Page Setup chuẩn đặt tên là `IN-A3-PDF`. Sau đó ở các trang Layout khác, bạn chỉ việc bấm nút **Set Current** để gán nguyên thiết lập này trong 1 tích tắc.

> [!TIP]
> Đánh dấu tick vào ô **Display plot styles** trong Page Setup nếu bạn muốn màn hình Layout hiển thị trước độ đậm nhạt của nét in đen trắng giống hệt như khi in ra giấy thật!

## Tự kiểm tra

```quiz
id: q-ac-07-02-1
type: single
question: "Tại sao trong mục Paper Size của Page Setup, khổ giấy 'ISO Full Bleed' lại được các kỹ sư ưu tiên lựa chọn hơn khổ ISO thông thường?"
options:
  - text: "Full Bleed cho phép in tràn viền lề bằng 0, không làm xén mất đường bao khung tên bản vẽ"
    correct: true
    why: "Khổ giấy Full Bleed mở rộng vùng in tối đa tới tận mép giấy thực tế."
  - text: "Full Bleed in nhanh hơn gấp 10 lần"
    correct: false
    why: "Tốc độ in phụ thuộc vào dung lượng đồ họa của tệp tin."
  - text: "Full Bleed tự động dịch chữ sang tiếng Anh"
    correct: false
    why: "Khổ giấy không can thiệp vào ngôn ngữ văn bản."
  - text: "Full Bleed chỉ hỗ trợ giấy A4, không hỗ trợ A3"
    correct: false
    why: "Full Bleed có đầy đủ từ A4, A3, A2, A1 đến A0."
explain: "Khổ giấy Full Bleed giúp người vẽ dễ dàng căn khung tên sát mép giấy kỹ thuật mà không lo bị viền trắng máy in cắt mất nét góc."
```

```quiz
id: q-ac-07-02-2
type: single
question: "Khi cài đặt Plot Scale cho không gian Layout trong Page Setup, thiết lập nào sau đây là BẮT BUỘC?"
options:
  - text: "Scale 1:1 (1 mm = 1 unit) và tuyệt đối không tick vào ô Fit to paper"
    correct: true
    why: "Layout là không gian tờ giấy in thật, do đó tỉ lệ in trang giấy ra ngoài đời luôn luôn là 1:1."
  - text: "Tick vào ô Fit to paper để máy tự kéo dãn hình cho đầy giấy"
    correct: false
    why: "Fit to paper làm sai lệch tỉ lệ xích chuẩn của bản vẽ."
  - text: "Scale 1:100"
    correct: false
    why: "Tỉ lệ 1:100 là tỉ lệ của khung nhìn Viewport, không phải tỉ lệ in của cả trang giấy Layout."
  - text: "Scale theo đơn vị Inch"
    correct: false
    why: "Việt Nam sử dụng hệ mét tiêu chuẩn ISO mm."
explain: "Tờ giấy A3 in ra giấy A3 ngoài đời là tỉ lệ 1:1. Tỉ lệ thu nhỏ của công trình (1:50, 1:100...) được quản lý bên trong Viewport."
```

```quiz
id: q-ac-07-02-3
type: truefalse
question: "Lựa chọn máy in ảo AutoCAD PDF (hoặc DWG to PDF.pc3) giúp tạo ra các tệp PDF vector sắc nét và có thể tắt mở layer khi xem tài liệu."
answer: true
explain: "Driver in PDF tích hợp của AutoCAD tạo ra file định dạng vector độ phân giải cao, hỗ trợ giữ nguyên cấu trúc layer và font chữ Unicode tiếng Việt."
```

## Lỗi thường gặp

- **Khung tên bị lệch một bên, mất một góc viền:** Do chọn khổ giấy ISO thông thường có lề in lớn, hoặc không chọn vùng in là `Layout`. Khắc phục: Đổi sang khổ `ISO Full Bleed` và chỉnh *Plot offset* về `X = 0`, `Y = 0`.
- **Bản vẽ in ra bị sai tỉ lệ thước kẻ:** Do vô tình tick vào ô *Fit to paper* trong lúc in. Luôn kiểm tra chắc chắn ô này không được đánh dấu.

## Bài tập thực hành

- [ ] Chuyển sang tab `Layout1`, gõ lệnh `PAGESETUP` để mở trình quản lý trang in. <!-- expect: PAGESETUP -->
- [ ] Bấm nút **Modify**, chọn máy in là `DWG To PDF.pc3` (hoặc `AutoCAD PDF`). <!-- expect: PAGESETUP -->
- [ ] Chọn khổ giấy `ISO full bleed A3 (420.00 x 297.00 mm)`.
- [ ] Kiểm tra Plot scale là `1:1`, bảng nét in là `monochrome.ctb`. Bấm OK và Close. <!-- expect: PAGESETUP -->
- [ ] Dùng lệnh `RECTANG` vẽ một khung chữ nhật đúng kích thước 420 x 297 mm trên trang giấy vừa tạo để kiểm tra độ khớp viền. <!-- expect: RECTANG -->

## Nguồn tham khảo

```links
- title: "Quản lý thiết lập trang in Page Setup từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=PAGESETUP"
  kind: official
```
