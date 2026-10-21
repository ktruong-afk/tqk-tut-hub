---
id: ac-06-01
title: Đóng gói và tái sử dụng hình vẽ với BLOCK, INSERT và WBLOCK
category: Khối và Tham chiếu
tags: [block, insert, wblock, basepoint, quan-ly]
level: intermediate
minutes: 25
needs: [ac-05-10]
appVersions: ['2024', '2025']
edition: all
---
# Đóng gói và tái sử dụng hình vẽ với BLOCK, INSERT và WBLOCK

> **Mục tiêu:**
> - Sử dụng lệnh `BLOCK` để gom nhiều đối tượng rời rạc thành một khối thống nhất có điểm chèn chuẩn.
> - Chèn các khối vào bản vẽ linh hoạt với lệnh `INSERT` theo các hệ số tỉ lệ và góc xoay khác nhau.
> - Xuất khối ra tệp bản vẽ độc lập bằng lệnh `WBLOCK` để tái sử dụng cho các dự án sau.

## Khái niệm khối Block trong AutoCAD

Khi thiết kế một tòa nhà hay một cỗ máy, bạn sẽ thấy vô số chi tiết lặp đi lặp lại: cánh cửa đi, thiết bị vệ sinh, bu lông, đai ốc, ký hiệu trục... Nếu bạn sao chép bằng lệnh `COPY`, bản vẽ sẽ chứa hàng ngàn đường thẳng và đường tròn rời rạc. Khi cần thay đổi kiểu dáng cửa, bạn sẽ phải đi sửa từng cái một!

**[[Block]]** là một trong những tính năng mạnh mẽ nhất của AutoCAD. Nó cho phép bạn "đóng gói" một tập hợp các đối tượng đồ họa thành một thực thể duy nhất với một cái tên cụ thể.

Lợi ích vượt trội khi dùng Block:
1. **Tiết kiệm dung lượng bộ nhớ:** AutoCAD chỉ lưu trữ định nghĩa hình học của Block một lần duy nhất. Mỗi lần bạn chèn (Insert), phần mềm chỉ lưu lại tọa độ và góc xoay.
2. **Cập nhật đồng loạt:** Khi bạn sửa đổi định nghĩa một Block gốc, toàn bộ hàng trăm vị trí đã chèn trên bản vẽ sẽ **tự động thay đổi theo ngay lập tức**!
3. **Thao tác nhanh gọn:** Chọn một chi tiết chỉ bằng 1 cú click chuột, không bao giờ bị rơi rớt nét.

![Nguyên lý hoạt động của khối Block](media/ac-06-01-block-concept.svg)

```hotspots
image: media/ac-06-01-block-concept.svg
alt: Nguyên lý tạo khối và tái sử dụng với lệnh BLOCK và INSERT
layout: central
points:
  - id: spot-1
    x: 24
    y: 35
    title: Đóng gói khối (Lệnh BLOCK)
    text: Gom các nét vẽ cánh cửa và cung mở thành 1 block mang tên 'CUA-DI-D900'.
  - id: spot-2
    x: 14
    y: 53
    title: Điểm chèn cơ sở (Base point)
    text: Tọa độ gốc chốt định vị của Block khi chèn vào bản vẽ.
  - id: spot-3
    x: 57
    y: 40
    title: Chèn Block tiêu chuẩn (Lệnh INSERT)
    text: Chèn vào phòng 1 với tỉ lệ 1:1 và góc xoay 0 độ.
  - id: spot-4
    x: 80
    y: 40
    title: Chèn Block xoay (Rotated)
    text: Chèn vào phòng 2 xoay một góc 90 độ mà không làm thay đổi block gốc.
```

## Cách dùng từng bước

