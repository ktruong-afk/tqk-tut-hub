---
id: ac-04-05
title: Bộ lọc Layer Filters và Trạng thái Layer States
category: Layer & Thuộc tính
tags: [layerstate, layer-filters, layer-states-manager, bo-loc-layer, trang-thai-layer]
level: beginner
minutes: 15
needs: [ac-04-01]
appVersions: ['2024', '2025']
edition: all
---
# Bộ lọc Layer Filters và Trạng thái Layer States

> **Mục tiêu:**
> - Sử dụng tính năng Property Filter và Group Filter để phân loại và tìm kiếm trong dự án có hàng trăm Layer.
> - Sử dụng Layer States Manager để chụp lưu (Snapshot) và khôi phục các trạng thái hiển thị của bản vẽ.
> - Chuyển đổi linh hoạt giữa các kịch bản trình chiếu bản vẽ (bản vẽ kiến trúc, bản vẽ kết cấu, bản vẽ điện nước).

## Lệnh này làm gì và khi nào dùng

Khi làm việc trong các dự án thực tế quy mô lớn (toà nhà cao tầng, nhà máy công nghiệp), số lượng layer có thể lên tới 200 - 500 layer. Việc cuộn chuột mò mẫm tìm một layer giữa hàng trăm cái tên là một cơn ác mộng.

AutoCAD cung cấp hai công cụ phân nhóm và tự động hoá mạnh mẽ:
- [[Bộ lọc lớp]] (Layer Filters):
  - **Property Filter:** Tự động gom các layer có thuộc tính chung bằng ký tự đại diện (ví dụ lọc tất cả các layer bắt đầu bằng `AR-*` hoặc toàn bộ các layer màu Đỏ).
  - **Group Filter:** Gom thủ công các layer bạn thường xuyên làm việc cùng vào một thư mục riêng biệt.
- [[Trạng thái lớp]] (Layer States Manager - lệnh `LAYERSTATE`, phím tắt `LAS`): Chụp lưu lại "bản chụp" toàn bộ trạng thái On/Off, Freeze, Lock, Color của hệ thống layer tại một thời điểm. Ví dụ: Bạn tạo trạng thái *"In An Kien Truc"* (bật layer tường, cửa; tắt layer điện nước) và trạng thái *"Thi Cong Dien"* (bật layer đèn, dây dẫn; làm mờ tường). Khi cần in bản nào, chỉ 1 cú nhấp chuột là toàn bộ hệ thống layer tự động bật tắt đúng kịch bản!

## Cách dùng từng bước

1. **Tạo bộ lọc thuộc tính (Property Filter):**
   - Mở bảng `LAYER` (`LA`).
   - Ở cột cây thư mục bên trái bảng, bấm nút **New Property Filter** (hình chiếc phễu).
   - Đặt tên bộ lọc (Filter name, ví dụ `Layers-Kien-Truc`).
   - Tại dòng *Name*: Gõ `KT-*` (dấu sao `*` là ký tự đại diện cho mọi chữ cái phía sau).
   - Khung xem trước phía dưới sẽ tự động lọc ra toàn bộ các layer có tiền tố `KT-` (như `KT-Tuong`, `KT-Cua`, `KT-San`). Bấm **OK**.
2. **Tạo bộ lọc nhóm kéo thả (Group Filter):**
   - Bấm nút **New Group Filter** (hình thư mục vàng).
   - Đặt tên nhóm (ví dụ `Nhóm_Thuong_Dung`).
   - Nhấp vào mục *All*, kéo thả các layer bạn hay dùng bỏ vào thư mục vừa tạo.
3. **Chụp lưu trạng thái Layer State (LAYERSTATE):**
   - Cấu hình bật tắt, đóng băng các layer theo đúng kịch bản mong muốn (ví dụ kịch bản để vẽ chi tiết cơ khí).
   - Gõ lệnh `LAYERSTATE` hoặc phím tắt `LAS` rồi nhấn [Enter].
   - Bấm nút **New...**, đặt tên cho trạng thái (ví dụ `Ban_Ve_Gia_Cong`).
   - Bấm **OK** rồi bấm **Close**.
4. **Khôi phục trạng thái đã lưu:**
   - Khi hệ thống layer bị chỉnh sửa xáo trộn, gõ lại lệnh `LAYERSTATE`.
   - Chọn tên trạng thái `Ban_Ve_Gia_Cong` rồi bấm nút **Restore**. Toàn bộ hệ thống layer sẽ lập tức quay trở lại trạng thái On/Off, Freeze, Lock ban đầu một cách hoàn hảo!

## Tuỳ chọn và mẹo

> [!TIP]
> Bạn có thể xuất (Export) một Layer State ra file có đuôi `.las` để mang sang nạp (Import) cho các file bản vẽ khác trong cùng dự án, giúp đồng bộ hoá quy chuẩn in ấn của cả công ty.

