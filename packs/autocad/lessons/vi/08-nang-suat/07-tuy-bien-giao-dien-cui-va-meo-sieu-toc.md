---
id: ac-08-07
title: Tuỳ biến giao diện người dùng CUI và 10 mẹo vẽ siêu tốc
category: Nâng cao năng suất
tags: [cui, quick-access, giao-dien, meo-ve, phim-tat, chuyen-nghiep]
level: advanced
minutes: 25
needs: [ac-08-05, ac-08-06]
appVersions: ['2024', '2025']
edition: all
---
# Tuỳ biến giao diện người dùng CUI và 10 mẹo vẽ siêu tốc

> **Mục tiêu:**
> - Sử dụng hộp thoại `CUI` để tùy biến sâu dải Ribbon, thanh Quick Access Toolbar và các thao tác nhấp đúp chuột.
> - Làm chủ bảng tổng hợp phím chức năng F1 đến F12 kiểm soát chế độ vẽ chính xác.
> - Áp dụng 10 mẹo thực chiến của chuyên gia để tối ưu hóa không gian làm việc và nhân đôi tốc độ thiết kế.

## Hộp thoại CUI: Làm chủ toàn bộ giao diện phần mềm

Giao diện mặc định của AutoCAD được thiết kế để phù hợp cho mọi ngành nghề, từ cơ khí chế tạo máy đến kiến trúc xây dựng, trắc địa và điện tử. Do đó, có tới 70% các nút bấm trên thanh Ribbon bạn sẽ không bao giờ dùng tới, trong khi những công cụ bạn cần hàng ngày lại bị giấu sâu trong các menu con.

Lệnh **`CUI` (Customize User Interface)** là trung tâm điều khiển tối cao cho phép bạn tái cấu trúc lại toàn bộ giao diện:
- Tạo các thẻ Ribbon riêng chứa các nút bấm của công ty bạn.
- Thêm các lệnh hay dùng nhất lên thanh công cụ truy cập nhanh **Quick Access Toolbar (QAT)** ở đỉnh màn hình.
- Đổi hành vi nhấp đúp chuột (Double-click Actions) theo ý thích cá nhân.

## Cách dùng từng bước với lệnh CUI

1. Gõ `CUI` rồi nhấn [Enter] (hoặc vào menu *Manage* > chọn **User Interface**).
2. Cửa sổ **Customize User Interface** mở ra với cấu trúc cây thư mục bên trái:
   - **Quick Access Toolbars:** Bấm mở rộng `Quick Access Toolbar 1`. Bạn có thể kéo thả bất kỳ lệnh nào từ danh sách *Command List* bên dưới đặt lên thanh này để bấm một chạm.
   - **Ribbon:** Tạo các thẻ `Tabs` và cụm công cụ `Panels` mang tên riêng của bạn (ví dụ: thẻ `CHUYEN_NGANH_XAY_DUNG`).
   - **Double Click Actions:** Quy định khi nhấp đúp vào đối tượng thì mở lệnh gì (ví dụ: nhấp đúp vào Polyline tự động mở lệnh `PEDIT`, nhấp đúp vào Text mở `MTEXT`).
   - **Mouse Buttons:** Gán chức năng phụ khi kết hợp phím [Shift] + chuột phải.
3. Sau khi tùy biến xong, bấm **Apply** và **OK** để lưu lại không gian làm việc (Workspace) của bạn.

## Bảng tổng hợp phím chức năng F1 - F12 phải thuộc lòng

Các phím từ F1 đến F12 trên hàng phím đầu tiên của bàn phím là các công tắc bật/tắt nhanh các trợ thủ hình học:

