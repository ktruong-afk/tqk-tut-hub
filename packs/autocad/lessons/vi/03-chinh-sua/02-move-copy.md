---
id: ac-03-02
title: Di chuyển với MOVE và nhân bản với COPY
category: Chỉnh sửa
tags: [move, copy, chinh-sua, base-point, nhan-ban]
level: beginner
minutes: 15
needs: [ac-03-01]
appVersions: ['2024', '2025']
edition: all
---
# Di chuyển với MOVE và nhân bản với COPY

> **Mục tiêu:**
> - Sử dụng lệnh MOVE để di dời đối tượng từ vị trí này sang vị trí khác chuẩn xác theo điểm chuẩn (Base Point).
> - Sử dụng lệnh COPY để nhân bản đối tượng thành nhiều bản sao độc lập với cự ly xác định.
> - Kết hợp chế độ bắt điểm Osnap và toạ độ tương đối khi thực hiện phép tịnh tiến.

## Lệnh này làm gì và khi nào dùng

Hai thao tác phổ biến nhất trong mọi phần mềm đồ hoạ là di chuyển và sao chép:
- `MOVE` (phím tắt `M`): Dời đối tượng gốc từ vị trí hiện tại đến vị trí mới. Đối tượng tại vị trí cũ sẽ biến mất.
- `COPY` (phím tắt `CO` hoặc `CP`): Tạo ra một hoặc nhiều bản sao mới giống hệt đối tượng ban đầu tại các vị trí chỉ định. Đối tượng gốc được giữ nguyên vẹn.

Cả hai lệnh đều hoạt động dựa trên nguyên lý véc-tơ dời hình gồm 2 điểm:
1. [[Điểm chuẩn]] (Base Point): Điểm gốc bạn chọn làm tay nắm để nhấc vật thể lên.
2. Điểm đến (Second Point of displacement): Vị trí bạn đặt tay nắm xuống.

```hotspots
image: media/ac-03-02-move-copy.svg
alt: So sánh trực quan cơ chế dời hình của lệnh MOVE và nhân bản của lệnh COPY
layout: central
points:
  - id: move-displacement
    x: 25
    y: 35
    title: Lệnh MOVE (Di chuyển)
    text: Vật thể gốc tại vị trí cũ biến mất và xuất hiện tại vị trí Second Point mới.
    quiz: q-ac-03-02-1
  - id: copy-multiple
    x: 75
    y: 35
    title: Lệnh COPY (Sao chép)
    text: Vật thể gốc được giữ nguyên vẹn. Cho phép nhấp chuột tạo liên tiếp nhiều bản sao mới.
    quiz: q-ac-03-02-2
```

## Cách dùng từng bước

1. **Di chuyển đối tượng (MOVE):**
   - Gõ `MOVE` hoặc phím tắt `M` rồi nhấn [Enter].
   - Nhấp chọn các đối tượng cần di chuyển, sau đó nhấn [Enter] để kết thúc bước chọn.
   - Chọn điểm chuẩn (Specify base point): Dùng Osnap nhấp vào một điểm mút, tâm tròn hoặc góc của vật thể.
   - Chọn điểm đến (Specify second point):
     - Cách 1: Dùng Osnap bấm vào vị trí đích trên bản vẽ.
     - Cách 2: Bật [F8], rê chuột theo hướng mong muốn, gõ khoảng cách (ví dụ `150`) rồi nhấn [Enter].
2. **Sao chép đối tượng (COPY):**
   - Gõ `COPY` hoặc phím tắt `CO` rồi nhấn [Enter].
   - Chọn đối tượng cần nhân bản, sau đó nhấn [Enter].
   - Chọn điểm chuẩn (Base point).
   - Nhấp liên tiếp vào các vị trí mới để thả các bản sao.
   - Nhấn phím [Esc] hoặc [Enter] để kết thúc lệnh Copy.

## Tuỳ chọn và mẹo

> [!TIP]
> Luôn chọn Base Point là một điểm đặc trưng hình học có sẵn trên vật thể (như Endpoint góc hộp hoặc Center tâm lỗ) để dễ dàng ráp nối khớp vào vị trí đích mà không bị lệch.

> [!TIP]
> Trong lệnh COPY, bạn có thể gõ tuỳ chọn `A` (Array) để sao chép thẳng hàng một dãy nhiều đối tượng cách đều nhau cùng một lúc.

## Tự kiểm tra