> [!TIP]
> Trên Ribbon (*Home > Layers panel*), có sẵn một ô danh sách cuộn **Layer States** giúp bạn chuyển đổi trạng thái hiển thị của toàn bộ bản vẽ chỉ trong 1 cú bấm chuột mà không cần mở hộp thoại.

## Tự kiểm tra

```quiz
id: q-ac-04-05-1
type: single
question: Trong bảng Layer Properties Manager, công cụ nào cho phép bạn tự động gom các layer có tên bắt đầu bằng "MEP-*" vào một nhóm riêng để dễ quản lý?
options:
  - text: New Property Filter (Bộ lọc thuộc tính có dùng ký tự đại diện *)
    correct: true
    why: Property Filter lọc tự động theo các tiêu chí tên, màu, trạng thái
  - text: Lệnh ERASE
    why: ERASE là lệnh xoá hình học
  - text: Lệnh EXPLODE
    why: EXPLODE là phá vỡ đối tượng
  - text: Lệnh ZOOM
    why: ZOOM thay đổi khung nhìn
explain: "Tính năng New Property Filter trong Layer Properties Manager sử dụng quy tắc lọc thông minh (như tiền tố MEP-*) để tự động phân nhóm các layer cùng chuyên ngành kỹ thuật."
tags: [layer, filter, property-filter]
```

```quiz
id: q-ac-04-05-2
type: single
question: Tính năng Layer States Manager (lệnh LAYERSTATE) dùng để làm gì trong quản lý dự án CAD?
options:
  - text: Chụp lưu và khôi phục nhanh các cấu hình hiển thị (On/Off, Freeze, Lock...) của toàn bộ hệ thống layer
    correct: true
    why: Layer States lưu trữ các kịch bản hiển thị layer để chuyển đổi linh hoạt
  - text: Tự động đổi màu tất cả layer sang màu đen
    why: Layer States không tự ép màu đen
  - text: Xoá sạch toàn bộ các layer bị thừa
    why: Xoá layer dùng lệnh PURGE
  - text: Đổi tên bản vẽ
    why: Đổi tên file dùng Save As hoặc Windows Explorer
explain: "Layer States Manager (phím tắt LAS) cho phép bạn lưu các cấu hình hiển thị layer theo từng mục đích sử dụng (in ấn kiến trúc, xem điện nước, gia công cơ khí) và khôi phục lại tức thì bằng nút Restore."
tags: [layerstate, layer-states-manager]
```

```quiz
id: q-ac-04-05-3
type: truefalse
question: Ký tự dấu sao (*) trong trường lọc tên của Property Filter đại diện cho bất kỳ chuỗi ký tự nào đứng sau nó.
answer: true
explain: "Dấu sao (*) là ký tự đại diện chuẩn (Wildcard Character). Ví dụ nhập 'E-*' sẽ khớp với mọi layer như E-LIGHT, E-POWER, E-CABLE."
tags: [layer, filter, wildcard]
```

## Lỗi thường gặp

- **Triệu chứng:** Trong bảng Layer Properties Manager bỗng nhiên chỉ thấy hiển thị 3 layer, hàng chục layer khác bị biến mất.
  - *Nguyên nhân:* Cột cây thư mục bên trái đang vô tình chọn vào một Bộ lọc (Filter) con thay vì chọn mục gốc *All*.
  - *Cách sửa:* Bấm chuột vào dòng đầu tiên `All` (hoặc `All Used Layers`) trong danh sách Filters bên trái để hiển thị lại toàn bộ các layer.
- **Triệu chứng:** Khôi phục Layer State nhưng một số layer mới tạo sau này không tự tắt.
  - *Nguyên nhân:* Các layer đó được tạo sau thời điểm bạn bấm chụp lưu Snapshot nên không nằm trong danh sách kiểm soát của State cũ.
  - *Cách sửa:* Bật tắt thủ công và bấm nút *Save* để cập nhật lại Layer State.

## Bài tập thực hành

- [ ] Gõ `LAYER` mở bảng điều khiển. <!-- expect: LAYER -->
- [ ] Bấm nút tạo **New Property Filter**, đặt tên là `Loc-Net`, nhập mục Name là `Net*` rồi bấm OK.
- [ ] Quan sát thấy danh sách chỉ còn hiển thị các layer bắt đầu bằng chữ Net (`Net-Thay`, `Net-Khuat`).
- [ ] Gõ `LAYERSTATE` mở bảng Layer States Manager. <!-- expect: LAYERSTATE -->
- [ ] Bấm **New...**, đặt tên trạng thái là `Trang_Thai_01` và lưu lại.

## Nguồn tham khảo

```links
- title: Bộ lọc Layer Filters và quản lý danh sách layer (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Layer+Filters
  kind: official
  lang: en
  note: Hướng dẫn chính thức về tạo Property Filter, Group Filter và ký tự đại diện Wildcard
- title: Lệnh LAYERSTATE và quản lý trạng thái layer (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=LAYERSTATE+Command
  kind: official
  lang: en
  note: Toàn bộ tuỳ chọn Save, Restore, Edit, Import/Export file .las của LAYERSTATE
```