### 1. Tạo Block nội bộ với lệnh BLOCK
1. Vẽ hoàn chỉnh hình dạng đối tượng trên màn hình (ví dụ một cánh cửa rộng 900mm).
2. Gõ `B` hoặc `BLOCK` rồi nhấn [Enter]. Hộp thoại **Block Definition** mở ra.
3. **Name:** Đặt tên khối rõ ràng, gợi nhớ (ví dụ: `CUA-DI-D900` hoặc `BULONG-M16`).
4. **Base Point (Điểm đặt):** Bấm nút **Pick point** rồi bắt điểm vào vị trí then chốt (ví dụ bản lề cửa hoặc tâm bu lông). *Tuyệt đối không để điểm đặt ở toạ độ 0,0 xa tít tắp!*
5. **Objects:** Bấm nút **Select objects**, quét chọn toàn bộ các nét vẽ của cánh cửa, nhấn [Enter].
   - Chọn mục `Convert to block` (biến ngay các nét vừa vẽ thành block).
6. Bấm nút **OK** để tạo khối.

### 2. Chèn Block vào bản vẽ với lệnh INSERT
1. Gõ `I` hoặc `INSERT` rồi nhấn [Enter] để mở bảng điều khiển **Blocks Palette**.
2. Tìm tên block trong danh sách `Current Drawing`.
3. Bấm và kéo thả block vào bản vẽ, hoặc nhấp đúp để chèn.
4. Bạn có thể nhập tỉ lệ phóng to/thu nhỏ (`Scale`) hoặc góc nghiêng (`Rotation`) trực tiếp trong bảng palette trước khi chèn.

### 3. Xuất khối ra thành file DWG riêng biệt với WBLOCK
Lệnh `BLOCK` chỉ lưu khối bên trong tệp bản vẽ hiện tại. Để biến khối này thành một tệp DWG riêng biệt trên ổ cứng máy tính và dùng cho các dự án khác, dùng lệnh `WBLOCK` (Write Block):
1. Gõ `W` hoặc `WBLOCK` rồi nhấn [Enter].
2. Tại mục *Source*, chọn `Block` và chọn tên khối trong danh sách xổ xuống (hoặc chọn `Objects` để xuất trực tiếp các nét vẽ).
3. Tại mục *Destination*, bấm nút `[...]` chọn đường dẫn thư mục lưu trên máy (ví dụ: `D:\THU-VIEN-CAD\CUA-DI-D900.dwg`).
4. Bấm **OK**. Bạn đã có một tệp DWG thư viện độc lập!

## Tuỳ chọn và mẹo quan trọng: Layer 0 và ByBlock

> [!IMPORTANT]
> **Quy tắc vàng vẽ Block:** Hãy vẽ các nét của Block trên **Layer 0** và để màu sắc theo **ByLayer**. Khi làm như vậy, sau khi đóng gói thành Block, bạn chèn Block vào bất kỳ layer nào (ví dụ layer `CUA` màu vàng hay layer `NOI_THAT` màu xanh), Block sẽ tự động đổi màu và độ dày nét theo layer đó!

> [!TIP]
> Nếu lỡ làm nổ một Block thành các nét rời bằng lệnh `EXPLODE`, bạn có thể tạo lại hoặc dùng tổ hợp phím [Ctrl + Shift + V] để dán các nét vừa copy thành một Block ẩn danh (Anonymous Block) cực nhanh.

## Tự kiểm tra

```quiz
id: q-ac-06-01-1
type: single
question: "Tại sao việc chỉ định chính xác Điểm đặt (Base Point) khi tạo Block là cực kỳ quan trọng?"
options:
  - text: "Điểm đặt là vị trí tay cầm con trỏ chuột khi chèn Block vào bản vẽ"
    correct: true
    why: "Nếu không chọn Base Point, điểm đặt mặc định sẽ là 0,0, khiến Block bay ra xa con trỏ chuột khi chèn."
  - text: "Điểm đặt quyết định màu sắc của Block"
    correct: false
    why: "Màu sắc do Layer hoặc thuộc tính ByLayer/ByBlock quyết định."
  - text: "Điểm đặt giúp AutoCAD tự động lưu file sau mỗi 5 phút"
    correct: false
    why: "Điểm đặt chỉ là tọa độ mốc hình học của Block."
  - text: "Điểm đặt làm cho Block không thể bị xóa khỏi bản vẽ"
    correct: false
    why: "Block vẫn có thể bị xóa bằng lệnh ERASE bình thường."
explain: "Nếu quên Pick Point khi tạo Block, tọa độ gốc (0,0) sẽ làm điểm chèn, dẫn đến tình trạng khi gõ INSERT, khối hình bị văng ra xa hàng cây số so với con trỏ chuột."
```

