---
id: ac-06-03
title: Khối động thông minh với Dynamic Block cơ bản (BEDIT)
category: Khối và Tham chiếu
tags: [dynamic-block, bedit, parameter, action, nang-cao]
level: intermediate
minutes: 25
needs: [ac-06-01]
appVersions: ['2024', '2025']
edition: all
---
# Khối động thông minh với Dynamic Block cơ bản (BEDIT)

> **Mục tiêu:**
> - Sử dụng môi trường Block Editor (`BEDIT`) để biên tập và thêm trí thông minh cho khối.
> - Hiểu và làm chủ nguyên lý cặp đôi: Tham số ([[Parameter]]) và Hành động (Action).
> - Tạo thành thạo 3 loại khối động phổ biến nhất: Co giãn (Stretch), Lật đối xứng (Flip) và Ẩn hiện (Visibility).

## Khái niệm Dynamic Block: Một khối thay thế hàng trăm khối tĩnh

Trong thư viện CAD thông thường, nếu bạn cần một cánh cửa đi, bạn sẽ phải tạo:
- `Cửa 1 cánh mở trái 800mm`, `Cửa 1 cánh mở phải 800mm`.
- `Cửa 1 cánh mở trái 900mm`, `Cửa 1 cánh mở phải 900mm`.
- `Cửa 2 cánh 1200mm`, `Cửa 2 cánh 1400mm`...

Kết quả là thư viện của bạn bị phình to với hàng trăm block tĩnh vụn vặt.

**[[DynamicBlock]] (Khối động)** ra đời để giải quyết tận gốc vấn đề này. Chỉ cần duy nhất 1 khối Block, nhưng khi chèn vào bản vẽ:
- Bạn có thể **kéo mũi tên (Grip)** để co giãn chiều rộng từ 700mm đến 1200mm.
- Bạn có thể **bấm mũi tên lật** để đổi chiều mở cửa trái/phải chỉ trong 1 tích tắc.
- Bạn có thể **bấm menu thả xuống** để chuyển từ cửa 1 cánh sang cửa 2 cánh hoặc cửa lùa!

![Cấu trúc và nguyên lý của Dynamic Block](media/ac-06-03-dynamic-block.svg)

```hotspots
image: media/ac-06-03-dynamic-block.svg
alt: Ba cơ chế tham số và hành động phổ biến nhất của Dynamic Block
layout: central
points:
  - id: spot-1
    x: 18
    y: 35
    title: Tham số dài Linear + Action Stretch
    text: Tạo tay cầm kéo dài chi tiết dầm, cột, thép theo phương tuyến tính.
  - id: spot-2
    x: 50
    y: 35
    title: Trục lật Flip Parameter
    text: Tạo nút bấm đảo chiều đối xứng gương cho các chi tiết có hướng như cửa hoặc chữ.
  - id: spot-3
    x: 82
    y: 35
    title: Trạng thái hiển thị Visibility States
    text: Menu danh sách xổ xuống cho phép ẩn/hiện các biến thể chi tiết khác nhau trong 1 block.
```

## Công thức cốt lõi: Parameter + Action

Mọi khối động trong AutoCAD đều hoạt động theo một nguyên lý toán học đơn giản:
$$\text{Dynamic Block} = \text{Hình vẽ} + \text{Tham số (Parameter)} + \text{Hành động (Action)}$$

- **Tham số (Parameter):** Xác định thuộc tính hình học cần thay đổi (chiều dài, góc xoay, trục đối xứng, điểm đặt). Khi đặt tham số, một tay kẹp (Grip) sẽ xuất hiện trên màn hình.
- **Hành động (Action):** Xác định phần mềm phải làm gì khi người vẽ kéo tay kẹp đó (kéo dãn `Stretch`, di chuyển `Move`, xoay `Rotate`, phóng to `Scale`, hoặc mảng `Array`).

## Cách tạo từng bước trong môi trường Block Editor

