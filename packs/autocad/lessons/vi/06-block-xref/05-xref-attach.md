---
id: ac-06-05
title: Làm việc nhóm và tham chiếu ngoài với External References (XREF)
category: Khối và Tham chiếu
tags: [xref, attach, imageattach, pdfattach, lam-viec-nhom]
level: intermediate
minutes: 25
needs: [ac-06-01]
appVersions: ['2024', '2025']
edition: all
---
# Làm việc nhóm và tham chiếu ngoài với External References (XREF)

> **Mục tiêu:**
> - Sử dụng bảng quản lý `XREF` để tham chiếu tệp bản vẽ DWG, hình ảnh raster và tệp PDF vào dự án.
> - Phân biệt bản chất giữa kiểu tham chiếu `Attach` và `Overlay` để tránh xung đột vòng lặp.
> - Thiết lập loại đường dẫn tương đối (`Relative Path`) để đảm bảo không bị thất lạc liên kết khi chia sẻ tệp.

## Khái niệm XREF và sức mạnh làm việc nhóm

Hãy hình dung một dự án thiết kế khách sạn quy mô lớn:
- Bộ phận Kiến trúc đang triển khai bố trí phòng ốc mặt bằng.
- Bộ phận Kết cấu đang vẽ dầm, cột, sàn.
- Bộ phận Cơ điện (MEP) đang thiết kế hệ thống ống thông gió, dây điện và cấp thoát nước.

Nếu cả 3 nhóm copy-paste toàn bộ hình vẽ vào chung một file duy nhất, tệp CAD sẽ nặng hàng trăm Megabyte, giật lag không thể mở nổi. Hơn nữa, mỗi lần kiến trúc dời một bức tường, kết cấu và điện nước sẽ không hề hay biết!

**[[Xref]] (External Reference - Tham chiếu ngoài)** là giải pháp tiêu chuẩn quốc tế:
Thay vì nhúng hẳn hình vẽ vào file như Block, XREF chỉ tạo một **đường dẫn liên kết ảo**. Bản vẽ của bạn chỉ "chiếu" tệp mặt bằng kiến trúc lên màn hình làm nền. Khi kỹ sư kiến trúc sửa tường và bấm lưu (Save), góc màn hình của bạn sẽ hiện thông báo: *"A reference file has changed"* kèm nút bấm **Reload** để tự động cập nhật ngay lập tức!

![Bảng điều khiển External References Palette và so sánh Attach vs Overlay](media/ac-06-05-xref-palette.svg)

```hotspots
image: media/ac-06-05-xref-palette.svg
alt: Bảng điều khiển tham chiếu ngoài External References (XR)
layout: central
points:
  - id: spot-1
    x: 26
    y: 28
    title: Tệp hiện hành (Current Drawing)
    text: Bản vẽ chính đang mở và thực hiện thiết kế trực tiếp.
  - id: spot-2
    x: 26
    y: 45
    title: Tệp DWG tham chiếu (Loaded)
    text: File lưới trục kết cấu được liên kết làm nền mờ, trạng thái đã nạp thành công.
  - id: spot-3
    x: 26
    y: 68
    title: Cảnh báo mất file (Not Found)
    text: Biểu tượng chấm than đỏ khi file nguồn bị xóa hoặc đổi tên ngoài ổ cứng.
  - id: spot-4
    x: 74
    y: 40
    title: Kiểu Attach
    text: Tham chiếu lồng nhau (Nested) - tự động kéo theo file con khi người khác xref bản vẽ của bạn.
  - id: spot-5
    x: 74
    y: 70
    title: Kiểu Overlay (Khuyên dùng)
    text: Chỉ hiển thị ở bản vẽ hiện hành, không bị truyền tiếp sang bản vẽ của người khác.
```

## Cách dùng từng bước

