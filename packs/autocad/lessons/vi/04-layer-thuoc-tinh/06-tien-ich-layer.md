---
id: ac-04-06
title: Các lệnh tiện ích thao tác Layer nhanh (LAYISO, LAYFRZ, LAYMRG)
category: Layer & Thuộc tính
tags: [layiso, layuniso, layfrz, laythw, layoff, layon, laymrg, tien-ich-layer]
level: beginner
minutes: 15
needs: [ac-04-01]
appVersions: ['2024', '2025']
edition: all
---
# Các lệnh tiện ích thao tác Layer nhanh (LAYISO, LAYFRZ, LAYMRG)

> **Mục tiêu:**
> - Sử dụng lệnh LAYISO để cô lập layer chỉ bằng một cú nhấp chuột lên đối tượng và phục hồi bằng LAYUNISO.
> - Tắt nhanh hiển thị với LAYOFF (bật lại bằng LAYON) và đóng băng với LAYFRZ (làm tan bằng LAYTHW).
> - Sử dụng lệnh LAYMRG để dọn dẹp, gộp các layer rác vào một layer chuẩn và tự động xoá layer thừa.

## Lệnh này làm gì và khi nào dùng

Mỗi lần muốn tắt một layer hay muốn kiểm tra xem một nét vẽ thuộc layer nào, nếu cứ phải mở bảng Layer Properties Manager rồi cuộn chuột tìm kiếm thì sẽ tốn rất nhiều thời gian.

AutoCAD trang bị một bộ công cụ "tiện ích Layer trực tiếp" (Layer Utilities) trên thanh Ribbon (*Home > Layers panel*), cho phép bạn thao tác bằng cách **nhấp thẳng vào đối tượng trên màn hình**:
- `LAYISO` ([[Cô lập lớp]]): Bạn nhấp vào một nét thấy, toàn bộ các layer khác (kích thước, chữ, nét khuất) sẽ tự động bị ẩn hoặc khoá mờ đi! Bạn có thể thoải mái chọn, xoá hoặc chỉnh sửa riêng nét thấy mà không sợ chạm nhầm vào các đối tượng khác. Khôi phục lại bằng lệnh `LAYUNISO`.
- `LAYOFF` / `LAYON`: Nhấp chuột vào đối tượng nào thì layer của đối tượng đó tự tắt bóng đèn. Muốn bật lại tất cả, chỉ cần gõ `LAYON`.
- `LAYFRZ` / `LAYTHW`: [[Đóng băng lớp]] nhanh đối tượng được chọn. Mở lại toàn bộ bằng `LAYTHW`.
- `LAYMRG` (Layer Merge): "Vũ khí dọn dẹp" tuyệt đỉnh khi nhận bản vẽ đối tác. Gộp toàn bộ các layer rác (ví dụ `layer1`, `net_ve_tam`) vào layer chuẩn `Net-Thay` và tự động xoá sạch layer rác khỏi file.

```hotspots
image: media/ac-04-06-layer-tools.svg
alt: Bảng công cụ tiện ích Layer gồm LAYISO cô lập, LAYFRZ đóng băng, LAYOFF tắt hiển thị và LAYMRG gộp lớp
layout: central
points:
  - id: tool-layiso
    x: 25
    y: 35
    title: Lệnh LAYISO (Cô lập Layer)
    text: Nhấp vào 1 vật thể → Tự động ẩn hoặc khoá toàn bộ các layer còn lại. Phục hồi bằng LAYUNISO.
    quiz: q-ac-04-06-1
  - id: tool-laymrg
    x: 75
    y: 75
    title: Lệnh LAYMRG (Gộp Layer)
    text: Chuyển toàn bộ đối tượng từ layer nguồn sang layer đích và tự xoá sạch layer nguồn rác.
    quiz: q-ac-04-06-2
```

## Cách dùng từng bước