### 1. Mở Block Editor với lệnh BEDIT
1. Gõ `BEDIT` (hoặc `BE`) rồi nhấn [Enter].
2. Chọn tên khối cần biến thành khối động trong danh sách, bấm **OK**.
3. Màn hình chuyển sang giao diện nền xám đặc trưng của **Block Editor** cùng bảng công cụ **Block Authoring Palettes**.

### 2. Tạo tính năng co giãn chiều dài (Linear + Stretch)
1. Trên bảng palette thẻ **Parameters**, chọn **Linear**.
2. Bấm điểm đầu và điểm cuối của đoạn thẳng cần co giãn. Một đoạn kích thước màu vàng mang tên `Distance1` xuất hiện kèm 2 mũi tên.
3. Chuyển sang thẻ **Actions**, chọn **Stretch**.
4. AutoCAD yêu cầu:
   - *Select parameter:* Bấm chọn vào chữ `Distance1`.
   - *Specify parameter point:* Bấm chọn mũi tên bên phải (mũi tên sẽ dùng để kéo).
   - *Specify first corner of stretch frame:* Quét một khung cửa sổ Crossing bao quanh đầu bên phải của chi tiết (giống hệt lệnh STRETCH).
   - *Select objects:* Quét chọn các nét vẽ cần bị kéo dãn, nhấn [Enter].
5. Một biểu tượng hình bàn tay nhỏ xuất hiện bên cạnh chữ `Distance1`. Hành động đã được gắn kết thành công!

### 3. Tạo tính năng đảo hướng lật (Flip Parameter + Flip Action)
1. Trong thẻ **Parameters**, chọn **Flip**.
2. Bấm 2 điểm để vẽ một đường trục đối xứng (ví dụ trục dọc qua giữa khung cửa).
3. Đặt chữ nhãn `Flip state1`.
4. Chuyển sang thẻ **Actions**, chọn **Flip**.
5. Bấm chọn nhãn `Flip state1`, sau đó quét chọn toàn bộ các nét vẽ của cánh cửa, nhấn [Enter].

### 4. Kiểm tra và lưu lại
1. Trên thanh Ribbon, bấm nút **Test Block**. Một cửa sổ thử nghiệm mở ra: bạn thử bấm vào block và kéo các mũi tên xem hình vẽ có co giãn và lật đúng ý không.
2. Đóng cửa sổ thử nghiệm.
3. Bấm nút **Close Block Editor** (`BCLOSE`) và chọn **Save the changes to...** (`BSAVE`).

## Tuỳ chọn và mẹo kiểm soát dải kích thước (Value Set)

Khi tạo tham số `Linear`, bạn thường không muốn người vẽ kéo một kích thước tùy tiện (ví dụ kéo cánh cửa ra 837.25mm rất khó sản xuất). Bạn có thể giới hạn dải kích thước:
- Chọn tham số `Distance1` trong Block Editor, mở bảng thuộc tính [[Properties]] ([Ctrl + 1]).
- Tìm mục **Value Set** > dòng **Dist type**:
  - Chọn **List:** Nhập các kích thước chuẩn sản xuất (ví dụ: `800`, `900`, `1000`, `1200`). Lúc này khi kéo grip, chi tiết chỉ nhảy đúng vào các mốc kích thước này!
  - Chọn **Increment:** Nhập bước nhảy (ví dụ mỗi nấc kéo nhảy đều đặn 50mm).

> [!TIP]
> Visibility State là tính năng cực kỳ hữu ích để làm ký hiệu mặt cắt: trong 1 block bạn có thể chọn hiển thị mặt cắt thép chữ I, thép chữ U, hoặc thép chữ V mà không cần tạo 3 block khác nhau.

## Tự kiểm tra

