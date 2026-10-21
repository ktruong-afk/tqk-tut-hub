---
id: ac-01-01
title: Làm quen giao diện và vùng làm việc AutoCAD
category: Làm quen
tags: [giao-dien, ribbon, status-bar, co-ban]
level: beginner
minutes: 15
needs: []
appVersions: ['2024', '2025']
edition: all
---
# Làm quen giao diện và vùng làm việc AutoCAD

> **Mục tiêu:**
> - Nhận biết các khu vực chức năng chính trên màn hình làm việc AutoCAD.
> - Sử dụng thanh dòng lệnh và thanh trạng thái để kiểm soát trạng thái vẽ.
> - Thao tác ẩn hiện các thành phần giao diện khi cần mở rộng không gian quan sát.

## Lệnh này làm gì và khi nào dùng

Khi lần đầu khởi động AutoCAD, bạn sẽ làm việc trong không gian làm việc mặc định có tên **Drafting & Annotation**. Giao diện này được tổ chức khoa học với các khu vực chuyên biệt: đỉnh màn hình là [[Dải Ribbon]] chứa hầu hết các công cụ vẽ và hiệu chỉnh; trung tâm là [[Vùng vẽ]] vô hạn màu tối; đáy màn hình là [[Dòng lệnh]] và [[Thanh trạng thái]].

Hiểu rõ cấu trúc giao diện giúp bạn phản xạ nhanh, tìm đúng công cụ khi thiết kế và không bị bỡ ngỡ khi các bảng điều khiển vô tình bị tắt.

```hotspots
image: media/ac-01-01-giao-dien.svg
alt: Sơ đồ các khu vực chính trên giao diện làm việc AutoCAD Drafting & Annotation
layout: central
points:
  - id: ribbon-area
    x: 48
    y: 10
    title: Dải Ribbon
    text: Nơi tập hợp toàn bộ công cụ vẽ, chỉnh sửa, ghi kích thước và quản lý layer theo từng thẻ chức năng.
  - id: drawing-canvas
    x: 50
    y: 52
    title: Vùng vẽ (Drawing Area)
    text: Không gian đồ hoạ chính để hiển thị và tạo dựng mô hình bản vẽ kỹ thuật.
    quiz: q-ac-01-01-1
  - id: viewcube-nav
    x: 93
    y: 29
    title: ViewCube
    text: Khối điều hướng 3D ảo cho phép chuyển nhanh giữa các góc nhìn Top, Front, Right hoặc trục đo.
  - id: command-line
    x: 50
    y: 80
    title: Thanh dòng lệnh (Command Line)
    text: Trái tim điều khiển của AutoCAD. Mọi lệnh gõ phím, chuỗi nhắc và thông số tuỳ chọn đều hiển thị tại đây.
    quiz: q-ac-01-01-2
  - id: status-bar
    x: 50
    y: 91
    title: Thanh trạng thái (Status Bar)
    text: Chứa toạ độ con trỏ và các biểu tượng bật/tắt chế độ hỗ trợ vẽ như Grid, Ortho, Osnap, Dynamic Input.
```

## Cách dùng từng bước

1. **Khởi tạo không gian:** Mở AutoCAD, nhấp nút **New** trên màn hình Start để vào vùng vẽ bản vẽ mới (`Drawing1.dwg`).
2. **Quan sát dòng lệnh:** Nhìn xuống đáy màn hình, bạn thấy dòng nhắc `Type a command`. Đây là nơi nhận lệnh bàn phím.
3. **Thử gọi lệnh bằng phím tắt:** Gõ phím `L` rồi nhấn [Spacebar] hoặc [Enter]. Dòng lệnh sẽ chuyển thành `LINE Specify first point:`.
4. **Huỷ lệnh an toàn:** Nhấn phím [Esc] trên bàn phím. Dòng lệnh trở về trạng thái sẵn sàng ban đầu.
5. **Mở rộng không gian làm việc:** Nhấn tổ hợp phím [Ctrl + 0] (Clean Screen) để ẩn toàn bộ Ribbon; nhấn lại [Ctrl + 0] để hiện lại.

## Tuỳ chọn và mẹo

> [!TIP]
> Nếu vô tình làm mất thanh dòng lệnh bên dưới màn hình, hãy nhấn tổ hợp phím [Ctrl + 9] để bật lại ngay lập tức thay vì phải cài đặt lại phần mềm.

> [!TIP]
> Bạn có thể kéo thả thanh dòng lệnh để thả nổi ở giữa màn hình hoặc gắn cố định vào đáy cửa sổ tuỳ theo thói quen quan sát.

## Tự kiểm tra