### 1. Mở bảng quản lý XREF và đính kèm bản vẽ DWG
1. Gõ lệnh `XR` hoặc `XREF` rồi nhấn [Enter]. Bảng **External References** mở ra.
2. Bấm vào biểu tượng tệp DWG có dấu mũi tên ở góc trên bên trái bảng (hoặc nhấp chuột phải chọn **Attach DWG...**).
3. Duyệt tìm tệp DWG cần tham chiếu (ví dụ: `LUOI-TRUC.dwg`), bấm **Open**.
4. Hộp thoại **Attach External Reference** xuất hiện:
   - **Reference Type:** Chọn **Overlay** (Nguyên tắc vàng: Luôn chọn Overlay trừ khi có lý do đặc biệt).
   - **Path Type:** Chọn **Relative path** (Đường dẫn tương đối).
   - **Insertion Point:** Bỏ tick ô *Specify On-screen* và giữ toạ độ là `0,0,0` để hai bản vẽ ăn khớp toạ độ tuyệt đối với nhau.
   - **Scale:** Giữ nguyên tỉ lệ `1.0`.
5. Bấm **OK**. Bản vẽ lưới trục sẽ xuất hiện ngay ngắn làm nền trên màn hình của bạn!

### 2. Đính kèm ảnh hoặc tệp PDF
- Dùng lệnh `IMAGEATTACH` để chèn ảnh khảo sát hiện trạng vệ tinh Google Earth hoặc ảnh chụp scan bản vẽ tay cũ dạng `.png` / `.jpg`.
- Dùng lệnh `PDFATTACH` để chèn tài liệu bản vẽ PDF của đối tác làm nền đồ lại nét.

## Phân biệt Attach vs Overlay và quy tắc đường dẫn

### 1. Attach vs Overlay
- **Attach (Đính kèm truyền tiếp):** Nếu File A attach File B, và File C lại attach File A $\to$ File C sẽ nhìn thấy cả File B. Rất dễ gây hiện tượng "vòng lặp luẩn quẩn" (Circular reference) làm treo máy.
- **Overlay (Chồng lớp đơn lập):** File A overlay File B. Khi File C tham chiếu File A $\to$ File C chỉ thấy nội dung của A, hoàn toàn không thấy B. Tuyệt đối an toàn cho các dự án lớn!

### 2. Relative Path vs Absolute Path
- **Absolute Path (Đường dẫn tuyệt đối - C:\Users\KTS\Duan\Truc.dwg):** Nếu mang tệp sang máy tính khác hoặc gửi qua Zalo/Email, ổ đĩa C của máy người nhận không có đúng cấu trúc thư mục đó $\to$ XREF bị lỗi `Not Found` đỏ lòm!
- **Relative Path (Đường dẫn tương đối - .\Truc.dwg):** Tệp chỉ cần nằm cùng thư mục hoặc trong thư mục con tương đối. Dù bạn copy cả thư mục dự án đi đâu (sang USB, máy khác, nén ZIP), liên kết vẫn nhận diện trơn tru 100%!

> [!TIP]
> Muốn làm mờ tệp XREF để tập trung vẽ nét của mình, dùng biến hệ thống `XDWGFADECTL`. Đặt giá trị bằng `50` (mờ 50%) để tệp tham chiếu chuyển sang màu xám dịu mắt, tránh lẫn lộn với nét vẽ mới.

> [!TIP]
> Khi cần gửi trọn gói toàn bộ bản vẽ và tất cả các tệp XREF, font chữ đính kèm cho đối tác, hãy dùng lệnh `ETRANSMIT`. AutoCAD sẽ tự động gom tất cả thành một file nén `.zip` hoàn hảo!

## Tự kiểm tra