```quiz
id: q-ac-03-02-1
type: single
question: Trong lệnh MOVE hoặc COPY, khái niệm "Base Point" (Điểm chuẩn) có ý nghĩa gì?
options:
  - text: Điểm mốc gốc dùng để tính khoảng cách và hướng di dời vật thể
    correct: true
    why: Base Point là điểm xuất phát của véc-tơ tịnh tiến
  - text: Điểm gốc toạ độ tuyệt đối (0,0) của bản vẽ
    why: Base Point có thể là bất kỳ điểm nào trên màn hình
  - text: Điểm tâm của màn hình máy tính
    why: Base Point không phụ thuộc vào tâm màn hình
  - text: Điểm bắt buộc phải nằm ngoài đối tượng
    why: Base Point thường nằm ngay trên đối tượng để dễ bắt điểm
explain: "Base Point (Điểm chuẩn) là điểm gốc quy chiếu, khoảng cách và phương hướng dịch chuyển của vật thể sẽ được tính từ Base Point đến Second Point."
tags: [move, copy, base-point]
```

```quiz
id: q-ac-03-02-2
type: single
question: Phím tắt chuẩn nào dưới đây dùng để kích hoạt lệnh COPY trong AutoCAD?
options:
  - text: CO hoặc CP
    correct: true
    why: Cả CO và CP đều là phím tắt mặc định của lệnh COPY
  - text: C
    why: C là phím tắt của lệnh vẽ đường tròn CIRCLE
  - text: Ctrl + C
    why: Ctrl + C là sao chép vào bộ nhớ đệm Windows
  - text: CC
    why: CC không phải phím tắt lệnh AutoCAD
explain: "Trong AutoCAD, phím C đại diện cho lệnh CIRCLE, do đó lệnh COPY có phím tắt là CO hoặc CP."
tags: [copy, phim-tat]
```

```quiz
id: q-ac-03-02-3
type: truefalse
question: Sau khi thực hiện lệnh COPY một lần, bạn có thể bấm chuột nhiều lần liên tiếp để tạo ra hàng loạt bản sao mà không cần gọi lại lệnh.
answer: true
explain: "Lệnh COPY trong AutoCAD hiện đại mặc định ở chế độ Multiple (đa bản sao), cho phép bạn nhấp chuột liên tục để rải bản sao ra khắp bản vẽ."
tags: [copy, multiple]
```

```quiz
id: q-ac-03-02-4
type: hotspot
question: Bấm vào sơ đồ minh hoạ lệnh COPY trên hình vẽ.
use: hotspots
answer: copy-multiple
explain: "Sơ đồ lệnh COPY nằm ở nửa bên phải, thể hiện vật thể gốc được giữ nguyên và tạo thêm bản sao mới."
tags: [copy, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Gõ chữ `C` với ý định sao chép nhưng AutoCAD lại bật lệnh vẽ đường tròn CIRCLE.
  - *Nguyên nhân:* Nhầm lẫn phím tắt (phím tắt của COPY là `CO` hoặc `CP`, còn `C` là CIRCLE).
  - *Cách sửa:* Gõ `CO` [Enter] khi muốn sao chép đối tượng.
- **Triệu chứng:** Đối tượng sau khi Move bị lệch một khoảng nhỏ so với vị trí cần ráp nối.
  - *Nguyên nhân:* Chọn Base Point tự do giữa khoảng không thay vì dùng Osnap bắt đúng vào góc mút của đối tượng.
  - *Cách sửa:* Bật Osnap [F3] và luôn bấm Base Point tại góc hoặc tâm của đối tượng.

## Bài tập thực hành

- [ ] Gõ `RECTANG` vẽ một hình chữ nhật kích thước `@80,50`. <!-- expect: RECTANG -->
- [ ] Gõ `MOVE`, chọn hình chữ nhật, bắt Base Point tại góc dưới bên trái. <!-- expect: MOVE -->
- [ ] Bật [F8], kéo sang phải và gõ khoảng cách `120` rồi nhấn [Enter] để di chuyển.
- [ ] Gõ `COPY`, chọn hình chữ nhật vừa dời. <!-- expect: COPY -->
- [ ] Bắt Base Point tại tâm hình, kéo chuột sang phải và sao chép ra thêm 2 bản sao cách nhau `100`mm.

## Nguồn tham khảo

```links
- title: Lệnh MOVE di chuyển đối tượng (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=MOVE+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về thao tác dời hình và nhập toạ độ dịch chuyển
- title: Lệnh COPY và tuỳ chọn sao chép mảng Array (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=COPY+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn Displacement, Mode, Multiple của lệnh COPY
```
