---
id: ac-05-02
title: Đo chuỗi liên tục và song song với DIMCONTINUE và DIMBASELINE
category: Ghi kích thước
tags: [dimcontinue, dimbaseline, dimension, nang-suat]
level: beginner
minutes: 20
needs: [ac-05-01]
appVersions: ['2024', '2025']
edition: all
---
# Đo chuỗi liên tục và song song với DIMCONTINUE và DIMBASELINE

> **Mục tiêu:**
> - Sử dụng lệnh `DIMCONTINUE` để đo một chuỗi các kích thước nối tiếp nhau nhanh chóng.
> - Sử dụng lệnh `DIMBASELINE` để đo các kích thước song song có chung gốc chuẩn.
> - Kiểm soát khoảng cách tầng giữa các đường kích thước song song với biến `DIMDLI`.

## Chuỗi kích thước nối tiếp và kích thước song song

Khi thiết kế mặt bằng kiến trúc (đo từng phòng, từng nhịp cột) hoặc bản vẽ cơ khí (đo bậc trục, rãnh then), bạn thường xuyên phải đặt hàng chục đường kích thước cạnh nhau. Nếu dùng `DIMLINEAR` lặp đi lặp lại từng đoạn một, bạn sẽ mất rất nhiều thời gian và khó giữ cho các con số thẳng hàng.

AutoCAD giải quyết vấn đề này bằng 2 công cụ cực mạnh:
- **`DIMCONTINUE` (Lệnh tắt `DCO`):** Đo nối tiếp liên tục. Điểm kết thúc của kích thước trước tự động trở thành điểm bắt đầu của kích thước tiếp theo. Toàn bộ các con số nằm thẳng trên một hàng duy nhất.
- **`DIMBASELINE` (Lệnh tắt `DBA`):** Đo song song từ một mốc chuẩn gốc ([[Baseline]]). Điểm gốc ban đầu được giữ nguyên, mỗi lần bấm chuột sẽ tạo ra một tầng kích thước mới nằm song song phía trên hoặc phía dưới, cách đều nhau một khoảng cố định.

![DIMCONTINUE và DIMBASELINE](media/ac-05-02-baseline-continue.svg)

```hotspots
image: media/ac-05-02-baseline-continue.svg
alt: So sánh hai phương pháp đo kích thước hàng loạt
layout: central
points:
  - id: spot-1
    x: 26
    y: 36
    title: Kích thước nối tiếp (DIMCONTINUE)
    text: Các đoạn kích thước nối đuôi nhau trên cùng một đường gióng thẳng hàng.
  - id: spot-2
    x: 74
    y: 36
    title: Kích thước song song (DIMBASELINE)
    text: Tất cả kích thước xuất phát từ một mốc chuẩn chung bên trái.
  - id: spot-3
    x: 74
    y: 65
    title: Khoảng cách tầng (Baseline Spacing)
    text: Khoảng cách đều đặn giữa các tầng kích thước song song, khuyên dùng từ 8mm đến 10mm.
```

## Cách dùng từng bước

### 1. Tạo chuỗi kích thước nối tiếp với DIMCONTINUE
1. Tạo một đường kích thước cơ sở đầu tiên bằng lệnh `DIMLINEAR` (ví dụ đo đoạn tường đầu tiên dài 1500mm).
2. Gõ `DCO` hoặc `DIMCONTINUE` rồi nhấn [Enter].
3. AutoCAD sẽ tự động bắt đầu từ điểm thứ hai của kích thước vừa tạo. Bạn chỉ việc di chuột và bấm lần lượt vào các điểm tiếp theo: mép cửa sổ, mép cột, góc phòng.
4. Mỗi cú bấm chuột tạo ra ngay một đoạn kích thước mới nối tiếp thẳng tắp.
5. Nhấn [Enter] hoặc [Esc] để kết thúc lệnh.

*(Mẹo: Nếu muốn tiếp tục từ một kích thước khác trên bản vẽ, nhấn [Enter] khi lệnh đang chạy để chuyển sang chế độ `Select`, sau đó bấm chọn đường kích thước mong muốn).*

### 2. Tạo kích thước song song với DIMBASELINE
1. Tạo một đường kích thước chuẩn ban đầu bằng `DIMLINEAR` (ví dụ đo bậc trục thứ nhất 25mm).
2. Gõ `DBA` hoặc `DIMBASELINE` rồi nhấn [Enter].
3. Bấm lần lượt vào các điểm mốc tiếp theo trên trục (bậc hai 60mm, bậc ba 110mm, chiều dài tổng 180mm).
4. Các đường kích thước tự động xếp tầng ngăn nắp, cách nhau đúng khoảng cách chuẩn.
5. Nhấn [Enter] hai lần để thoát lệnh.

## Tuỳ chọn và mẹo kiểm soát khoảng cách tầng

Khoảng cách giữa các đường kích thước xếp tầng trong `DIMBASELINE` được quy định bởi biến hệ thống `DIMDLI` (Dimension Line Increment).
- Nếu khoảng cách quá nhỏ (dưới 6mm), chữ số của tầng dưới có thể bị đè lên đường gióng của tầng trên.
- Trong hộp thoại `DIMSTYLE`, thẻ **Lines** > ô **Baseline spacing**, nên đặt giá trị từ `8` đến `10` mm (đối với bản vẽ cơ khí) hoặc tương ứng với tỉ lệ in ấn.

