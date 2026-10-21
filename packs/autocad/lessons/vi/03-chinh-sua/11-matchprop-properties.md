---
id: ac-03-11
title: Sao chép thuộc tính với MATCHPROP và bảng PROPERTIES
category: Chỉnh sửa
tags: [matchprop, properties, sao-chep-thuoc-tinh, layer, mau-sac, chinh-sua]
level: beginner
minutes: 15
needs: [ac-03-01]
appVersions: ['2024', '2025']
edition: all
---
# Sao chép thuộc tính với MATCHPROP và bảng PROPERTIES

> **Mục tiêu:**
> - Sử dụng lệnh MATCHPROP ("chổi sơn thuộc tính") để sao chép layer, màu sắc, linetype sang các đối tượng khác.
> - Sử dụng bảng điều khiển PROPERTIES (Ctrl + 1) để kiểm tra và thay đổi thông số hình học, cao độ và thuộc tính.
> - Lọc và chỉnh sửa đồng loạt thuộc tính của hàng chục đối tượng cùng lúc thông qua bảng Properties.

## Lệnh này làm gì và khi nào dùng

Khi vẽ bản vẽ lớn, rất nhiều đối tượng vô tình bị vẽ sai layer, sai màu sắc hoặc sai kiểu đường nét. Thay vì phải chọn từng đối tượng rồi đổi từng thông số thủ công, AutoCAD cung cấp hai công cụ quản lý thuộc tính quyền năng nhất:
- `MATCHPROP` (phím tắt `MA`): Thường được ví như chiếc "chổi sơn thần kỳ" (Format Painter). Bạn chỉ cần nhấp vào một đối tượng mẫu chuẩn, sau đó quét chổi qua bất kỳ đối tượng nào khác, toàn bộ Layer, Màu sắc, Kiểu đường nét (Linetype), Độ dày nét (Lineweight) và tỷ lệ Hatch sẽ được áp đặt tức thì!
- `PROPERTIES` (phím tắt `PR`, `CH` hoặc tổ hợp [Ctrl + 1]): Bảng thuộc tính toàn diện nhất của AutoCAD. Khi mở bảng này, mọi thông tin của đối tượng đang chọn (toạ độ điểm mút, bán kính, diện tích, góc nghiêng, layer, độ dày...) đều hiện ra để bạn sửa trực tiếp bằng bàn phím.

## Cách dùng từng bước

1. **Sao chép nhanh thuộc tính bằng MATCHPROP:**
   - Gõ `MATCHPROP` hoặc phím tắt `MA` rồi nhấn [Enter]. Con trỏ chuột biến thành hình chiếc chổi quét sơn.
   - Nhấp chuột chọn đối tượng mẫu (Select source object): Đây là đối tượng đang có layer và thuộc tính chuẩn mà bạn muốn bắt chước.
   - Quét chọn các đối tượng đích (Select destination object):
     - Nhấp từng đối tượng muốn đổi.
     - Hoặc kéo khung quét qua hàng loạt đối tượng.
   - Toàn bộ các đối tượng đích sẽ lập tức đổi màu, đổi layer và đổi kiểu nét giống hệt đối tượng mẫu.
   - Nhấn [Enter] hoặc [Esc] để kết thúc lệnh.
2. **Tuỳ chỉnh các thuộc tính sao chép (Settings):**
   - Đang trong lệnh MATCHPROP sau khi chọn đối tượng mẫu, gõ chữ `S` (Settings) rồi [Enter].
   - Một hộp thoại hiện ra cho phép bạn chọn lọc: ví dụ chỉ muốn sao chép Layer mà không muốn sao chép Màu sắc hay Chiều cao chữ.
3. **Sử dụng bảng PROPERTIES (Ctrl + 1):**
   - Nhấn tổ hợp phím [Ctrl + 1] trên bàn phím để mở bảng Properties (thường neo ở cạnh trái màn hình).
   - Nhấp chuột chọn một đối tượng bất kỳ trên bản vẽ (ví dụ một đường tròn).
   - Trong bảng Properties, quan sát các trường thông tin:
     - Mục *General:* Layer, Color, Linetype, Lineweight.
     - Mục *Geometry:* Center X, Center Y, Radius (Bán kính), Diameter (Đường kính), Area (Diện tích), Circumference (Chu vi).
   - Nhấp đúp chuột vào ô giá trị (ví dụ đổi ô *Radius* từ `30` thành `50`), đường tròn trên bản vẽ sẽ tự động to lên tức thì mà không cần dùng lệnh Scale!

## Tuỳ chọn và mẹo

> [!TIP]
> Phím tắt [Ctrl + 1] là phím bật/tắt bảng Properties. Hãy giữ bảng này luôn mở ở chế độ tự động gập (Auto-hide) sát mép màn hình để kiểm tra nhanh diện tích hoặc đổi layer chỉ trong 1 thao tác bấm chuột.

> [!TIP]
> Khi quét chọn nhiều đối tượng cùng một lúc, ô danh sách xổ xuống ở đỉnh bảng Properties cho phép bạn lọc riêng từng loại (ví dụ chỉ lọc riêng đối tượng Text để đổi chiều cao chữ hàng loạt).

