---
id: ac-05-08
title: Tự động thích ứng tỉ lệ bản vẽ với tính năng Annotative
category: Ghi kích thước
tags: [annotative, dimension, scale, viewport, chuyen-nghiep]
level: advanced
minutes: 25
needs: [ac-05-04]
appVersions: ['2024', '2025']
edition: all
---
# Tự động thích ứng tỉ lệ bản vẽ với tính năng Annotative

> **Mục tiêu:**
> - Hiểu bản chất cơ chế chú thích thông minh Annotative trong AutoCAD.
> - Bật tính năng Annotative cho Text, Dimension và Multileader để tự động co giãn theo tỉ lệ in.
> - Quản lý danh sách tỉ lệ chú thích và xử lý hiển thị đa tỉ lệ trên cùng một đối tượng.

## Nỗi ám ảnh tỉ lệ bản vẽ cổ điển và lời giải Annotative

Trong cách vẽ truyền thống trước đây, nếu một chi tiết mặt bằng cần in ở tỉ lệ 1:100, người vẽ phải tạo Dimstyle 1:100 (chữ số cao 250mm). Nếu chi tiết trích đoạn vệ sinh cần in ở tỉ lệ 1:20, người vẽ lại phải tạo thêm một Dimstyle 1:20 (chữ số cao 50mm). Kết quả là trong một tệp bản vẽ có hàng chục kiểu Dimstyle, Textstyle rác rưởi, rất dễ đo nhầm tỉ lệ.

Từ phiên bản AutoCAD 2008, Autodesk đã đưa ra cuộc cách mạng mang tên **[[Annotative]]** (ký hiệu biểu tượng thước ba cạnh màu xanh).

Với Annotative:
- Bạn chỉ cần **DUY NHẤT một kiểu Dimstyle và TextStyle**.
- Bạn luôn quy định chiều cao chữ khi in thật ra giấy là `2.5mm`.
- Trong không gian làm việc hoặc qua các khung nhìn Viewport của Layout, khi bạn đổi tỉ lệ hiển thị (1:100, 1:50, 1:20...), toàn bộ chữ số kích thước sẽ **tự động phóng to hoặc thu nhỏ tương ứng** để khi in ra giấy, chiều cao của chúng luôn luôn bằng đúng 2.5mm!

## Cách kích hoạt tính năng Annotative

### 1. Trong Dimension Style (DIMSTYLE)
1. Gõ `D` [Enter], chọn kiểu kích thước cần sửa hoặc bấm **New**.
2. Chuyển sang thẻ **Fit**.
3. Tại mục *Scale for dimension features*, tích chọn vào ô tròn **Annotative** (thay vì ô *Use overall scale of*).
4. Bấm **OK** để lưu lại.

### 2. Trong Text Style (STYLE)
1. Gõ `ST` [Enter].
2. Chọn kiểu chữ, tích chọn ô vuông **Annotative**.
3. Ô **Paper Text Height** nhập `2.5` mm (chiều cao chuẩn in ra giấy).
4. Bấm **Apply**.

### 3. Trong Multileader Style (MLEADERSTYLE)
1. Gõ `MLS` [Enter], sửa kiểu ghi chú.
2. Tại thẻ **Leader Structure**, tích chọn ô **Annotative**.

## Cách dùng từng bước trên thanh trạng thái

Ở góc dưới cùng bên phải màn hình (thanh trạng thái [[Status Bar]]), bạn sẽ thấy 3 biểu tượng liên quan đến Annotative:
1. **Annotation Scale (Tỉ lệ chú thích hiện hành):** Ví dụ đang chọn `1:100`. Khi bạn đo kích thước, kích thước đó sẽ tự động mang tỉ lệ 1:100.
2. **Auto Add Scales (Tự động thêm tỉ lệ - Biểu tượng cây thước có dấu sấm sét):** Khi bật nút này, nếu bạn đổi tỉ lệ sang 1:50, AutoCAD sẽ tự động gán thêm tỉ lệ 1:50 vào tất cả các đối tượng Annotative đang có.
3. **Show Annotation Objects (Hiển thị đối tượng chú thích - Biểu tượng bóng đèn):** Bật để hiển thị tất cả các kích thước bất kể tỉ lệ hiện hành là bao nhiêu.

## Quản lý danh sách tỉ lệ của đối tượng (OBJECTSCALE)

Một đối tượng Annotative có thể chứa nhiều tỉ lệ cùng lúc:
1. Chọn đối tượng kích thước trên màn hình.
2. Nhấp chuột phải > chọn **Annotation Object Scale** > chọn **Add/Delete Scales...** (hoặc gõ lệnh `OBJECTSCALE`).
3. Trong hộp thoại, bạn có thể bấm **Add** để gán thêm tỉ lệ (ví dụ thêm 1:50 vào kích thước vốn chỉ có 1:100).
4. Giờ đây, khi bạn xem chi tiết này ở khung nhìn 1:100 hay 1:50, kích thước đều hiển thị hoàn hảo!