```quiz
id: q-ac-06-03-1
type: single
question: "Hai thành phần bắt buộc phải kết hợp với nhau để tạo nên tính năng biến đổi hình học trong Dynamic Block là gì?"
options:
  - text: "Tham số (Parameter) và Hành động (Action)"
    correct: true
    why: "Mọi biến đổi đều cần một Parameter định vị và một Action thực thi lệnh tương ứng."
  - text: "Layer và Linetype"
    correct: false
    why: "Layer và Linetype chỉ quản lý hiển thị nét vẽ."
  - text: "Command line và Status bar"
    correct: false
    why: "Đây là các thành phần giao diện của AutoCAD."
  - text: "Font chữ và Khổ giấy in"
    correct: false
    why: "Không liên quan đến cơ chế biến đổi hình học của khối động."
explain: "Parameter định nghĩa thuộc tính đo lường (như độ dài, góc, trục lật), còn Action định nghĩa hành vi (như Stretch, Move, Rotate, Flip)."
```

```quiz
id: q-ac-06-03-2
type: single
question: "Nút bấm nào trên thanh Ribbon trong môi trường Block Editor cho phép bạn kiểm tra thử hoạt động của khối động trước khi lưu?"
options:
  - text: "Test Block"
    correct: true
    why: "Test Block mở môi trường thử nghiệm tạm thời an toàn mà không làm hỏng bản vẽ chính."
  - text: "BCLOSE"
    correct: false
    why: "BCLOSE đóng cửa sổ biên tập khối."
  - text: "EXPLODE"
    correct: false
    why: "EXPLODE làm nổ tung khối thành từng nét rời rạc."
  - text: "PURGE"
    correct: false
    why: "PURGE dùng để dọn dẹp các đối tượng rác."
explain: "Test Block là công cụ tiêu chuẩn để kiểm tra tính mượt mà của các điểm kéo Grip trước khi phát hành khối."
```

```quiz
id: q-ac-06-03-3
type: truefalse
question: "Thiết lập Dist Type thành kiểu List trong bảng Properties của tham số Linear cho phép bạn giới hạn các kích thước chuẩn cố định khi kéo dãn Block."
answer: false
explain: "Sử dụng tính năng Value Set dạng List giúp chuẩn hóa kích thước sản xuất, tránh cho người vẽ nhập các kích thước tùy tiện."
```

## Lỗi thường gặp

- **Kéo mũi tên nhưng một nửa chi tiết bị bỏ lại phía sau:** Do khi chọn khung kéo dãn trong Action Stretch, bạn chưa bao trọn các đỉnh của chi tiết, hoặc chưa chọn đủ đối tượng trong bước Select Objects. Khắc phục: Nhấp đúp vào biểu tượng Action Stretch trong BEDIT để xác định lại khung và đối tượng.
- **Biểu tượng dấu chấm than màu vàng xuất hiện trên Parameter:** Cảnh báo tham số đó chưa được gán Hành động (Action) nào để điều khiển nó. Khắc phục: Vào thẻ Actions và gán hành động tương ứng.

## Bài tập thực hành

- [ ] Vẽ một thanh thép hình chữ nhật 200 x 30 mm bằng `RECTANG` và đóng gói thành khối bằng `BLOCK` tên `THEP-DYNAMIC`. <!-- expect: BLOCK -->
- [ ] Gõ `BEDIT`, chọn khối `THEP-DYNAMIC` để vào môi trường sửa khối. <!-- expect: BEDIT -->
- [ ] Gán tham số `Linear` theo chiều dài 200mm. <!-- expect: BEDIT -->
- [ ] Gán hành động `Stretch` cho mũi tên bên phải của thanh thép. <!-- expect: BEDIT -->
- [ ] Bấm nút **Close Block Editor** (`BCLOSE`) và chọn lưu thay đổi (`BSAVE`). <!-- expect: BCLOSE -->
- [ ] Bấm chọn khối trên bản vẽ và thử kéo tay kẹp hình tam giác để dãn thanh thép dài thành 350mm.

## Nguồn tham khảo

```links
- title: "Tổng quan về Dynamic Blocks chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Dynamic+Blocks"
  kind: official
- title: "Hướng dẫn môi trường Block Editor (BEDIT) từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=BEDIT"
  kind: official
```
