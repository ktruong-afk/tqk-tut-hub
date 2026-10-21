---
id: ac-03-04
title: Lấy đối xứng với MIRROR và tạo song song với OFFSET
category: Chỉnh sửa
tags: [mirror, offset, doi-xung, song-song, dong-tam]
level: beginner
minutes: 15
needs: [ac-03-02]
appVersions: ['2024', '2025']
edition: all
---
# Lấy đối xứng với MIRROR và tạo song song với OFFSET

> **Mục tiêu:**
> - Sử dụng lệnh MIRROR để nhân bản các chi tiết đối xứng qua một trục thẳng xác định.
> - Sử dụng lệnh OFFSET để tạo các đường song song hoặc các đường tròn đồng tâm với cự ly chính xác.
> - Kiểm soát tuỳ chọn xoá hay giữ hình gốc (Erase source objects) và chế độ MIRRTEXT với chữ ghi chú.

## Lệnh này làm gì và khi nào dùng

Trong bản vẽ kỹ thuật, tính đối xứng và sự đồng dạng song song xuất hiện ở hầu hết mọi công trình: trục xe, khung cửa, tường bao, cánh bướm, rãnh then... Thay vì vẽ thủ công cả hai bên, bạn chỉ cần vẽ một nửa và dùng hai lệnh sau:
- `MIRROR` (phím tắt `MI`): Tạo bản sao [[Đối xứng]] hoàn hảo của đối tượng qua một trục thẳng (Mirror Line) được định nghĩa bởi 2 điểm.
- `OFFSET` (phím tắt `O`): Tạo ra một đối tượng mới có hình dáng hoàn toàn tương đồng, chạy song song với đối tượng gốc (hoặc đồng tâm nếu là đường tròn) ở một khoảng cách cố định.

Hai lệnh này là "vũ khí tăng tốc" giúp giảm hơn 50% thời gian vẽ phác thảo.

```hotspots
image: media/ac-03-04-mirror-offset.svg
alt: Minh hoạ phép lấy đối xứng qua trục của lệnh MIRROR và tạo đường song song đồng tâm của lệnh OFFSET
layout: central
points:
  - id: mirror-axis
    x: 25
    y: 35
    title: Lệnh MIRROR (Đối xứng qua trục)
    text: Trục đối xứng được xác định bởi 2 điểm mốc. Bản sao được lật ngược sang phía đối diện.
    quiz: q-ac-03-04-1
  - id: offset-distance
    x: 75
    y: 35
    title: Lệnh OFFSET (Song song & Đồng tâm)
    text: Nhập khoảng cách d, bấm chọn đường gốc rồi nhấp về phía cần tạo đối tượng song song.
    quiz: q-ac-03-04-2
```

## Cách dùng từng bước

1. **Lấy đối xứng qua trục (MIRROR):**
   - Gõ `MIRROR` hoặc phím tắt `MI` rồi nhấn [Enter].
   - Nhấp chọn các đối tượng cần lấy đối xứng rồi nhấn [Enter].
   - Chọn điểm thứ nhất của trục đối xứng (First point of mirror line).
   - Bật [F8] (Ortho), nhấp điểm thứ hai của trục đối xứng.
   - Trả lời câu hỏi: `Erase source objects? [Yes/No] <N>:`
     - Nhấn [Enter] (hoặc gõ `N`): Giữ lại hình gốc ban đầu (tạo thành hình hoàn chỉnh 2 bên).
     - Gõ `Y`: Xoá hình gốc, chỉ giữ lại hình lật ngược.
2. **Tạo đối tượng song song (OFFSET):**
   - Gõ `OFFSET` hoặc phím tắt `O` rồi nhấn [Enter].
   - Nhập khoảng cách song song mong muốn (Specify offset distance, ví dụ `20`) rồi [Enter].
   - Nhấp chuột chọn đối tượng cần offset.
   - Nhấp chuột sang bên trái, bên phải, bên trong hoặc bên ngoài để chỉ định hướng tạo đối tượng mới.
   - Tiếp tục nhấp chọn các đối tượng khác nếu cần, hoặc nhấn [Enter] để kết thúc.

## Tuỳ chọn và mẹo

> [!TIP]
> Biến hệ thống `MIRRTEXT`: Mặc định bằng 0. Khi bằng 0, nếu bạn quét chọn cả chữ văn bản đem lấy đối xứng bằng MIRROR, nội dung chữ vẫn giữ nguyên chiều đọc từ trái sang phải mà không bị lộn ngược chữ trong gương.

> [!TIP]
> Trong lệnh OFFSET, bạn có thể gõ tuỳ chọn `T` (Through) để tạo đường song song đi xuyên qua một điểm bắt điểm xác định thay vì phải đo trước khoảng cách.

## Tự kiểm tra

