---
id: ac-03-12
title: Thực hành tổng hợp chỉnh sửa chi tiết cơ khí 2D
category: Chỉnh sửa
tags: [tong-hop, chinh-sua, co-khi, tay-don, fillet, offset, trim, mirror]
level: beginner
minutes: 25
needs: [ac-03-04, ac-03-05, ac-03-06]
appVersions: ['2024', '2025']
edition: all
---
# Thực hành tổng hợp chỉnh sửa chi tiết cơ khí 2D

> **Mục tiêu:**
> - Kết hợp chuỗi các lệnh hiệu chỉnh cốt lõi: OFFSET, TRIM, FILLET, MIRROR để tạo hình chi tiết cơ khí phức tạp.
> - Xây dựng tư duy dựng hình nhanh: phác thảo hình cơ sở → dời hình song song → cắt tỉa nét thừa → bo tròn chuyển tiếp.
> - Hoàn thiện bản vẽ với hoa văn mặt cắt kim loại HATCH và kiểm tra độ chính xác hình học.

## Lệnh này làm gì và khi nào dùng

Trong thực tế sản xuất cơ khí, không có chi tiết máy nào được vẽ ngay từ đầu bằng các nét cong chuẩn xác. Thay vào đó, quy trình thiết kế chuyên nghiệp luôn tuân theo công thức:
1. Xác định các đường tim trục chuẩn và đường tròn cơ sở.
2. Dùng `OFFSET` để phóng các đường viền song song tạo độ dày thành vỏ.
3. Dùng `TRIM` và `EXTEND` để xén sạch các giao cắt thừa.
4. Dùng `FILLET` để bo tròn toàn bộ các góc lượn chuyển tiếp giảm ứng suất.
5. Dùng `MIRROR` để lật đối xứng nửa còn lại.
6. Dùng `HATCH` để tô mặt cắt thể hiện vật liệu kim loại.

Bài thực hành tổng hợp này sẽ hướng dẫn bạn chế tạo chi tiết **Tay đòn truyền động (Connecting Lever Arm)** - một chi tiết kinh điển đòi hỏi sự phối hợp mượt mà của toàn bộ các lệnh Chặng 03.

```hotspots
image: media/ac-03-12-tong-hop-part.svg
alt: Bản vẽ chi tiết tay đòn cơ khí 2D kết hợp các lệnh Fillet bo góc, Offset song song và Mirror đối xứng
layout: central
points:
  - id: part-boss-left
    x: 26
    y: 52
    title: Cụm đầu lớn (Head Boss)
    text: Gồm đường tròn ngoài R60 và lỗ trục trong đường kính Ø60 (R30).
    quiz: q-ac-03-012-1
  - id: part-fillet-neck
    x: 50
    y: 43
    title: Thân nối bo tròn (Fillet R40)
    text: Cung chuyển tiếp mượt mà giữa thân tay đòn và hai đầu trục bằng lệnh FILLET.
    quiz: q-ac-03-012-2
  - id: part-boss-right
    x: 74
    y: 52
    title: Cụm đầu nhỏ (Tail Boss)
    text: Gồm đường tròn ngoài R45 và lỗ trục trong đường kính Ø40 (R20), cách tâm đầu lớn 360mm.
```

## Cách dùng từng bước

1. **Vẽ đường tim trục tâm:**
   - Gõ `LINE`, bật [F8] (Ortho), vẽ một đường ngang dài 500mm làm trục đối xứng tâm nằm ngang.
2. **Dựng hai đầu trục (Boss):**
   - Bắt điểm Endpoint bên trái, gõ `CIRCLE` vẽ đường tròn bán kính `R60` và đường tròn đồng tâm `R30`.
   - Bật [F8], từ tâm đầu lớn rê chuột sang phải khoảng cách `360`mm, gõ `CIRCLE` vẽ đường tròn ngoài `R45` và đường tròn trong `R20`.
