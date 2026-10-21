---
id: ac-05-03
title: Ghi kích thước hàng loạt siêu tốc với QDIM
category: Ghi kích thước
tags: [qdim, dimension, nang-suat, meo-ve]
level: intermediate
minutes: 15
needs: [ac-05-01]
appVersions: ['2024', '2025']
edition: all
---
# Ghi kích thước hàng loạt siêu tốc với QDIM

> **Mục tiêu:**
> - Sử dụng lệnh `QDIM` để tạo hàng loạt kích thước chỉ bằng một thao tác quét chuột.
> - Chuyển đổi linh hoạt giữa các chế độ Continuous, Baseline, Staggered và Ordinate trong QDIM.
> - Chỉnh sửa và loại bỏ các điểm đo thừa trực tiếp trong câu lệnh đo nhanh.

## Sức mạnh của lệnh đo nhanh QDIM

Nếu bạn có một dãy hàng rào 20 cột, hoặc một chi tiết cơ khí bậc thang phức tạp, việc bấm từng điểm đo bằng `DIMLINEAR` hay `DIMCONTINUE` vẫn mất vài phút. Lệnh `QDIM` (Quick Dimension) được sinh ra để rút ngắn toàn bộ quá trình đó xuống chỉ còn... 3 giây!

Chỉ cần quét chuột chọn toàn bộ cụm đối tượng, `QDIM` sẽ tự động phân tích tất cả các đỉnh, mút đoạn thẳng và tâm hình tròn, sau đó dựng ngay một dàn kích thước hoàn chỉnh theo bất kỳ phương nào bạn muốn.

Các chế độ đo tích hợp mạnh mẽ trong `QDIM`:
- **`Continuous` (Mặc định):** Dựng chuỗi kích thước nối tiếp nhau.
- **`Baseline`:** Tự động lấy một đầu mút làm gốc và xếp tầng các kích thước song song.
- **`Staggered`:** Xếp sole các con số kích thước trên dưới để tránh bị đè chữ trong những đoạn hẹp.
- **`Radius` / `Diameter`:** Tự động đo toàn bộ các cung cong hoặc đường tròn được quét chọn.
- **`Ordinate`:** Đo toạ độ tương đối theo gốc toạ độ gia công phay/tiện CNC.

## Cách dùng từng bước

### 1. Đo chuỗi kích thước bằng một lần quét
1. Gõ `QDIM` rồi nhấn [Enter].
2. Dùng cửa sổ chọn (`Window` hoặc `Crossing`) quét qua toàn bộ các đoạn thẳng, khối hình cần đo. Nhấn [Enter] để kết thúc chọn đối tượng.
3. Di chuột lên trên hoặc sang ngang. Toàn bộ chuỗi kích thước lập tức hiện ra theo vị trí con trỏ chuột.
4. Bấm chuột trái để đặt vị trí đường kích thước.

### 2. Đổi chế độ đo sang Baseline hoặc Staggered
1. Gõ `QDIM` [Enter] và quét chọn các đối tượng, nhấn [Enter].
2. Trước khi bấm chuột định vị, nhìn xuống thanh nhắc lệnh sẽ thấy danh sách chế độ: `[Continuous/Staggered/Baseline/Ordinate/Radius/Diameter/datumPoint/Edit]`.
3. Gõ `B` [Enter] để chuyển sang kiểu đo song song từ gốc chung (`Baseline`).
4. Gõ `S` [Enter] nếu các chi tiết quá sát nhau và bạn muốn số kích thước so le tự động (`Staggered`).

### 3. Loại bỏ điểm đo không cần thiết bằng tuỳ chọn Edit
1. Khi `QDIM` phân tích hình vẽ, đôi khi nó chọn cả những điểm chi tiết nhỏ bên trong mà bạn không muốn đo.
2. Tại thanh nhắc lệnh, gõ `E` (Edit) rồi nhấn [Enter].
3. Các điểm đo sẽ sáng lên. Bạn chỉ việc bấm chuột vào các điểm muốn loại trừ (`Remove`) hoặc bấm thêm điểm mới (`Add`).
4. Nhấn [Enter] để quay lại và đặt kích thước như bình thường.

## Tuỳ chọn và mẹo làm việc nhanh

> [!TIP]
> Bạn có thể quét chọn cả đường tròn lẫn đường thẳng cùng lúc. Nếu chọn tuỳ chọn `Radius` hoặc `Diameter`, QDIM sẽ tự động lọc và chỉ đo các đường tròn trong vùng quét, bỏ qua các đoạn thẳng khác.

