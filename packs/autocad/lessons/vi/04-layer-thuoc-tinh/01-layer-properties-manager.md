---
id: ac-04-01
title: Quản lý lớp bản vẽ với Layer Properties Manager
category: Layer & Thuộc tính
tags: [layer, layer-properties-manager, quan-ly-lop, tao-layer, co-ban]
level: beginner
minutes: 15
needs: [ac-03-12]
appVersions: ['2024', '2025']
edition: all
---
# Quản lý lớp bản vẽ với Layer Properties Manager

> **Mục tiêu:**
> - Sử dụng bảng Layer Properties Manager để tạo mới, đổi tên và xoá các lớp bản vẽ (Layer).
> - Kiểm soát các trạng thái cơ bản của layer: Bật/Tắt (On/Off), Đóng băng (Freeze) và Khoá (Lock).
> - Hiểu rõ vai trò của Layer 0 mặc định và thiết lập Layer hiện hành (Current Layer) khi vẽ.

## Lệnh này làm gì và khi nào dùng

Hãy tưởng tượng bạn vẽ một công trình xây dựng phức tạp lên nhiều tờ giấy bóng kính trong suốt xếp chồng lên nhau: một tờ vẽ cột tường bê tông, một tờ vẽ đường ống nước, một tờ vẽ dây điện và một tờ vẽ bàn ghế nội thất. Khi cần xem riêng hệ thống điện nước, bạn chỉ việc rút các tờ giấy khác ra. Đó chính là nguyên lý của [[Lớp bản vẽ]] (Layer) trong AutoCAD.

Lệnh `LAYER` (phím tắt `LA`) mở bảng [[Quản lý lớp]] (Layer Properties Manager) - trung tâm chỉ huy tổ chức toàn bộ bản vẽ:
- **Tên Layer (Name):** Phân loại cấu kiện (ví dụ `Net-Thay`, `Net-Khuat`, `Kich-Thuoc`, `Cot-Truc`).
- **On / Off (Bật / Tắt - biểu tượng bóng đèn 💡):** Ẩn hoặc hiện các đối tượng thuộc layer trên màn hình.
- **Freeze / Thaw ([[Đóng băng lớp]] - biểu tượng mặt trời ☀️ / bông tuyết ❄️):** Ẩn layer đồng thời giải phóng bộ nhớ đồ hoạ giúp bản vẽ chạy mượt hơn.
- **Lock / Unlock ([[Khoá lớp]] - biểu tượng ổ khoá 🔓 / 🔒):** Vẫn cho nhìn thấy đối tượng trên màn hình nhưng khoá chặt, ngăn ngừa tuyệt đối mọi thao tác xoá nhầm hay di chuyển nhầm.

```hotspots
image: media/ac-04-01-layer-manager.svg
alt: Bảng điều khiển Layer Properties Manager hiển thị danh sách các layer, màu sắc, linetype và lineweight
layout: central
points:
  - id: layer-new-btn
    x: 8
    y: 17
    title: Nút tạo Layer mới (+ New Layer)
    text: Tạo một lớp mới trong bản vẽ (phím tắt Alt + N trong bảng).
    quiz: q-ac-04-01-1
  - id: layer-status-icons
    x: 40
    y: 40
    title: Các cột trạng thái (On, Freeze, Lock)
    text: Biểu tượng bóng đèn (ẩn/hiện), mặt trời (đóng băng đồ hoạ) và ổ khoá (bảo vệ không cho sửa).
    quiz: q-ac-04-01-2
```

## Cách dùng từng bước

1. **Mở bảng Layer Properties Manager:**
   - Gõ lệnh `LAYER` hoặc phím tắt `LA` rồi nhấn [Enter].
   - Hoặc nhấp vào biểu tượng lớn *Layer Properties* trên thẻ Home của Ribbon.
2. **Tạo Layer mới:**
   - Bấm vào nút biểu tượng **New Layer** (hoặc nhấn tổ hợp [Alt + N]).
   - Gõ tên cho layer mới (ví dụ `Net-Thay`).
3. **Gán thuộc tính cho Layer:**
   - Nhấp vào ô màu sắc (Color) của layer: Chọn màu mong muốn trong bảng Select Color (ví dụ màu White cho nét thấy, màu Red cho nét trục) rồi bấm OK.
   - Nhấp vào ô Linetype: Chọn kiểu đường nét (Continuous, Hidden, Center...).
   - Nhấp vào ô Lineweight: Chọn độ dày nét in (ví dụ 0.35mm cho nét thấy).
4. **Đặt làm Layer hiện hành (Set Current):**
   - Nhấp chọn tên layer vừa tạo rồi bấm vào nút có dấu tích xanh **Set Current** (hoặc nhấp đúp chuột vào tên layer).
   - Từ thời điểm này, mọi hình học bạn vẽ ra (Line, Circle, Text...) sẽ tự động thuộc về layer đó.
5. **Chuyển đối tượng đã vẽ sang Layer khác:**
   - Nhấp chọn các đối tượng đang có trên màn hình.
   - Bấm vào thanh danh sách cuộn Layer trên dải Ribbon và chọn tên layer đích.
   - Nhấn phím [Esc] để bỏ chọn.

## Tuỳ chọn và mẹo

> [!TIP]
> **Tuyệt đối không vẽ toàn bộ bản vẽ trên Layer 0!** Layer 0 là lớp mặc định đặc biệt của AutoCAD, dùng để định nghĩa khối thư viện Block hoặc làm việc nội bộ. Hãy luôn tạo các layer riêng biệt trước khi bắt tay vào vẽ.

