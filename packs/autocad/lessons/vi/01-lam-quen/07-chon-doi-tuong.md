---
id: ac-01-07
title: Các phương pháp chọn đối tượng và thao tác với Grips
category: Làm quen
tags: [selection, window, crossing, qselect, grips]
level: beginner
minutes: 15
needs: [ac-01-06]
appVersions: ['2024', '2025']
edition: all
---
# Các phương pháp chọn đối tượng và thao tác với Grips

> **Mục tiêu:**
> - Phân biệt phương pháp chọn Window Selection (xanh dương) và Crossing Selection (xanh lá).
> - Sử dụng tính năng chọn lọc đối tượng nâng cao Quick Select (QSELECT).
> - Thao tác kéo giãn, di chuyển hoặc thay đổi kích thước nhanh bằng các điểm kẹp Grips.

## Lệnh này làm gì và khi nào dùng

Trước khi chỉnh sửa, sao chép hoặc xoá bất kỳ hình học nào, bạn phải chọn (select) chúng. Chọn sai đối tượng sẽ dẫn đến sửa nhầm bản vẽ. AutoCAD cung cấp hai chế độ chọn quét chuột kinh điển:
- [[Hộp chọn bao quanh]] (Window Selection): Quét chuột từ **Trái sang Phải** (vùng màu xanh dương viền nét liền). Chỉ những đối tượng nằm trọn vẹn 100% bên trong khung mới được chọn.
- [[Hộp chọn cắt qua]] (Crossing Selection): Quét chuột từ **Phải sang Trái** (vùng màu xanh lá viền nét đứt). Bất kỳ đối tượng nào nằm bên trong HOẶC chỉ cần bị đường biên cắt qua đều được chọn.

Bên cạnh đó, khi nhấp trực tiếp vào đối tượng lúc không có lệnh nào chạy, các ô vuông nhỏ màu xanh gọi là [[Điểm kẹp]] (Grips) sẽ xuất hiện, cho phép bạn kéo giãn hoặc chỉnh sửa hình học tức thời.

```hotspots
image: media/ac-01-07-selection.svg
alt: So sánh trực quan giữa hộp chọn Window Selection từ trái qua phải và Crossing Selection từ phải qua trái
layout: central
points:
  - id: window-left-to-right
    x: 25
    y: 40
    title: Window Selection (Trái → Phải)
    text: Khung màu xanh dương nét liền. Chỉ chọn những vật thể nằm lọt hoàn toàn bên trong khung chọn.
    quiz: q-ac-01-07-1
  - id: crossing-right-to-left
    x: 75
    y: 40
    title: Crossing Selection (Phải → Trái)
    text: Khung màu xanh lá nét đứt. Chọn mọi vật thể nằm trong hoặc chạm cắt qua đường biên của khung.
    quiz: q-ac-01-07-2
```

## Cách dùng từng bước

1. **Chọn từng đối tượng:** Nhấp chuột trái trực tiếp lên đường thẳng hoặc hình học cần chọn.
2. **Chọn vùng Window (Trái sang Phải):**
   - Nhấp chuột trái một lần vào vùng trống bên trái đối tượng rồi thả tay ra (không đè giữ chuột).
   - Di chuyển chuột sang bên phải để mở khung chữ nhật màu xanh dương.
   - Nhấp chuột trái lần thứ hai để xác nhận chọn.
3. **Chọn vùng Crossing (Phải sang Trái):**
   - Nhấp chuột trái một lần vào vùng trống bên phải đối tượng rồi thả tay ra.
   - Di chuyển chuột sang bên trái để mở khung chữ nhật màu xanh lá nét đứt.
   - Nhấp chuột trái lần thứ hai để xác nhận.
4. **Bỏ bớt đối tượng đã chọn:** Đè giữ phím [Shift] trên bàn phím và nhấp vào đối tượng muốn loại khỏi vùng chọn.
5. **Huỷ bỏ toàn bộ vùng chọn:** Nhấn phím [Esc] trên bàn phím.
6. **Lọc chọn hàng loạt bằng QSELECT:** Gõ lệnh `QSELECT` (hoặc `QSE`), chọn kiểu đối tượng (Object type) và thuộc tính (Color, Layer, Line weight) để tự động gom toàn bộ đối tượng thoả mãn.

## Tuỳ chọn và mẹo

> [!TIP]
> Trong AutoCAD, hãy thực hiện thao tác nhấp-thả chuột thay vì đè giữ chuột để mở khung chọn chữ nhật. Đè giữ chuột sẽ kích hoạt chế độ chọn tự do Lasso Selection khó kiểm soát hơn.

> [!TIP]
> Nhấp vào một điểm kẹp (Grip) màu xanh để biến nó thành màu đỏ (Hot Grip). Lúc này bạn có thể di chuyển con trỏ chuột để kéo giãn hình học trực tiếp mà không cần gõ lệnh.