```quiz
id: q-ac-06-01-2
type: single
question: "Khác biệt cốt lõi giữa lệnh BLOCK (B) và WBLOCK (W) trong AutoCAD là gì?"
options:
  - text: "BLOCK lưu khối bên trong bản vẽ hiện hành, WBLOCK xuất khối thành một tệp DWG riêng ngoài ổ cứng"
    correct: true
    why: "WBLOCK (Write Block) ghi dữ liệu ra tệp tin DWG độc lập để dùng chung cho nhiều bản vẽ khác."
  - text: "BLOCK chỉ dùng cho đường thẳng, WBLOCK chỉ dùng cho hình tròn"
    correct: false
    why: "Cả hai đều đóng gói bất kỳ đối tượng hình học nào."
  - text: "BLOCK miễn phí, WBLOCK phải trả tiền bản quyền riêng"
    correct: false
    why: "Cả hai đều là lệnh tiêu chuẩn tích hợp sẵn trong AutoCAD."
  - text: "BLOCK không xoay được góc, WBLOCK xoay được 360 độ"
    correct: false
    why: "Mọi Block đều có thể xoay được góc khi chèn."
explain: "Sử dụng WBLOCK để xây dựng kho thư viện block dùng chung cho toàn bộ phòng ban hoặc dự án công ty."
```

```quiz
id: q-ac-06-01-3
type: truefalse
question: "Nếu bạn vẽ các chi tiết trên Layer 0 với thuộc tính màu ByLayer trước khi tạo Block, Block đó sẽ tự động đổi màu theo màu của layer mà nó được chèn vào."
answer: false
explain: "Vẽ trên Layer 0 là chuẩn mực bắt buộc khi tạo thư viện Block để có thể tái sử dụng linh hoạt trên nhiều bản vẽ khác nhau."
```

## Lỗi thường gặp

- **Chèn Block vào bị văng tít ra ngoài màn hình:** Do khi tạo lệnh `BLOCK`, bạn quên bấm nút `Pick Point` nên điểm đặt bị gán toạ độ gốc `0,0,0`. Khắc phục: Mở trình sửa block bằng `BEDIT` và dùng lệnh `BASE` để định lại điểm chèn.
- **Block không đổi màu theo layer mới:** Do lúc vẽ chi tiết ban đầu, bạn đã gán một màu cố định (ví dụ ép màu Red) thay vì để `ByLayer` trên `Layer 0`.

## Bài tập thực hành

- [ ] Chuyển sang `Layer 0`. Vẽ một cánh cửa kích thước 50 x 900 mm bằng `RECTANG` và một cung cong mở góc 90 độ bằng `ARC`. <!-- expect: RECTANG -->
- [ ] Gõ lệnh `BLOCK` (hoặc `B`), đặt tên là `TEST-CUA-900`. <!-- expect: BLOCK -->
- [ ] Bấm nút `Pick point`, chọn điểm chân bản lề góc cánh cửa; quét chọn toàn bộ hình và bấm OK. <!-- expect: BLOCK -->
- [ ] Gõ lệnh `INSERT` (hoặc `I`), chèn 2 bản sao của khối vừa tạo vào màn hình với góc xoay 0 độ và 90 độ. <!-- expect: INSERT -->
- [ ] Dùng lệnh `WBLOCK` (hoặc `W`), xuất khối `TEST-CUA-900` ra một tệp DWG riêng biệt. <!-- expect: WBLOCK -->

## Nguồn tham khảo

```links
- title: "Khái niệm và cách tạo Block chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=BLOCK"
  kind: official
- title: "Lệnh WBLOCK xuất khối ra tệp tin độc lập từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=WBLOCK"
  kind: official
```