> [!TIP]
> Tắt nút *Auto Add Scales* (cây thước có sấm sét) sau khi hoàn thiện bản vẽ để tránh việc vô tình nhảy tỉ lệ khiến tệp bản vẽ bị gán hàng trăm tỉ lệ rác làm chậm máy.

> [!TIP]
> Dùng biến hệ thống `ANNOALLVISIBLE = 1` để luôn nhìn thấy toàn bộ các kích thước dù tỉ lệ khung nhìn hiện tại có trùng khớp hay không.

## Tự kiểm tra

```quiz
id: q-ac-05-08-1
type: single
question: "Biểu tượng nhận biết một đối tượng có tính năng Annotative trong AutoCAD là gì?"
options:
  - text: "Mặt cắt cây thước đo ba cạnh hình tam giác"
    correct: true
    why: "Biểu tượng thước đo ba cạnh (Architectural Scale) thể hiện tính năng Annotative."
  - text: "Hình ngôi sao 5 cánh màu vàng"
    correct: false
    why: "Không có biểu tượng ngôi sao cho tính năng này."
  - text: "Hình cái cờ lê màu đỏ"
    correct: false
    why: "Cờ lê là biểu tượng của phần cài đặt Settings."
  - text: "Hình ổ khoá màu xám"
    correct: false
    why: "Ổ khoá là tính năng Lock layer hoặc khoá Viewport."
explain: "Khi rê chuột vào một chữ hoặc kích thước Annotative, con trỏ sẽ hiện biểu tượng mặt cắt cây thước tam giác màu xanh."
```

```quiz
id: q-ac-05-08-2
type: single
question: "Lợi ích lớn nhất khi sử dụng Dimstyle có bật Annotative là gì?"
options:
  - text: "Chữ số kích thước luôn giữ đúng chiều cao chuẩn khi in ở bất kỳ tỉ lệ nào (1:100, 1:50, 1:20...)"
    correct: true
    why: "Annotative tự động nhân tỉ lệ để chiều cao trên giấy in luôn là hằng số cố định."
  - text: "Tự động sửa sai kích thước chi tiết từ 100mm thành 200mm"
    correct: false
    why: "Annotative không thay đổi giá trị đo thực tế của đối tượng."
  - text: "Tự động lưu bản vẽ sau mỗi 10 giây"
    correct: false
    why: "Tự lưu thuộc quyền quản lý của tính năng AutoSave."
  - text: "Không cần cài đặt AutoCAD mà vẫn in được"
    correct: false
    why: "Annotative là tính năng đồ hoạ nội bộ của AutoCAD."
explain: "Với Annotative, người thiết kế chỉ cần dùng 1 kiểu kích thước duy nhất cho mọi bản vẽ từ tỉ lệ tổng thể đến trích đoạn chi tiết."
```

```quiz
id: q-ac-05-08-3
type: truefalse
question: "Một kích thước Annotative có thể cùng lúc hỗ trợ nhiều tỉ lệ khác nhau nhờ lệnh OBJECTSCALE."
answer: false
explain: "Bạn có thể định vị các vị trí chữ khác nhau cho từng tỉ lệ cụ thể để tránh bị đè nét khi thu phóng."
```

## Lỗi thường gặp

- **Kích thước đột ngột biến mất khi đổi tỉ lệ khung nhìn:** Do kích thước đó chưa được thêm tỉ lệ hiện hành vào danh sách Annotative. Khắc phục: Bật biến `ANNOALLVISIBLE = 1` hoặc dùng `OBJECTSCALE` để thêm tỉ lệ tương ứng.
- **Bản vẽ bị chậm và giật khi chọn đối tượng:** Do bật nút Auto Add Scales liên tục khiến mỗi kích thước gánh hàng chục tỉ lệ không dùng tới. Khắc phục: Dùng lệnh `SCALELISTEDIT` dọn bớt tỉ lệ thừa và tắt nút sấm sét.

## Bài tập thực hành

- [ ] Gõ `DIMSTYLE`, chọn kiểu `ISO-25`, tạo kiểu mới đặt tên là `DIM-ANNOTATIVE`. <!-- expect: DIMSTYLE -->
- [ ] Trong thẻ `Fit`, tích chọn vào tuỳ chọn `Annotative`. Bấm OK và Set Current. <!-- expect: DIMSTYLE -->
- [ ] Nhìn xuống thanh trạng thái góc phải, đổi Annotation Scale sang `1:50`.
- [ ] Dùng `DIMLINEAR` đo thử một đoạn thẳng 2000mm và quan sát kích cỡ chữ tự động phóng to gấp 50 lần. <!-- expect: DIMLINEAR -->

## Nguồn tham khảo

```links
- title: "Khái niệm và cơ chế hoạt động Annotative từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=Annotative"
  kind: official
```