1. **Cô lập layer bằng LAYISO:**
   - Gõ lệnh `LAYISO` rồi nhấn [Enter].
   - Nhấp chuột chọn một đối tượng thuộc layer bạn muốn giữ lại (ví dụ một nét thấy).
   - Nhấn [Enter]. Ngay lập tức toàn bộ các layer kích thước, nét khuất, chữ viết sẽ bị ẩn hoặc khoá mờ đi.
   - Bạn thoải mái chỉnh sửa, quét chọn đối tượng mong muốn.
2. **Huỷ bỏ cô lập bằng LAYUNISO:**
   - Sau khi chỉnh sửa xong, gõ lệnh `LAYUNISO` rồi nhấn [Enter].
   - Toàn bộ các layer bị ẩn/khoá trước đó sẽ lập tức hiển thị lại đầy đủ như cũ!
3. **Tắt nhanh lớp bằng LAYOFF:**
   - Gõ `LAYOFF` rồi nhấn [Enter].
   - Nhấp chuột lần lượt vào các đối tượng bạn muốn ẩn (bấm vào chữ → layer chữ tắt; bấm vào kích thước → layer kích thước tắt).
   - Nhấn [Enter] để kết thúc lệnh.
   - Khi muốn bật lại toàn bộ tất cả các layer đang bị tắt: Gõ `LAYON` rồi nhấn [Enter].
4. **Gộp layer rác bằng LAYMRG:**
   - Gõ `LAYMRG` rồi nhấn [Enter].
   - Nhấp chọn đối tượng thuộc layer rác cần gộp (hoặc gõ `N` để chọn theo tên).
   - Nhấn [Enter] để kết thúc bước chọn layer nguồn.
   - Nhấp chọn đối tượng thuộc layer đích mà bạn muốn chuyển đến.
   - AutoCAD hỏi xác nhận: `Are you sure you want to continue? [Yes/No] <N>:`. Gõ `Y` rồi nhấn [Enter].
   - Kết quả: Toàn bộ vật thể tự động chuyển sang layer đích và layer rác biến mất hoàn toàn!

## Tuỳ chọn và mẹo

> [!TIP]
> Cấu hình cách thức hoạt động của `LAYISO`: Gõ `LAYISO`, gõ `S` (Settings), bạn có thể chọn giữa chế độ *Off* (ẩn hoàn toàn các layer khác) hoặc chế độ *Lock and Fade* (khoá và làm mờ 50% các layer khác - rất an toàn và trực quan).

> [!TIP]
> Luôn dùng `LAYMRG` thay vì cố gắng chọn rồi chuyển layer thủ công khi bạn muốn xoá triệt để một layer cứng đầu không chịu cho xoá trong Layer Properties Manager.

## Tự kiểm tra

```quiz
id: q-ac-04-06-1
type: single
question: Sau khi thực hiện lệnh LAYISO để cô lập một layer làm việc, bạn dùng lệnh nào để khôi phục lại hiển thị cho toàn bộ các layer khác?
options:
  - text: LAYUNISO
    correct: true
    why: LAYUNISO là lệnh giải phóng trạng thái cô lập của LAYISO
  - text: LAYON
    why: LAYON chỉ bật lại các layer bị tắt bởi LAYOFF
  - text: LAYTHW
    why: LAYTHW làm tan băng các layer bị đóng băng bởi LAYFRZ
  - text: UNDO
    why: Dùng UNDO sẽ huỷ luôn các thao tác vẽ bạn vừa làm trong lúc cô lập
explain: "Lệnh LAYUNISO là cặp lệnh đối xứng với LAYISO, giúp đưa tất cả các layer vừa bị ẩn hoặc khoá trở về trạng thái hiển thị bình thường trước đó."
tags: [layiso, layuniso, tien-ich]
```