> [!TIP]
> Dùng tuỳ chọn `datumPoint` (gõ `P`) trong chế độ `Baseline` để chỉ định lại vị trí gốc toạ độ chuẩn (0) theo đúng ý đồ thiết kế, thay vì để AutoCAD tự chọn điểm biên ngoài cùng.

## Tự kiểm tra

```quiz
id: q-ac-05-03-1
type: single
question: "Ưu điểm vượt trội lớn nhất của lệnh QDIM so với DIMLINEAR thông thường là gì?"
options:
  - text: "Cho phép quét chọn nhiều đối tượng cùng lúc để tạo hàng loạt kích thước trong một thao tác"
    correct: true
    why: "QDIM tự trích xuất các điểm mút hình học và xuất toàn bộ kích thước chỉ sau một cú click."
  - text: "Tự động đổi màu kích thước sang màu đỏ"
    correct: false
    why: "Màu sắc do Layer hoặc Dimstyle quản lý."
  - text: "Chỉ hoạt động được với các khối Dynamic Block"
    correct: false
    why: "QDIM dùng được trên mọi đối tượng hình học 2D cơ bản."
  - text: "Không bao giờ cần chỉ định vị trí đặt đường kích thước"
    correct: false
    why: "Bạn vẫn phải di chuột và bấm click để đặt vị trí dàn kích thước."
explain: "Lệnh QDIM giúp tiết kiệm tới 80% thời gian khi phải đo các mặt bằng hoặc trục cơ khí có nhiều bậc liên tiếp."
```

```quiz
id: q-ac-05-03-2
type: single
question: "Trong lệnh QDIM, tuỳ chọn nào cho phép loại bỏ bớt các mốc đo không mong muốn trong vùng quét?"
options:
  - text: "Tuỳ chọn Edit (gõ E)"
    correct: true
    why: "Tuỳ chọn Edit cho phép Remove bớt điểm hoặc Add thêm điểm đo."
  - text: "Lệnh ERASE"
    correct: false
    why: "ERASE sẽ xoá mất đối tượng hình vẽ gốc."
  - text: "Nhấn nút Esc"
    correct: false
    why: "Esc sẽ huỷ bỏ toàn bộ lệnh QDIM."
  - text: "Tuỳ chọn Ordinate"
    correct: false
    why: "Ordinate là chế độ đo toạ độ gia công."
explain: "Tuỳ chọn Edit trong QDIM cung cấp tính năng thêm hoặc bớt các điểm chốt đo rất trực quan."
```

```quiz
id: q-ac-05-03-3
type: truefalse
question: "QDIM có thể tự động đo đường kính cho tất cả các hình tròn được quét chọn nếu chuyển sang tuỳ chọn Diameter."
answer: false
explain: "Khi quét cả một cụm nhiều lỗ khoan rồi chọn Diameter trong QDIM, toàn bộ các lỗ sẽ được gắn ký hiệu kích thước đường kính tức thì."
```

## Lỗi thường gặp

- **Dàn kích thước xuất hiện quá nhiều điểm vụn vặt:** Do quét trúng nét hatch hoặc các đường tim trục có nhiều giao điểm. Khắc phục: Khoá hoặc ẩn layer tim trục / layer hatch trước khi gõ `QDIM`, hoặc dùng tuỳ chọn `Edit` để loại bớt điểm.
- **Kích thước bị chồng lấn do khoảng cách quá gần:** Các đoạn thẳng cách nhau chỉ 1-2mm khiến số bị dính vào nhau. Khắc phục: Chọn chế độ `Staggered` để số kích thước tự động xếp sole sole so le nhau.

## Bài tập thực hành

- [ ] Vẽ một đường zigzag bậc thang gồm 5 bậc bằng lệnh `PLINE` (mỗi bậc ngang 30mm, đứng 20mm). <!-- expect: PLINE -->
- [ ] Gõ `QDIM`, quét toàn bộ đường bậc thang vừa vẽ và nhấn Enter. <!-- expect: QDIM -->
- [ ] Di chuột lên phía trên để tạo chuỗi đo ngang liên tục 5 bậc. <!-- expect: QDIM -->
- [ ] Gõ tiếp `QDIM`, quét lại hình bậc thang, gõ `B` để chuyển sang chế độ `Baseline` và kéo sang mép trái để đo tổng chiều cao các bậc. <!-- expect: QDIM -->

## Nguồn tham khảo

```links
- title: "Tài liệu lệnh QDIM từ Autodesk Knowledge Network"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=QDIM"
  kind: official
```