## Tự kiểm tra

```quiz
id: q-ac-03-011-1
type: single
question: Lệnh MATCHPROP (phím tắt MA) trong AutoCAD có chức năng chính tương đương với công cụ nào dưới đây?
options:
  - text: Format Painter (Chổi sao chép định dạng trong Microsoft Word / Excel)
    correct: true
    why: MATCHPROP sao chép toàn bộ thuộc tính layer, màu, linetype từ đối tượng này sang đối tượng khác
  - text: Lệnh dán đối tượng Paste (Ctrl + V)
    why: Paste là dán hình học, không phải sao chép thuộc tính
  - text: Lệnh phóng to màn hình Zoom
    why: Zoom thay đổi góc nhìn
  - text: Lệnh in ấn bản vẽ Plot
    why: Plot dùng để xuất bản vẽ ra giấy/PDF
explain: "Lệnh MATCHPROP sao chép toàn bộ thuộc tính (layer, màu sắc, linetype, lineweight, hatch scale, text style) từ một đối tượng mẫu sang các đối tượng đích, tương tự như Format Painter."
tags: [matchprop, properties, so-sanh]
```

```quiz
id: q-ac-03-011-2
type: single
question: Tổ hợp phím tắt nhanh nào trên bàn phím dùng để bật hoặc ẩn bảng thuộc tính đối tượng (Properties Palette)?
options:
  - text: Ctrl + 1
    correct: true
    why: Ctrl + 1 là phím tắt mặc định mở bảng Properties
  - text: Ctrl + 9
    why: Ctrl + 9 bật tắt dòng lệnh Command Line
  - text: Ctrl + 0
    why: Ctrl + 0 bật tắt chế độ Clean Screen
  - text: Ctrl + S
    why: Ctrl + S dùng để lưu file
explain: "Nhấn tổ hợp phím [Ctrl + 1] sẽ mở ra bảng điều khiển Properties đầy đủ nhất của AutoCAD, cho phép can thiệp vào mọi thuộc tính hình học của đối tượng."
tags: [properties, phim-tat]
```

```quiz
id: q-ac-03-011-3
type: truefalse
question: Khi mở bảng Properties, bạn có thể chỉnh sửa trực tiếp giá trị bán kính của đường tròn bằng cách gõ số mới vào ô Radius.
answer: true
explain: "Bảng Properties cho phép chỉnh sửa hai chiều: thay đổi giá trị số trong các ô Geometry (như Radius, Length, Angle) sẽ lập tức làm thay đổi hình dáng thực tế của đối tượng trên bản vẽ."
tags: [properties, geometry]
```

## Lỗi thường gặp

- **Triệu chứng:** Dùng MATCHPROP sao chép từ một đường nét đứt (Hidden) sang đường thẳng khác nhưng đường đích nhìn vẫn như nét liền.
  - *Nguyên nhân:* Thuộc tính Linetype đã được sao chép thành công nhưng tỷ lệ hiển thị nét đứt (`LTSCALE`) của bản vẽ đang quá lớn hoặc quá bé khiến nét đứt không hiển thị được mắt thường.
  - *Cách sửa:* Gõ lệnh `LTSCALE` và thử chỉnh lại hệ số tỷ lệ (ví dụ gõ `10` hoặc `0.5`).
- **Triệu chứng:** Mở bảng Properties lên nhưng màn hình bị giật lag và bảng chiếm mất diện tích vẽ.
  - *Nguyên nhân:* Bảng Properties đang ở chế độ ghim cứng cố định.
  - *Cách sửa:* Bấm vào biểu tượng hình tam giác nhỏ trên thanh tiêu đề của bảng Properties để bật chế độ *Auto-hide* (tự động thu nhỏ thành một thanh icon gọn gàng khi rê chuột ra ngoài).

## Bài tập thực hành

- [ ] Gõ `LINE` vẽ một đoạn thẳng thứ nhất. <!-- expect: LINE -->
- [ ] Mở bảng `PROPERTIES` bằng phím [Ctrl + 1], nhấp chọn đoạn thẳng và đổi màu Color của nó sang màu `Red` (Đỏ). <!-- expect: PROPERTIES -->
- [ ] Gõ `LINE` vẽ thêm 3 đoạn thẳng khác màu trắng mặc định. <!-- expect: LINE -->
- [ ] Gõ `MATCHPROP`, nhấp chọn đoạn thẳng màu đỏ làm mẫu. <!-- expect: MATCHPROP -->
- [ ] Quét chổi qua cả 3 đoạn thẳng màu trắng để biến toàn bộ thành màu đỏ đồng bộ.

## Nguồn tham khảo

```links
- title: Lệnh MATCHPROP sao chép thuộc tính (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=MATCHPROP+Command
  kind: official
  lang: en
  note: Hướng dẫn chi tiết cài đặt Property Settings và sao chép thuộc tính trong AutoCAD
- title: Bảng thuộc tính Properties Palette (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Properties+Palette
  kind: official
  lang: en
  note: Toàn bộ danh mục General, Geometry, Misc của bảng điều khiển Properties
```