3. **Tạo thân tay đòn bằng OFFSET và LINE:**
   - Vẽ đường thẳng nối tiếp tuyến hoặc đường nối hai đỉnh góc phần tư trên của hai đường tròn lớn.
   - Gõ `OFFSET`, nhập cự ly `15`mm để tạo thành thân cần dày dặn.
4. **Cắt tỉa phần thừa bằng TRIM:**
   - Gõ `TRIM` (phím tắt `TR`), nhấp chuột xén bỏ các cung tròn nằm bên trong thân tay đòn để thông thoáng lòng chi tiết.
5. **Bo tròn góc chuyển tiếp bằng FILLET:**
   - Gõ `FILLET` (phím tắt `F`), gõ `R` nhập bán kính `40` rồi nhấn [Enter].
   - Nhấp chọn thân thẳng và đường tròn đầu lớn: Một cung bo R40 sẽ tự động sinh ra nối mượt hai phần.
   - Nhấn [Spacebar] lặp lại lệnh và bo tròn tiếp góc nối với đầu nhỏ.
6. **Lấy đối xứng nửa dưới bằng MIRROR:**
   - Gõ `MIRROR` (phím tắt `MI`), quét chọn toàn bộ phần thân trên và các cung bo vừa tạo.
   - Bấm 2 điểm mút của đường trục tim ngang làm trục đối xứng, nhấn [Enter] (No) để tạo nửa dưới đối xứng tuyệt đối.
7. **Tô mặt cắt kim loại:**
   - Gõ `HATCH`, chọn mẫu `ANSI31`.
   - Nhấp Pick Point vào thân tay đòn, kiểm tra thấy 2 lỗ trục tròn được chừa rỗng tự nhiên.
   - Nhấn [Enter] để hoàn thành bản vẽ.

## Tuỳ chọn và mẹo

> [!TIP]
> Thay vì vẽ cả hai bên trên và dưới, việc chỉ vẽ một nửa rồi dùng lệnh MIRROR không chỉ nhanh gấp đôi mà còn đảm bảo chi tiết không bao giờ bị lệch kích thước giữa hai phía.

> [!TIP]
> Luôn giữ các đường tim trục tâm (Centerline) trên một Layer riêng để sau này dễ dàng ẩn/hiện mà không làm mất hình dáng chi tiết.

## Tự kiểm tra

```quiz
id: q-ac-03-012-1
type: single
question: Trong quy trình dựng hình chi tiết tay đòn cơ khí đối xứng, bước nào dưới đây giúp tiết kiệm thời gian nhất?
options:
  - text: Chỉ cần vẽ hoàn chỉnh một nửa phía trên rồi dùng lệnh MIRROR lật đối xứng xuống dưới
    correct: true
    why: MIRROR đảm bảo đối xứng tuyệt đối và tiết kiệm 50% thời gian vẽ
  - text: Vẽ thủ công toàn bộ cả hai nửa trên và dưới bằng tay
    why: Vẽ hai lần dễ gây sai lệch kích thước và mất nhiều thời gian
  - text: Dùng lệnh SCALE để phóng to hình
    why: SCALE không tạo ra hình đối xứng
  - text: Dùng lệnh ROTATE xoay 180 độ
    why: Xoay sẽ đảo lộn đầu to đầu nhỏ thay vì đối xứng
explain: "Tận dụng tính chất đối xứng của các chi tiết cơ khí bằng lệnh MIRROR là phương pháp thiết kế tối ưu nhất: chỉ vẽ một nửa và lật sang nửa còn lại."
tags: [tong-hop, mirror, quy-trinh]
```