```quiz
id: q-ac-01-01-1
type: single
question: Khu vực nào trên màn hình hiển thị trực tiếp các đối tượng hình học đang vẽ?
options:
  - { text: Vùng vẽ (Drawing Area), correct: true, why: Vùng vẽ là không gian đồ hoạ trung tâm chứa toàn bộ hình học kỹ thuật }
  - { text: Dải Ribbon, why: Ribbon chỉ chứa các nút lệnh và công cụ }
  - { text: Dòng lệnh, why: Dòng lệnh dùng để nhập lệnh và đọc hướng dẫn }
  - { text: Thanh trạng thái, why: Thanh trạng thái chứa các công tắc bật tắt chế độ vẽ }
explain: Vùng vẽ (Drawing Area) chiếm phần lớn diện tích màn hình, là không gian đồ hoạ 2D/3D nơi bạn tạo lập và quan sát bản vẽ.
tags: [giao-dien, drawing-area]
```

```quiz
id: q-ac-01-01-2
type: single
question: Phím tắt nào dùng để ẩn hoặc hiện thanh dòng lệnh (Command Line)?
options:
  - { text: Ctrl + 9, correct: true, why: Ctrl + 9 là phím tắt mặc định để bật tắt hiển thị dòng lệnh }
  - { text: Ctrl + 1, why: Ctrl + 1 dùng để mở bảng thuộc tính Properties }
  - { text: Ctrl + 0, why: Ctrl + 0 dùng cho chế độ Clean Screen ẩn Ribbon }
  - { text: F2, why: F2 mở cửa sổ lịch sử dòng lệnh chứ không ẩn thanh lệnh }
explain: Nhấn [Ctrl + 9] sẽ xuất hiện hộp thoại xác nhận đóng hoặc mở lại thanh Command Line trên màn hình.
tags: [giao-dien, phim-tat]
```

```quiz
id: q-ac-01-01-3
type: truefalse
question: Nhấn phím [Esc] giúp huỷ bỏ lệnh đang thực hiện và đưa AutoCAD về trạng thái sẵn sàng.
answer: true
explain: Phím [Esc] là phím thoát huỷ lệnh tiêu chuẩn trong AutoCAD. Khi gặp sự cố thao tác nhầm, bạn luôn có thể nhấn [Esc] một hoặc hai lần.
tags: [giao-dien, esc]
```

```quiz
id: q-ac-01-01-4
type: hotspot
question: Bấm vào vị trí của Dải Ribbon trên sơ đồ giao diện.
use: hotspots
answer: ribbon-area
explain: Dải Ribbon nằm ở phía trên cùng của giao diện, gom các nhóm lệnh theo từng tab chức năng.
tags: [giao-dien, ribbon]
```

## Lỗi thường gặp

- **Triệu chứng:** Mất hoàn toàn thanh dòng lệnh, gõ chữ không biết lệnh đang hỏi gì.
  - *Nguyên nhân:* Vô tình bấm nhầm dấu X đóng cửa sổ dòng lệnh hoặc bấm nhầm [Ctrl + 9].
  - *Cách sửa:* Nhấn tổ hợp phím [Ctrl + 9] trên bàn phím để kích hoạt lại dòng lệnh.
- **Triệu chứng:** Toàn bộ thanh công cụ Ribbon biến mất, màn hình chỉ còn vùng đen lớn.
  - *Nguyên nhân:* Vô tình kích hoạt chế độ toàn màn hình Clean Screen bằng phím [Ctrl + 0].
  - *Cách sửa:* Nhấn lại [Ctrl + 0] để đưa giao diện trở lại bố cục đầy đủ.

## Bài tập thực hành

- [ ] Khởi động AutoCAD và quan sát các thành phần giao diện trên màn hình.
- [ ] Nhấn phím [Ctrl + 9] để ẩn dòng lệnh, sau đó nhấn lại [Ctrl + 9] để hiện lại.
- [ ] Nhấn [Ctrl + 0] để chuyển sang chế độ Clean Screen, quan sát diện tích vùng vẽ rồi nhấn [Ctrl + 0] lần nữa để hoàn tất.
- [ ] Gõ `LINE` trên bàn phím rồi nhấn phím [Spacebar] để kích hoạt lệnh vẽ đường thẳng. <!-- expect: LINE -->
- [ ] Nhấn phím [Esc] hai lần để huỷ lệnh và quan sát dòng lệnh trở về trạng thái sẵn sàng.

## Nguồn tham khảo

```links
- title: Giao diện người dùng AutoCAD (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=User+Interface
  kind: official
  lang: en
  note: Hướng dẫn chi tiết từng thành phần giao diện từ tài liệu chuẩn của hãng Autodesk
- title: Tổng quan về AutoCAD (Wikipedia tiếng Việt)
  url: https://vi.wikipedia.org/wiki/AutoCAD
  kind: article
  lang: vi
  note: Giới thiệu lịch sử phát triển và các phiên bản phần mềm AutoCAD
```