```quiz
id: q-ac-04-06-2
type: single
question: Lệnh nào dưới đây cho phép bạn chuyển toàn bộ đối tượng từ một layer rác sang layer chuẩn và tự động xoá bỏ layer rác đó khỏi bản vẽ?
options:
  - text: LAYMRG (Layer Merge)
    correct: true
    why: LAYMRG gộp layer nguồn vào layer đích và tự động xoá sạch layer nguồn
  - text: LAYDEL
    why: LAYDEL xoá thẳng layer và xoá luôn mọi đối tượng trên đó mà không gộp
  - text: LAYOFF
    why: LAYOFF chỉ tắt tạm thời hiển thị
  - text: MATCHPROP
    why: MATCHPROP đổi thuộc tính từng đối tượng nhưng không xoá layer rác
explain: "Lệnh LAYMRG (Layer Merge) là công cụ chuyên nghiệp để dọn dẹp bản vẽ: gộp toàn bộ thực thể của layer cũ vào layer mới và triệt tiêu vĩnh viễn layer thừa."
tags: [laymrg, gop-layer, don-dep]
```

```quiz
id: q-ac-04-06-3
type: truefalse
question: Khi thực hiện lệnh LAYOFF, bạn có thể nhấp chuột trực tiếp lên các đối tượng trên bản vẽ để tắt nhanh layer của chúng mà không cần mở bảng Layer Properties Manager.
answer: true
explain: "Lệnh LAYOFF cho phép người dùng bấm chuột trực tiếp vào hình vẽ trên màn hình để tắt ngay layer đó một cách trực quan và cực kỳ nhanh chóng."
tags: [layoff, truc-quan]
```

```quiz
id: q-ac-04-06-4
type: hotspot
question: Bấm vào vị trí minh hoạ lệnh LAYISO (Cô lập Layer) trên sơ đồ công cụ.
use: hotspots
answer: tool-layiso
explain: "Lệnh LAYISO nằm ở góc trên bên trái của sơ đồ các tiện ích Layer."
tags: [layiso, hotspot]
```

## Lỗi thường gặp

- **Triệu chứng:** Dùng LAYISO xong nhưng các layer khác không bị ẩn đi mà chỉ bị mờ mờ và có biểu tượng ổ khoá.
  - *Nguyên nhân:* Tuỳ chọn Settings của lệnh LAYISO đang ở chế độ *Lock and Fade* thay vì *Off*.
  - *Cách sửa:* Gõ `LAYISO`, gõ `S` (Settings), gõ `O` (Off) để các layer khác ẩn hoàn toàn nếu bạn không thích chế độ làm mờ.
- **Triệu chứng:** Dùng LAYOFF tắt nhầm mất layer hiện hành và AutoCAD hiện cảnh báo *"The current layer will be turned off"*.
  - *Nguyên nhân:* Nhấp tắt đúng layer đang dùng để vẽ.
  - *Cách sửa:* Gõ `LAYON` để bật lại toàn bộ, sau đó chọn một layer khác làm Current Layer trước khi tắt layer cũ.

## Bài tập thực hành

- [ ] Gõ `LINE` vẽ 2 đoạn thẳng trên layer `Net-Thay` và 2 đoạn thẳng trên layer `Net-Khuat`. <!-- expect: LINE -->
- [ ] Gõ `LAYISO` và nhấp chọn 1 đoạn thẳng trên layer `Net-Thay`. <!-- expect: LAYISO -->
- [ ] Quan sát thấy các đoạn thẳng trên layer `Net-Khuat` đã bị ẩn hoặc khoá mờ đi.
- [ ] Gõ `LAYUNISO` để khôi phục lại hiển thị cho toàn bộ các layer. <!-- expect: LAYUNISO -->
- [ ] Gõ `LAYOFF` và nhấp thử vào 1 đối tượng để tắt nhanh layer đó, sau đó gõ `LAYON` để bật lại. <!-- expect: LAYOFF -->

## Nguồn tham khảo

```links
- title: Các lệnh tiện ích Layer trong AutoCAD (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Layer+Tools
  kind: official
  lang: en
  note: Hướng dẫn chính thức về LAYISO, LAYUNISO, LAYOFF, LAYON, LAYFRZ, LAYTHW
- title: Lệnh LAYMRG gộp layer và dọn dẹp bản vẽ (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=LAYMRG+Command
  kind: official
  lang: en
  note: Hướng dẫn thao tác gộp layer an toàn trong các dự án CAD lớn
```
