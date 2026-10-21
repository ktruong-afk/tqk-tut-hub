---
id: ac-01-06
title: Các công cụ hỗ trợ vẽ chính xác (Ortho, Polar, Osnap, Otrack)
category: Làm quen
tags: [osnap, ortho, polar, otrack, chinh-xac]
level: beginner
minutes: 20
needs: [ac-01-05]
appVersions: ['2024', '2025']
edition: all
---
# Các công cụ hỗ trợ vẽ chính xác (Ortho, Polar, Osnap, Otrack)

> **Mục tiêu:**
> - Sử dụng chế độ Ortho (F8) và Polar Tracking (F10) để khống chế phương vẽ.
> - Cấu hình chế độ bắt điểm tự động Object Snap (F3) vào các vị trí hình học đặc trưng.
> - Kết hợp Object Snap Tracking (F11) để gióng điểm thẳng hàng không cần vẽ đường gióng phụ.

## Lệnh này làm gì và khi nào dùng

Vẽ kỹ thuật đòi hỏi sự chuẩn xác tới từng micromet. Bạn không bao giờ được phép "nhìn bằng mắt thường" rồi bấm đại một điểm gần đầu mút. Thay vào đó, AutoCAD trang bị các bộ công cụ trợ giúp vẽ chính xác:
- [[Chế độ Ortho]] (F8): Khoá chặt chuyển động con trỏ chuột theo hai phương ngang hoặc dọc.
- [[Chế độ Polar Tracking]] (F10): Dẫn hướng con trỏ bám theo các góc định trước (30°, 45°, 90°...).
- [[Điểm bắt]] (Object Snap - Osnap, F3): Hút con trỏ tự động và chính xác tuyệt đối vào các điểm đặc trưng hình học như đầu mút (Endpoint), trung điểm (Midpoint), tâm tròn (Center), giao điểm (Intersection).
- [[Object Snap Tracking]] (Otrack, F11): Kéo các tia gióng phụ ảo từ các điểm bắt điểm đã chọn.

Làm chủ 4 phím chức năng [F3], [F8], [F10], [F11] là nền tảng để vẽ nhanh và chuẩn xác trong mọi bản vẽ cơ khí, kiến trúc.

```hotspots
image: media/ac-01-06-osnap-hud.svg
alt: Sơ đồ các ký hiệu bắt điểm Osnap và các nút chức năng hỗ trợ vẽ trên thanh trạng thái
layout: central
points:
  - id: snap-endpoint
    x: 10
    y: 43
    title: Điểm đầu/cuối (Endpoint)
    text: Biểu tượng hình vuông màu xanh lá. Bắt chính xác vào điểm mút của đoạn thẳng, cung tròn hoặc đa tuyến.
    quiz: q-ac-01-06-1
  - id: snap-midpoint
    x: 30
    y: 41
    title: Trung điểm (Midpoint)
    text: Biểu tượng hình tam giác màu xanh lá. Bắt đúng điểm chia đôi chính giữa của bất kỳ đoạn thẳng hay cạnh nào.
  - id: snap-center
    x: 70
    y: 43
    title: Tâm đường tròn (Center)
    text: Biểu tượng hình tròn có dấu cộng. Bắt chuẩn xác tâm của đường tròn, cung tròn hoặc hình elip.
  - id: hud-buttons
    x: 50
    y: 84
    title: Các nút chức năng thanh trạng thái
    text: Dãy nút F8 (Ortho), F10 (Polar), F3 (Osnap), F11 (Otrack) cho phép bật tắt tức thời bằng phím bấm.
    quiz: q-ac-01-06-2
```

## Cách dùng từng bước

1. **Cấu hình bảng bắt điểm:** Gõ lệnh `OSNAP` (phím tắt `OS`) hoặc `DSETTINGS` (phím tắt `DS`), chuyển đến thẻ **Object Snap**.
2. **Chọn các điểm bắt điểm thông dụng:** Tích chọn 4 chế độ quan trọng nhất:
   - *Endpoint* (Điểm mút)
   - *Midpoint* (Trung điểm)
   - *Center* (Tâm tròn)
   - *Intersection* (Giao điểm)
   - *Extension* hoặc *Perpendicular* (Vuông góc)
3. **Bật/Tắt nhanh khi đang vẽ:**
   - Nhấn [F3] để bật/tắt toàn bộ tính năng Osnap.
   - Nhấn [F8] để khoá phương vuông góc khi vẽ tường hoặc trục thẳng.
   - Nhấn [F10] khi cần vẽ đường chéo theo góc bội số của 30° hoặc 45°.
4. **Sử dụng Otrack (F11) gióng điểm:** Rê chuột lướt nhẹ qua một Endpoint để xuất hiện dấu cộng nhỏ, sau đó rê chuột ra xa. Một đường gióng nét đứt màu xanh sẽ tự động xuất hiện để bạn bấm điểm thẳng hàng mà không cần vẽ đường phụ.

## Tuỳ chọn và mẹo