> [!TIP]
> Sử dụng tính năng **Lock (Khoá layer)** khi bạn chuẩn bị thực hiện các lệnh xoá hoặc quét chọn hàng loạt: Các đối tượng thuộc layer bị khoá sẽ tự động mờ đi và được bảo vệ 100%, không lệnh nào có thể xoá hay dời chúng đi được.

## Tự kiểm tra

```quiz
id: q-ac-04-01-1
type: single
question: Khi bạn khoá một Layer bằng biểu tượng chiếc ổ khoá (Lock), các đối tượng thuộc Layer đó sẽ có trạng thái như thế nào?
options:
  - text: Vẫn hiển thị trên màn hình nhưng không thể bị xoá, di chuyển hay chỉnh sửa nhầm
    correct: true
    why: Lock bảo vệ an toàn đối tượng không cho phép sửa đổi nhưng vẫn nhìn thấy và bắt điểm được
  - text: Biến mất hoàn toàn khỏi màn hình
    why: Biến mất là chức năng của On/Off hoặc Freeze
  - text: Bị xoá vĩnh viễn khỏi bản vẽ
    why: Khoá layer không làm mất dữ liệu
  - text: Tự động đổi màu sang màu đen
    why: Đối tượng chỉ bị mờ nhẹ để báo hiệu đang bị khoá
explain: "Tính năng Lock (Khoá layer) giúp bảo vệ các đối tượng quan trọng (như khung tên, tim trục) không bị vô tình xoá nhầm hoặc dịch chuyển khi bạn quét chuột chỉnh sửa bản vẽ."
tags: [layer, lock, an-toan]
```

```quiz
id: q-ac-04-01-2
type: single
question: Phím tắt tiêu chuẩn nào dùng để mở nhanh bảng Layer Properties Manager trong AutoCAD?
options:
  - text: LA
    correct: true
    why: LA là phím tắt chính thức của lệnh LAYER
  - text: L
    why: L là phím tắt của lệnh LINE
  - text: LY
    why: LY không phải phím tắt chuẩn
  - text: LR
    why: LR không phải phím tắt chuẩn
explain: "Gõ LA rồi nhấn Spacebar hoặc Enter là cách nhanh nhất để gọi bảng điều khiển quản lý lớp Layer Properties Manager."
tags: [layer, phim-tat]
```

```quiz
id: q-ac-04-01-3
type: truefalse
question: Layer 0 là lớp mặc định có sẵn trong mọi bản vẽ AutoCAD và không thể bị xoá bỏ hay đổi tên.
answer: true
explain: "Layer 0 là lớp hệ thống đặc thù gắn liền với nhân đồ hoạ của AutoCAD, không thể xoá bỏ, không thể đổi tên và có các tính chất đặc biệt khi tạo khối Block."
tags: [layer, layer-0]
```

```quiz
id: q-ac-04-01-4
type: hotspot
question: Bấm vào nút tạo Layer mới (+ New Layer) trên bảng điều khiển.
use: hotspots
answer: layer-new-btn
explain: "Nút New Layer nằm ở góc trên bên trái của thanh công cụ trong bảng quản lý layer."
tags: [layer, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Không thể xoá một Layer trong bảng quản lý và nhận thông báo lỗi *"The selected layer was not deleted"*.
  - *Nguyên nhân:* Layer bạn muốn xoá đang là Layer hiện hành (Current Layer), hoặc đang chứa các đối tượng trong bản vẽ, hoặc là Layer 0 / Defpoints.
  - *Cách sửa:* Đặt một layer khác làm Current Layer và dùng lệnh `QSELECT` để xoá sạch các đối tượng đang nằm trên layer đó trước khi xoá layer.
- **Triệu chứng:** Vẽ một hình tròn nhưng không thấy xuất hiện trên màn hình.
  - *Nguyên nhân:* Layer hiện hành đang bị tắt bóng đèn (Turn Off) hoặc đang bị đóng băng (Freeze).
  - *Cách sửa:* Bật sáng biểu tượng bóng đèn của layer đó lên.

## Bài tập thực hành

- [ ] Gõ `LAYER` (hoặc `LA`) để mở bảng Layer Properties Manager. <!-- expect: LAYER -->
- [ ] Bấm nút tạo Layer mới, đặt tên là `Net-Thay` và chọn màu `White`, độ dày nét `0.35 mm`.
- [ ] Tạo layer thứ hai có tên `Net-Khuat`, chọn màu `Yellow` và nạp kiểu đường `HIDDEN`.
- [ ] Nhấp đúp chuột vào layer `Net-Thay` để đặt làm Layer hiện hành.
- [ ] Gõ `LINE` vẽ một hình hộp chữ nhật để kiểm tra nét vẽ tự động thuộc về layer `Net-Thay`. <!-- expect: LINE -->

## Nguồn tham khảo

```links
- title: Bảng quản lý lớp Layer Properties Manager (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Layer+Properties+Manager
  kind: official
  lang: en
  note: Hướng dẫn chi tiết tạo layer, cấu hình On/Off, Freeze, Lock và thuộc tính lớp
- title: Vai trò của Layer 0 và Defpoints trong AutoCAD (Autodesk Support)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Layer+0+and+Defpoints
  kind: official
  lang: en
  note: Giải thích cơ chế đặc biệt của hai layer hệ thống mặc định
```