> [!TIP]
> Bạn có thể kết hợp cả hai kiểu: Đặt một hàng `DIMCONTINUE` ở tầng dưới để đo chi tiết từng ô cửa sổ, và đặt một đường `DIMLINEAR` hoặc `DIMBASELINE` ở tầng trên để đo kích thước phủ bì toàn bộ căn nhà.

> [!TIP]
> Nếu lỡ bấm nhầm điểm trong lúc chạy chuỗi, hãy nhấn [Ctrl + Z] ngay trong lệnh để lùi lại một bước đo mà không làm hỏng toàn bộ chuỗi kích thước đã đo.

## Tự kiểm tra

```quiz
id: q-ac-05-02-1
type: single
question: "Để bắt đầu sử dụng DIMCONTINUE (DCO), điều kiện bắt buộc trước đó là gì?"
options:
  - text: "Bản vẽ phải có sẵn ít nhất một đường kích thước tuyến tính hoặc góc làm gốc"
    correct: true
    why: "DIMCONTINUE cần một kích thước có sẵn để lấy đường gióng làm điểm nối tiếp."
  - text: "Phải chuyển bản vẽ sang không gian 3D"
    correct: false
    why: "DIMCONTINUE hoạt động trong không gian bản vẽ 2D thông thường."
  - text: "Phải biến toàn bộ hình vẽ thành một khối Block"
    correct: false
    why: "Ghi kích thước không yêu cầu đối tượng phải là Block."
  - text: "Phải tắt toàn bộ chế độ truy bắt điểm Osnap"
    correct: false
    why: "Cần bật Osnap để bắt các điểm đo tiếp theo chính xác."
explain: "Nếu trên bản vẽ chưa có kích thước nào, lệnh DIMCONTINUE sẽ yêu cầu bạn chọn một kích thước cơ sở để tiếp tục."
```

```quiz
id: q-ac-05-02-2
type: single
question: "Biến hệ thống hoặc thông số nào quyết định khoảng cách giữa các tầng kích thước song song trong DIMBASELINE?"
options:
  - text: "Baseline spacing (biến DIMDLI)"
    correct: true
    why: "DIMDLI (Dimension Line Increment) điều chỉnh cự ly tầng giữa các đường kích thước song song."
  - text: "Biến LTSCALE"
    correct: false
    why: "LTSCALE điều chỉnh tỉ lệ nét đứt của đường linetype."
  - text: "Biến TEXTSIZE"
    correct: false
    why: "TEXTSIZE chỉ chỉnh chiều cao chữ viết rời."
  - text: "Biến OFFSETDIST"
    correct: false
    why: "OFFSETDIST dùng cho lệnh OFFSET đường nét."
explain: "Baseline spacing trong thẻ Lines của Dimstyle quy định khoảng cách nhảy tầng giữa các đường đo song song."
```

```quiz
id: q-ac-05-02-3
type: truefalse
question: "Trong khi đang chạy lệnh DIMCONTINUE, bạn có thể nhấn Enter để chọn tiếp tục từ một đường kích thước khác ở vị trí xa hơn."
answer: false
explain: "Nhấn Enter chuyển con trỏ chuột sang ô vuông cho phép bạn bấm chọn bất kỳ đường kích thước nào đang có trên bản vẽ để tiếp tục kéo chuỗi."
```

## Lỗi thường gặp

- **Chuỗi kích thước chạy ngược hướng:** Đường kích thước nối tiếp nhảy về phía trái thay vì sang phải. Nguyên nhân là do khi tạo kích thước cơ sở, điểm thứ hai bạn bấm nằm ở bên trái. Cách sửa: Nhấn [Enter] trong lệnh `DIMCONTINUE` để chọn lại mốc gióng ở phía bên phải.
- **Chữ số kích thước tầng trên đè lên số tầng dưới:** Giá trị `Baseline spacing` bị đặt quá nhỏ (ví dụ 0 hoặc 2mm). Khắc phục bằng cách vào hộp thoại `DIMSTYLE`, thẻ `Lines`, sửa `Baseline spacing` thành `8` hoặc `10`.
- **Đường gióng bị lệch khỏi hàng:** Vô tình kéo chuột lệch khỏi phương thẳng hàng hoặc không dùng truy bắt điểm chính xác.

## Bài tập thực hành

- [ ] Vẽ 4 đường thẳng đứng cách nhau lần lượt 30mm, 45mm, 60mm bằng `LINE` hoặc `OFFSET`. <!-- expect: LINE -->
- [ ] Dùng `DIMLINEAR` đo khoảng cách giữa đường thứ nhất và đường thứ hai (30mm). <!-- expect: DIMLINEAR -->
- [ ] Gõ `DIMCONTINUE` (hoặc `DCO`), bấm lần lượt vào đường thứ ba và thứ tư để tạo chuỗi đo liên tục 45mm và 60mm. <!-- expect: DIMCONTINUE -->
- [ ] Dùng `DIMBASELINE` (hoặc `DBA`), chọn điểm gốc ban đầu và đo song song tổng cự ly từ vạch 1 đến vạch 3 (75mm) và đến vạch 4 (135mm). <!-- expect: DIMBASELINE -->

## Nguồn tham khảo

```links
- title: "Tài liệu lệnh DIMCONTINUE từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=DIMCONTINUE"
  kind: official
- title: "Tài liệu lệnh DIMBASELINE từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=DIMBASELINE"
  kind: official
```
