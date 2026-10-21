---
id: ac-07-01
title: Phân biệt không gian vẽ Model Space và không gian in Layout
category: Layout và In ấn
tags: [model, layout, paper-space, in-an, co-ban]
level: intermediate
minutes: 20
needs: [ac-06-08]
appVersions: ['2024', '2025']
edition: all
---
# Phân biệt không gian vẽ Model Space và không gian in Layout

> **Mục tiêu:**
> - Phân biệt bản chất và mục đích sử dụng giữa không gian [[Model]] và không gian [[Layout]].
> - Làm chủ quy tắc vàng vẽ đúng tỉ lệ 1:1 trong Model và bố cục trang giấy in trong Layout.
> - Điều hướng, tạo mới và quản lý các tab Layout trong tệp bản vẽ kỹ thuật.

## Hai thế giới song song trong một tệp AutoCAD

Khi mới học vẽ AutoCAD, rất nhiều người mắc sai lầm vẽ khung tên A3 trực tiếp trong màn hình đen Model rồi dùng lệnh `SCALE` phóng to khung tên lên 50 hay 100 lần để bao quanh ngôi nhà. Cách làm thủ công này khiến bản vẽ bị rối loạn tỉ lệ, chữ số kích thước không đồng bộ và cực kỳ khó khăn khi chuyển giao cho đối tác.

Các kỹ sư quốc tế luôn phân tách đồ họa thành hai không gian chuyên biệt:
1. **Model Space (Không gian mô hình):** Nằm ở tab `Model` góc dưới bên trái màn hình. Đây là một vũ trụ vô hạn không có giới hạn biên giới. Bạn luôn luôn **vẽ với tỉ lệ thật 1:1** theo đơn vị thực tế (ví dụ: bức tường dài 15 mét thì gõ đúng `15000` mm, dầm dài 6 mét gõ đúng `6000` mm).
2. **Layout / Paper Space (Không gian giấy in):** Nằm ở các tab bên cạnh như `Layout1`, `Layout2`. Đây là một tờ giấy in thật ngoài đời (khổ A4, A3, A1, A0). Trên tờ giấy trắng này, bạn đặt khung tên chuẩn, chèn bảng danh mục bản vẽ, và mở các "khung cửa sổ" ([[Viewport]]) nhìn vào không gian Model với bất kỳ tỉ lệ thu phóng nào (1:100, 1:50, 1:20...).

![So sánh Model Space và Layout](media/ac-07-01-model-vs-layout.svg)

```hotspots
image: media/ac-07-01-model-vs-layout.svg
alt: So sánh không gian mô hình Model Space và không gian giấy Layout
layout: central
points:
  - id: spot-1
    x: 25
    y: 35
    title: Model Space (Vẽ 1:1)
    text: "Không gian mô hình vô tận màu tối, mọi vật thể được dựng theo đúng kích thước thực tế."
  - id: spot-2
    x: 25
    y: 75
    title: Tỉ lệ thực 1:1
    text: "Không bao giờ dùng lệnh SCALE để phóng to thu nhỏ công trình trong Model."
  - id: spot-3
    x: 75
    y: 35
    title: Layout Space (Trang giấy in)
    text: "Tờ giấy in màu trắng đại diện cho khổ giấy A4, A3 hoặc A1 thực tế ngoài đời."
  - id: spot-4
    x: 75
    y: 70
    title: Khung nhìn Viewport
    text: "Mở ô cửa sổ Viewport trên Layout để trích xuất các hình chiếu với các tỉ lệ in khác nhau."
```

## Cách dùng từng bước

### 1. Chuyển đổi giữa Model và Layout
- Nhìn xuống góc dưới bên trái của khu vực vẽ: Bạn sẽ thấy thẻ `Model` và các thẻ `Layout1`, `Layout2`.
- Bấm chuột trái vào thẻ `Layout1`: Màn hình sẽ chuyển từ màu đen vô hạn sang một trang giấy trắng có đường nét đứt bao quanh.
- Đường viền nét đứt này thể hiện vùng in khả dụng (Printable area) của máy in, ngoài đường nét đứt thì máy in không in tới được.

### 2. Tạo thêm tab Layout mới
1. Nhấp chuột phải vào một tab Layout bất kỳ ở đáy màn hình.
2. Menu ngữ cảnh xuất hiện các thao tác quản lý:
   - **New Layout:** Tạo một trang layout trắng mới tinh.
   - **From Template...:** Tạo layout từ một file mẫu có sẵn khung tên công ty.
   - **Delete:** Xóa trang layout không dùng.
   - **Rename:** Đổi tên trang thành tiếng Việt (ví dụ: `KT-01-MAT-BANG`, `KC-02-COT`).
   - **Move or Copy...:** Sao chép nguyên vẹn trang layout sang vị trí mới để làm trang tiếp theo.

## Ưu điểm tuyệt đối khi trình bày trên Layout