| Phím | Tên chế độ | Chức năng cốt lõi |
|---|---|---|
| **F1** | Help | Mở tài liệu trợ giúp trực tuyến Autodesk |
| **F2** | Expanded History | Bật/tắt cửa sổ phóng to lịch sử dòng lệnh Command Line |
| **F3** | **Object Snap (Osnap)** | **Bật/tắt truy bắt điểm hình học** (Endpoint, Midpoint, Center...) |
| **F7** | Grid Display | Bật/tắt lưới toạ độ ô vuông trên màn hình |
| **F8** | **Ortho Mode** | **Khóa phương vẽ vuông góc tuyệt đối** (chỉ vẽ ngang hoặc đứng) |
| **F9** | Snap Mode | Bật/tắt chế độ bước nhảy chuột theo mắt lưới |
| **F10** | Polar Tracking | Vẽ theo góc định hướng tuỳ biến (15°, 30°, 45°...) |
| **F11** | Object Snap Tracking | Bắt điểm dóng hàng ảo từ các đỉnh đối tượng |
| **F12** | **Dynamic Input** | **Hiển thị thông số kích thước và góc trực tiếp tại đầu con trỏ chuột** |

## 10 mẹo vẽ siêu tốc của chuyên gia AutoCAD

1. **Phím Spacebar là phím Enter:** Tuyệt đối không dùng ngón út với sang phím [Enter] xa xôi. Luôn dùng ngón tay cái bên trái dập phím cách `[Spacebar]` để thực thi lệnh hoặc gọi lại lệnh vừa dùng.
2. **Nhấn Spacebar lần 2 để lặp lại lệnh:** Vừa vẽ xong một hình tròn, chỉ cần nhấn `[Spacebar]` là AutoCAD tự động gọi lại lệnh `CIRCLE` ngay lập tức!
3. **Giữ phím Shift để đảo ngược công năng:** Khi đang dùng lệnh `TRIM` (cắt tỉa), nhấn giữ phím [Shift] sẽ biến con trỏ thành lệnh `EXTEND` (phóng dài) mà không cần đổi lệnh!
4. **Giữ phím Shift khi chọn đối tượng:** Bấm chọn nhầm đối tượng trong một cụm lớn? Nhấn giữ [Shift] và bấm vào đối tượng đó để loại trừ (Remove from selection) mà không phải chọn lại từ đầu.
5. **Mở rộng tối đa màn hình vẽ ([Ctrl + 0]):** Tổ hợp phím `Clean Screen` ẩn toàn bộ dải Ribbon và thanh công cụ cồng kềnh, biến toàn bộ màn hình máy tính thành một tờ giấy vẽ mênh mông! Bấm `Ctrl + 0` lần nữa để khôi phục.
6. **Bật tắt nhanh các bảng palette thần thánh:**
   - [Ctrl + 1]: Bảng thuộc tính Properties.
   - [Ctrl + 2]: AutoCAD DesignCenter.
   - [Ctrl + 3]: Tool Palettes kho chi tiết.
   - [Ctrl + 9]: Bật lại dòng lệnh khi lỡ tay tắt mất.
7. **Dán thành Block ngay lập tức ([Ctrl + Shift + V]):** Quét chọn các nét, nhấn [Ctrl + C] để copy, rồi nhấn [Ctrl + Shift + V] để dán ra màn hình dưới dạng một khối Block thống nhất không cần gõ lệnh `BLOCK`.
8. **Đổi màu nền đen sâu (True Black):** Màn hình xám mặc định của AutoCAD đời mới dễ gây mỏi mắt khi vẽ lâu. Vào `OPTIONS` > thẻ *Display* > nút *Colors* > đổi màu 2D Model space thành màu đen tuyền `#000000` để các nét màu nổi bật và bảo vệ mắt.
9. **Dùng lệnh MATCHPROP (MA) như chổi quét thần kỳ:** Sao chép toàn bộ thuộc tính layer, màu sắc, linetype và lineweight từ nét này sang hàng loạt nét khác chỉ bằng 1 cú quẹt chuột.
10. **Tự động lưu file an toàn (SAVETIME):** Gõ biến hệ thống `SAVETIME` và đặt bằng `5` (phút) để không bao giờ bị mất quá 5 phút công sức vẽ khi máy tính gặp sự cố.