> [!TIP]
> Không nên tích chọn nút *Select All* trong bảng cài đặt Osnap vì sẽ gây loạn điểm bắt khi bản vẽ dày đặc đối tượng. Hãy chỉ bật những chế độ bạn thường xuyên dùng.

> [!TIP]
> Khi cần bắt tạm thời một điểm đặc biệt (như tiếp tuyến Tangent), hãy đè giữ phím [Shift] rồi nhấp chuột phải để mở menu Osnap Override dùng một lần.

## Tự kiểm tra

```quiz
id: q-ac-01-06-1
type: single
question: Biểu tượng hình học nào đại diện cho chế độ bắt điểm trung điểm (Midpoint) trong AutoCAD?
options:
  - { text: Hình tam giác, correct: true, why: Ký hiệu của Midpoint là hình tam giác màu xanh lá }
  - { text: Hình vuông, why: Hình vuông là ký hiệu của Endpoint }
  - { text: Hình tròn, why: Hình tròn là ký hiệu của Center }
  - { text: Dấu X chéo, why: Dấu X là ký hiệu của Intersection }
explain: "Trong AutoCAD, mỗi điểm bắt có một biểu tượng đồ hoạ riêng biệt (AutoSnap Marker) để người vẽ nhận diện tức thì: hình vuông là Endpoint, hình tam giác là Midpoint."
tags: [osnap, midpoint]
```

```quiz
id: q-ac-01-06-2
type: single
question: Phím chức năng nào dùng để bật hoặc tắt chế độ bắt điểm tự động (Object Snap)?
options:
  - { text: F3, correct: true, why: Phím F3 là phím bật tắt Osnap tiêu chuẩn }
  - { text: F8, why: F8 dùng cho Ortho }
  - { text: F7, why: F7 dùng cho Grid }
  - { text: F12, why: F12 dùng cho Dynamic Input }
explain: Phím [F3] bật hoặc tắt trạng thái hoạt động của Object Snap. Khi bật, biểu tượng trên thanh trạng thái chuyển sang màu sáng.
tags: [osnap, phim-tat]
```

```quiz
id: q-ac-01-06-3
type: truefalse
question: Chế độ Ortho (F8) và Polar Tracking (F10) có thể hoạt động đồng thời cùng một lúc.
answer: false
explain: Ortho và Polar Tracking loại trừ lẫn nhau. Khi bạn bật Ortho, Polar Tracking sẽ tự động tắt và ngược lại.
tags: [ortho, polar]
```

```quiz
id: q-ac-01-06-4
type: hotspot
question: Bấm vào vị trí của biểu tượng Endpoint trên hình vẽ.
use: hotspots
answer: snap-endpoint
explain: Endpoint nằm ở điểm mút của đoạn thẳng, được đánh dấu bằng khung hình vuông xanh lá.
tags: [osnap, endpoint]
```

## Lỗi thường gặp

- **Triệu chứng:** Rê chuột vào gần đường thẳng nhưng không thấy hiện khung xanh bắt điểm.
  - *Nguyên nhân:* Tính năng Osnap đang bị tắt hoặc loại điểm đó chưa được tích chọn trong cài đặt.
  - *Cách sửa:* Nhấn phím [F3] để bật Osnap; nếu vẫn chưa thấy, gõ `OSNAP` và kiểm tra xem đã tích ô *Endpoint* hay chưa.
- **Triệu chứng:** Không thể vẽ đường chéo tự do, con trỏ chuột luôn bị giật giật sang ngang hoặc đứng.
  - *Nguyên nhân:* Chế độ khoá phương vuông góc Ortho ([F8]) đang vô tình bật.
  - *Cách sửa:* Nhấn phím [F8] để tắt Ortho và vẽ tự do mọi góc độ.

## Bài tập thực hành

- [ ] Gõ `OSNAP` mở hộp thoại Drafting Settings và kích hoạt các chế độ Endpoint, Midpoint, Center. <!-- expect: OSNAP -->
- [ ] Nhấn [F8] để bật chế độ Ortho, sau đó gõ `LINE` vẽ một đoạn thẳng ngang dài 150mm. <!-- expect: LINE -->
- [ ] Bật [F3] và rê chuột tìm ký hiệu tam giác Midpoint tại điểm giữa của đoạn thẳng vừa vẽ.
- [ ] Từ trung điểm đó, vẽ một đường thẳng đứng vuông góc lên trên 80mm. <!-- expect: LINE -->
- [ ] Nhấn [F8] để tắt Ortho, sau đó nối một đường chéo khép kín về Endpoint ban đầu. <!-- expect: LINE -->

## Nguồn tham khảo

```links
- title: Bắt điểm đối tượng Object Snap (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Object+Snaps
  kind: official
  lang: en
  note: Danh sách đầy đủ các điểm bắt điểm hình học và phím tắt trong AutoCAD
- title: Hỗ trợ gióng điểm với Polar Tracking và Otrack (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Polar+Tracking
  kind: official
  lang: en
  note: Hướng dẫn thiết lập bước góc và các tia gióng phụ ảo
```