- **Một mô hình $\to$ Nhiều bản vẽ:** Bạn chỉ cần vẽ mặt bằng nhà đúng 1 lần trong Model. Trên Layout, bạn có thể tạo 3 trang khác nhau: một trang in mặt bằng kiến trúc tổng thể tỉ lệ 1:100, một trang in chi tiết vệ sinh tỉ lệ 1:25, và một trang in chi tiết cầu thang tỉ lệ 1:20.
- **Khung tên và chữ luôn chuẩn 100%:** Dù chi tiết bên trong thu nhỏ 1:100 hay 1:20, khung tên A3 của bạn vẫn giữ nguyên kích thước 420 x 297 mm, và chiều cao chữ số ghi chú luôn chuẩn xác 2.5mm khi cầm trên tay.

> [!TIP]
> Bấm dấu cộng `[+]` ngay bên cạnh tab Layout cuối cùng để tạo nhanh một trang in mới chỉ trong 1 giây.

> [!TIP]
> Bạn có thể ẩn/hiện hoặc đổi màu layer của một chi tiết trong riêng khung nhìn Layout này mà không làm ảnh hưởng tới các khung nhìn khác (tính năng `VP Freeze` cực mạnh sẽ học ở bài sau).

## Tự kiểm tra

```quiz
id: q-ac-07-01-1
type: single
question: "Nguyên tắc vàng khi dựng hình trong không gian Model Space của AutoCAD là gì?"
options:
  - text: "Luôn luôn vẽ với tỉ lệ kích thước thật 1:1 theo đơn vị thực tế (ví dụ mm)"
    correct: true
    why: "Model là không gian thế giới thực vô hạn, mọi vật thể đều phải vẽ đúng 100% kích thước thật."
  - text: "Thu nhỏ đối tượng 100 lần ngay khi vẽ để vừa màn hình"
    correct: false
    why: "Thu nhỏ ngay khi vẽ sẽ phá hủy tính chính xác của các lệnh đo và xuất khối lượng."
  - text: "Vẽ khung tên thật to rồi thu nhỏ dần công trình lại"
    correct: false
    why: "Đây là cách vẽ cổ điển sai lầm làm hỏng hệ thống kích thước."
  - text: "Chỉ được vẽ đường thẳng, không được vẽ đường cong"
    correct: false
    why: "Model vẽ được mọi đối tượng hình học 2D và 3D."
explain: "Vẽ tỉ lệ 1:1 trong Model là tôn chỉ bất biến của AutoCAD. Mọi việc thu phóng tỉ lệ in ấn đều được giao cho không gian Layout xử lý."
```

```quiz
id: q-ac-07-01-2
type: single
question: "Màu nền mặc định của không gian Layout trong AutoCAD thể hiện điều gì?"
options:
  - text: "Màu trắng đại diện cho tờ giấy in thực tế ngoài đời"
    correct: true
    why: "Màu trắng giúp người vẽ hình dung trực quan bố cục trang giấy in A4, A3 hay A1."
  - text: "Báo hiệu bản vẽ đang bị nhiễm virus"
    correct: false
    why: "Màu trắng là thiết lập hiển thị tiêu chuẩn của AutoCAD cho Layout."
  - text: "Bản vẽ đã bị khóa vĩnh viễn không sửa được"
    correct: false
    why: "Layout hoàn toàn vẽ và chỉnh sửa bình thường."
  - text: "Máy tính sắp hết pin"
    correct: false
    why: "Không liên quan đến phần cứng máy tính."
explain: "Không gian Layout mô phỏng trực tiếp mặt phẳng tờ giấy in với đường biên mép giấy và đường nét đứt giới hạn đầu phun máy in."
```

```quiz
id: q-ac-07-01-3
type: truefalse
question: "Bạn có thể tạo nhiều tab Layout khác nhau trong cùng một tệp DWG để quản lý nhiều trang hồ sơ bản vẽ."
answer: true
explain: "AutoCAD cho phép tạo hàng chục tab Layout đại diện cho từng tờ bản vẽ trong một bộ hồ sơ thiết kế hoàn chỉnh."
```

## Lỗi thường gặp

- **Scale khung tên to lên để bọc lấy hình trong Model:** Thói quen xấu thời CAD đời cũ làm hỏng kích thước Annotative và mất khả năng in hàng loạt. Khắc phục: Chuyển toàn bộ khung tên sang Layout và dùng khung nhìn `MVIEW`.
- **Vẽ nhầm chi tiết công trình bên Layout:** Tưởng mình đang vẽ ở Model nên vẽ tường và cột trực tiếp trên mặt giấy Layout. Khắc phục: Cắt đối tượng ([Ctrl + X]), chuyển sang tab Model và dán lại ([Ctrl + V]).

## Bài tập thực hành

- [ ] Trong không gian `Model`, vẽ một hình chữ nhật kích thước 10000 x 6000 mm bằng lệnh `RECTANG`. <!-- expect: RECTANG -->
- [ ] Bấm vào tab `Layout1` ở góc dưới bên trái màn hình để chuyển sang không gian giấy in.
- [ ] Nhấp chuột phải vào tab `Layout1`, chọn `Rename` và đổi tên thành `BAN-VE-01`.
- [ ] Bấm dấu `[+]` ở đáy màn hình để tạo thêm một tab Layout mới.
- [ ] Bấm lại tab `Model` để quay về không gian mô hình ban đầu.

## Nguồn tham khảo

```links
- title: "Phân biệt Model Space và Paper Space từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Model+Space+and+Paper+Space"
  kind: official
```