```quiz
id: q-ac-03-012-2
type: single
question: Để tạo góc lượn cong chuyển tiếp mềm mại giữa thân tay đòn và phần đầu trục tròn nhằm giảm ứng suất, bạn sử dụng lệnh nào?
options:
  - text: FILLET
    correct: true
    why: FILLET tạo cung tròn tiếp tuyến mượt mà giữa hai bề mặt giao nhau
  - text: CHAMFER
    why: CHAMFER tạo mặt vát phẳng nhọn chứ không tạo góc lượn cong
  - text: OFFSET
    why: OFFSET tạo đường song song
  - text: STRETCH
    why: STRETCH dùng để kéo giãn
explain: "Lệnh FILLET (phím tắt F) với bán kính R xác định là lệnh tiêu chuẩn để tạo các góc lượn bo tròn chuyển tiếp trong thiết kế chi tiết máy."
tags: [tong-hop, fillet, goc-luon]
```

```quiz
id: q-ac-03-012-3
type: truefalse
question: Sau khi đã xén tỉa xong bằng lệnh TRIM, bạn có thể dùng lệnh JOIN để gộp toàn bộ đường bao ngoài của tay đòn thành một đường Polyline duy nhất trước khi tô Hatch.
answer: true
explain: "Hợp nhất các đoạn rời rạc thành một đường Polyline khép kín bằng lệnh JOIN giúp việc quản lý đường bao và tô mặt cắt Hatch diễn ra nhanh chóng và không bao giờ bị lỗi hở biên."
tags: [tong-hop, join, pline]
```

```quiz
id: q-ac-03-012-4
type: hotspot
question: Bấm vào vị trí cung lượn chuyển tiếp Fillet R40 trên hình chi tiết.
use: hotspots
answer: part-fillet-neck
explain: "Cung lượn Fillet nằm ở phần cổ nối giữa thân tay đòn và đầu trục tròn."
tags: [tong-hop, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Bo tròn góc bằng FILLET xong nhưng đường tròn đầu lớn bị xén mất toàn bộ chu vi thành hình trăng khuyết.
  - *Nguyên nhân:* Chọn điểm nhấp chuột trên đường tròn ở vị trí đối diện (xa hơn điểm tiếp xúc mong muốn).
  - *Cách sửa:* Nhấn [Ctrl + Z], khi thực hiện lệnh FILLET hãy nhấp chuột vào phân đoạn gần với điểm giao cắt mong muốn nhất.
- **Triệu chứng:** Nửa dưới đối xứng qua MIRROR bị lệch méo không khớp với nửa trên.
  - *Nguyên nhân:* Đường tim trục ngang bị vẽ nghiêng một góc nhỏ do chưa bật phím [F8] Ortho.
  - *Cách sửa:* Bật [F8] và dựng lại đường tim ngang chuẩn xác trước khi Mirror.

## Bài tập thực hành

- [ ] Gõ `CIRCLE` vẽ đường tròn bán kính `60` tại toạ độ `0,0`. <!-- expect: CIRCLE -->
- [ ] Gõ `CIRCLE` vẽ đường tròn bán kính `45` tại toạ độ `360,0`. <!-- expect: CIRCLE -->
- [ ] Gõ `LINE` vẽ đường thẳng nối đỉnh góc phần tư trên của hai đường tròn. <!-- expect: LINE -->
- [ ] Gõ `FILLET`, gõ `R` nhập `40` rồi bo góc chuyển tiếp giữa đường thẳng và hai đường tròn. <!-- expect: FILLET -->
- [ ] Gõ `MIRROR`, quét chọn nửa trên và lấy đối xứng qua trục nối tâm để hoàn thành khung chi tiết. <!-- expect: MIRROR -->
- [ ] Gõ `HATCH`, chọn mẫu `ANSI31` và tô kín thân chi tiết vừa tạo. <!-- expect: HATCH -->

## Nguồn tham khảo

```links
- title: Phối hợp các lệnh hiệu chỉnh 2D nâng cao (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Modify+Objects
  kind: official
  lang: en
  note: Sách hướng dẫn chính thức về các phương pháp phối hợp lệnh hiệu chỉnh trong AutoCAD
- title: Tiêu chuẩn góc lượn và vát mép trong cơ khí (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Fillet+and+Chamfer
  kind: official
  lang: en
  note: Giải thích nguyên lý giảm nồng độ ứng suất bằng cung bo tròn Fillet
```