## Tự kiểm tra

```quiz
id: q-ac-01-07-1
type: single
question: Khi quét chuột từ Trái sang Phải (Window Selection - khung màu xanh dương), đối tượng nào sẽ được chọn?
options:
  - { text: Chỉ các đối tượng nằm trọn vẹn bên trong khung, correct: true, why: Window Selection yêu cầu đối tượng phải nằm 100% bên trong khung }
  - { text: Mọi đối tượng chạm vào đường biên, why: Đó là cơ chế của Crossing Selection }
  - { text: Tất cả các đối tượng trong bản vẽ, why: Muốn chọn tất cả phải nhấn Ctrl + A }
  - { text: Chỉ các đối tượng có màu xanh, why: Màu khung chọn không phụ thuộc màu của đối tượng }
explain: Khung màu xanh dương (quét Trái sang Phải) chỉ chọn những đối tượng nằm hoàn toàn 100% bên trong khung, rất hữu ích khi muốn lọc bỏ các đường bao bên ngoài.
tags: [selection, window]
```

```quiz
id: q-ac-01-07-2
type: single
question: Khung chọn nào có viền nét đứt và nền màu xanh lá cây?
options:
  - { text: Crossing Selection (quét từ Phải sang Trái), correct: true, why: Crossing Selection có nền xanh lá viền đứt }
  - { text: Window Selection (quét từ Trái sang Phải), why: Window Selection có nền xanh dương viền liền }
  - { text: Fence Selection, why: Fence là đường chọn ziczac }
  - { text: Lasso Selection, why: Lasso là vẽ vùng tự do }
explain: Crossing Selection xuất hiện khi bạn nhấp chuột và kéo từ phải sang trái, có đặc điểm nhận diện là viền nét đứt màu xanh lá cây.
tags: [selection, crossing]
```

```quiz
id: q-ac-01-07-3
type: truefalse
question: Muốn loại bỏ một đối tượng ra khỏi danh sách đang chọn mà không phải chọn lại từ đầu, bạn đè giữ phím [Shift] và nhấp vào đối tượng đó.
answer: true
explain: Phím [Shift] là phím đảo ngược chọn đối tượng trong AutoCAD. Đè giữ Shift và bấm vào đối tượng đang chọn sẽ bỏ chọn nó.
tags: [selection, shift]
```

```quiz
id: q-ac-01-07-4
type: hotspot
question: Bấm vào vị trí minh hoạ Crossing Selection (quét từ Phải sang Trái) trên hình.
use: hotspots
answer: crossing-right-to-left
explain: Crossing Selection nằm ở nửa bên phải của sơ đồ, có khung viền nét đứt màu xanh lá cây.
tags: [selection, crossing]
```

## Lỗi thường gặp

- **Triệu chứng:** Khi quét chuột xuất hiện đường cong tự do ngoằn ngoèo thay vì khung hình chữ nhật.
  - *Nguyên nhân:* Bạn đang nhấn đè giữ chuột trái khi di chuyển (chế độ chọn Lasso Selection).
  - *Cách sửa:* Chỉ nhấp chuột một lần rồi thả tay, di chuyển chuột đến góc đối diện rồi nhấp lần thứ hai.
- **Triệu chứng:** Quét chuột qua đối tượng nhưng không thấy đối tượng được chọn.
  - *Nguyên nhân:* Đang quét theo chế độ Window (Trái sang Phải) mà đối tượng lại thò một phần ra ngoài khung.
  - *Cách sửa:* Quét từ Phải sang Trái (Crossing) hoặc mở rộng khung bao trọn toàn bộ hình học.

## Bài tập thực hành

- [ ] Gõ `LINE` và vẽ liên tiếp 3 đoạn thẳng song song cách nhau trên vùng vẽ. <!-- expect: LINE -->
- [ ] Dùng phương pháp quét chuột từ Trái sang Phải (Window) bao trọn 1 đoạn thẳng ở giữa để chọn riêng đoạn thẳng đó.
- [ ] Nhấn phím [Esc] để bỏ chọn.
- [ ] Dùng phương pháp quét từ Phải sang Trái (Crossing) cắt ngang qua cả 3 đoạn thẳng để chọn toàn bộ.
- [ ] Gõ lệnh `ERASE` và nhấn [Enter] để xoá sạch các đoạn thẳng vừa chọn. <!-- expect: ERASE -->

## Nguồn tham khảo

```links
- title: Các phương pháp chọn đối tượng trong AutoCAD (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=To+Select+Objects
  kind: official
  lang: en
  note: Hướng dẫn chi tiết Window, Crossing, Fence, QSELECT và các chế độ chọn nâng cao
- title: Thao tác với điểm kẹp Grips (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Grip+Editing
  kind: official
  lang: en
  note: Các chế độ Stretch, Move, Rotate, Scale thông qua điểm kẹp Hot Grips
```