```quiz
id: q-ac-06-05-1
type: single
question: "Tại sao kiểu tham chiếu Overlay được khuyên dùng ưu tiên hơn Attach trong hầu hết các dự án làm việc nhóm?"
options:
  - text: "Overlay chỉ hiển thị ở bản vẽ hiện tại, ngăn ngừa lỗi vòng lặp tham chiếu và tránh làm phình to bản vẽ"
    correct: true
    why: "Overlay không kéo theo các tệp lồng nhau sang bản vẽ của người khác, giúp cấu trúc file trong sạch."
  - text: "Overlay tự động dịch bản vẽ sang tiếng Anh"
    correct: false
    why: "Overlay không có tính năng dịch ngôn ngữ."
  - text: "Overlay làm cho file nhẹ đi đúng 10 lần"
    correct: false
    why: "Cả hai kiểu đều nhẹ như nhau vì chỉ lưu đường dẫn liên kết."
  - text: "Overlay ngăn không cho người khác xóa bản vẽ"
    correct: false
    why: "Overlay không liên quan đến quyền truy cập bảo mật file."
explain: "Kiểu Overlay tránh triệt để tình trạng Circular Reference (File A gọi File B, File B lại gọi File A) gây treo đơ phần mềm."
```

```quiz
id: q-ac-06-05-2
type: single
question: "Kiểu đường dẫn nào giúp bạn copy toàn bộ thư mục dự án sang máy tính khác mà XREF không bao giờ bị mất liên kết (Not Found)?"
options:
  - text: "Relative Path (Đường dẫn tương đối)"
    correct: true
    why: "Relative Path chỉ lưu vị trí tương quan giữa các file trong cùng cấu trúc thư mục dự án."
  - text: "Absolute Path (Đường dẫn tuyệt đối)"
    correct: false
    why: "Absolute Path gắn cứng tên ổ đĩa C:, D: nên sang máy khác sẽ rất dễ bị mất đường dẫn."
  - text: "No Path"
    correct: false
    why: "No Path đòi hỏi file phải luôn nằm cùng thư mục hoặc trong đường dẫn tìm kiếm hệ thống."
  - text: "Hyperlink Path"
    correct: false
    why: "Hyperlink dùng cho đường link web, không dùng cho XREF bản vẽ."
explain: "Luôn chọn Relative Path khi làm việc nhóm để linh hoạt trao đổi thư mục dự án qua mạng nội bộ hoặc ổ cứng di động."
```

```quiz
id: q-ac-06-05-3
type: truefalse
question: "Khi tệp DWG gốc được sửa và lưu lại, bản vẽ của bạn sẽ tự động hiện thông báo yêu cầu Reload để cập nhật nét vẽ mới nhất của đồng đội."
answer: false
explain: "Tính năng cập nhật tức thì của XREF giúp các bộ môn Kiến trúc, Kết cấu, MEP luôn luôn phối hợp ăn khớp theo thời gian thực."
```

## Lỗi thường gặp

- **Trạng thái XREF báo Not Found (chấm than đỏ):** Do file gốc bị xóa, đổi tên hoặc chuyển thư mục. Khắc phục: Chọn tệp bị lỗi trong bảng External References, nhìn xuống ô `Saved Path` ở dưới cùng và bấm nút `[...]` để chỉ lại đường dẫn mới.
- **Không chọn hoặc sửa được nét vẽ của tệp XREF:** Đây là tính năng bảo vệ an toàn của XREF chứ không phải lỗi! XREF là một khối chiếu bảo vệ nguyên vẹn thiết kế của người khác. Nếu thật sự muốn sửa, nhấp chuột phải chọn **Open** để mở file gốc hoặc dùng **Edit Xref In-Place** (`REFEDIT`).

## Bài tập thực hành

- [ ] Gõ `XREF` (hoặc `XR`) để mở bảng điều khiển External References. <!-- expect: XREF -->
- [ ] Quan sát tệp hiện tại đang hiển thị với trạng thái `Current`.
- [ ] Gõ lệnh `IMAGEATTACH` để mở hộp thoại duyệt tệp ảnh raster. <!-- expect: IMAGEATTACH -->
- [ ] Gõ lệnh `PDFATTACH` để mở hộp thoại duyệt tệp tài liệu PDF. <!-- expect: PDFATTACH -->
- [ ] Đóng bảng điều khiển XREF.

## Nguồn tham khảo

```links
- title: "Quản lý External References từ Autodesk Knowledge Network"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=XREF"
  kind: official
- title: "Chèn ảnh Raster bằng IMAGEATTACH từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=IMAGEATTACH"
  kind: official
```