> [!TIP]
> Lưu không gian làm việc cá nhân của bạn bằng lệnh `WSSAVE` (Workspace Save) với tên riêng của bạn (ví dụ `KHONG_GIAN_LAM_VIEC_TOI_UU`). Dù người khác có nghịch làm xáo trộn giao diện, bạn chỉ việc chọn lại tên mình là mọi thứ lập tức trở về đúng trật tự!

## Tự kiểm tra

```quiz
id: q-ac-08-07-1
type: single
question: "Lệnh nào trong AutoCAD mở trung tâm tùy biến toàn diện giao diện người dùng (Ribbon, Quick Access Toolbar, chuột và phím tắt)?"
options:
  - text: "CUI (Customize User Interface)"
    correct: true
    why: "CUI là lệnh điều khiển toàn bộ cấu trúc giao diện người dùng của phần mềm."
  - text: "GUI"
    why: "GUI là thuật ngữ chung về giao diện đồ họa, không phải lệnh AutoCAD."
  - text: "MENU"
    why: "MENU chỉ nạp lại tệp giao diện mặc định."
  - text: "CUSTOM"
    why: "CUSTOM không phải lệnh nội bộ chuẩn."
explain: "Sử dụng lệnh CUI để tùy chỉnh và cá nhân hóa sâu sắc không gian làm việc của bạn."
```

```quiz
id: q-ac-08-07-2
type: single
question: "Phím chức năng nào trên bàn phím dùng để bật hoặc tắt nhanh chế độ vẽ vuông góc tuyệt đối Ortho Mode?"
options:
  - text: "Phím F8"
    correct: true
    why: "F8 là phím tắt mặc định khóa các đường thẳng chạy thẳng đứng hoặc nằm ngang."
  - text: "Phím F3"
    why: "F3 dùng để bật tắt truy bắt điểm Osnap."
  - text: "Phím F7"
    why: "F7 dùng để bật tắt lưới Grid."
  - text: "Phím F12"
    why: "F12 dùng để bật tắt Dynamic Input."
explain: "F8 và F3 là hai phím chức năng được sử dụng nhiều nhất trong suốt quá trình vẽ kỹ thuật."
```

```quiz
id: q-ac-08-07-3
type: truefalse
question: "Khi đang thực hiện lệnh TRIM, bạn có thể nhấn giữ phím Shift để tạm thời chuyển sang tính năng của lệnh EXTEND mà không cần phải thoát lệnh."
answer: true
explain: "Tính năng giữ Shift để đảo ngược công năng giữa TRIM và EXTEND là một trong những mẹo tăng tốc độ vẽ kinh điển của các chuyên gia AutoCAD."
```

## Lỗi thường gặp

- **Vô tình làm mất dải Ribbon hoặc thanh dòng lệnh:** Do bấm nhầm tổ hợp phím [Ctrl + 0] (Clean Screen) hoặc [Ctrl + 9]. Khắc phục: Nhấn lại [Ctrl + 0] để mở lại Ribbon và nhấn [Ctrl + 9] để hiện lại Command Line.
- **Mất thanh menu trên cùng (Menu Bar):** Gõ biến hệ thống `MENUBAR` và đặt giá trị là `1` để hiển thị lại hàng menu File, Edit, View, Insert cổ điển.

## Bài tập thực hành

- [ ] Gõ lệnh `CUI` để mở hộp thoại Customize User Interface. <!-- expect: CUI -->
- [ ] Quan sát cây thư mục cấu hình: `Quick Access Toolbars`, `Ribbon`, `Toolbars`.
- [ ] Bấm nút Cancel để đóng hộp thoại CUI an toàn.
- [ ] Nhấn thử tổ hợp phím `Ctrl + 0` để trải nghiệm chế độ toàn màn hình Clean Screen, sau đó nhấn lại `Ctrl + 0` để khôi phục.
- [ ] Nhấn lần lượt các phím chức năng `F3` (Osnap) và `F8` (Ortho) để quan sát thông báo trạng thái dưới dòng lệnh.

## Nguồn tham khảo

```links
- title: "Tùy biến giao diện với lệnh CUI từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=CUI"
  kind: official
- title: "Phím tắt và phím chức năng AutoCAD từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=Function+Keys"
  kind: official
```