```quiz
id: q-ac-03-04-1
type: single
question: Để xác định trục đối xứng trong lệnh MIRROR, bạn cần nhấp chọn bao nhiêu điểm trên bản vẽ?
options:
  - text: 2 điểm (tạo thành một đường thẳng trục đối xứng)
    correct: true
    why: 2 điểm xác định duy nhất một đường thẳng làm trục đối xứng trong không gian
  - text: 1 điểm (tâm đối xứng)
    why: MIRROR trong CAD là đối xứng qua trục thẳng chứ không phải đối xứng qua tâm
  - text: 3 điểm
    why: 3 điểm dùng cho cung tròn
  - text: Không cần bấm điểm nào
    why: Phải xác định trục thì AutoCAD mới biết lật về hướng nào
explain: "Trục đối xứng trong lệnh MIRROR được định nghĩa bởi hai điểm mốc (First point và Second point of mirror line)."
tags: [mirror, truc-doi-xung]
```

```quiz
id: q-ac-03-04-2
type: single
question: Khi dùng lệnh OFFSET lên một đường tròn có bán kính R=50 với khoảng cách d=15 và bấm chuột ra phía ngoài, kết quả là gì?
options:
  - text: Một đường tròn đồng tâm mới có bán kính R=65
    correct: true
    why: "Bấm ra ngoài sẽ cộng thêm khoảng cách offset: 50 + 15 = 65"
  - text: Một đường tròn đồng tâm mới có bán kính R=35
    why: R=35 là kết quả khi bấm chuột vào bên trong
  - text: Một đường thẳng tiếp tuyến với đường tròn
    why: OFFSET đường tròn luôn sinh ra đường tròn đồng tâm
  - text: Một hình elip
    why: OFFSET đường tròn không tạo ra hình elip
explain: "Lệnh OFFSET áp dụng lên đường tròn sẽ luôn tạo ra đường tròn đồng tâm: bấm ra ngoài thì bán kính tăng thêm d (50 + 15 = 65), bấm vào trong thì bán kính giảm đi d."
tags: [offset, duong-tron, ban-kinh]
```

```quiz
id: q-ac-03-04-3
type: truefalse
question: Khi biến MIRRTEXT đặt giá trị bằng 0, văn bản chữ khi lấy đối xứng bằng lệnh MIRROR sẽ không bị lộn ngược chữ.
answer: true
explain: "Biến MIRRTEXT = 0 giữ nguyên chiều đọc bình thường của chữ văn bản kỹ thuật khi thực hiện lệnh MIRROR, tránh gây khó đọc bản vẽ."
tags: [mirror, mirrtext]
```

```quiz
id: q-ac-03-04-4
type: hotspot
question: Bấm vào vị trí minh hoạ trục đối xứng Mirror Line trên hình vẽ.
use: hotspots
answer: mirror-axis
explain: "Trục đối xứng nằm ở giữa bên trái, thể hiện bằng đường nét gạch chấm màu đỏ có 2 điểm mốc."
tags: [mirror, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Khi lấy đối xứng một nửa bản vẽ, nửa mới bị nghiêng chéo không khớp vào đường tim.
  - *Nguyên nhân:* Khi bấm điểm thứ hai của trục đối xứng chưa bật phím [F8] (Ortho), làm trục đối xứng bị xiên một góc nhỏ.
  - *Cách sửa:* Luôn bật chế độ Ortho ([F8]) khi xác định trục đối xứng thẳng đứng hoặc nằm ngang.
- **Triệu chứng:** Lệnh OFFSET không chịu nhận đường bao kín mà báo lỗi *"Cannot offset that object"*.
  - *Nguyên nhân:* Khoảng cách offset đặt quá lớn so với bán kính góc lượn trong của hình khiến hình học bị giao nhau tự triệt tiêu.
  - *Cách sửa:* Giảm khoảng cách offset nhỏ hơn bán kính góc bo trong nhỏ nhất.

## Bài tập thực hành

- [ ] Gõ `LINE` vẽ một nửa hình cánh bướm bên trái với 3 đoạn gấp khúc. <!-- expect: LINE -->
- [ ] Gõ `MIRROR`, quét chọn 3 đoạn thẳng vừa vẽ. <!-- expect: MIRROR -->
- [ ] Bấm 2 điểm mút của trục đứng giữa, nhấn [Enter] (No) để tạo nửa đối xứng bên phải.
- [ ] Gõ `CIRCLE` vẽ một đường tròn bán kính `40` tại tâm toạ độ. <!-- expect: CIRCLE -->
- [ ] Gõ `OFFSET`, nhập khoảng cách `10`, nhấp chọn đường tròn rồi bấm ra phía ngoài để tạo đường tròn đồng tâm R50. <!-- expect: OFFSET -->

## Nguồn tham khảo

```links
- title: Lệnh MIRROR và quản lý đối xứng (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=MIRROR+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về lật đối xứng và cấu hình biến hệ thống MIRRTEXT
- title: Lệnh OFFSET tạo đường song song (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=OFFSET+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn Distance, Through, Erase, Layer của lệnh OFFSET
```
