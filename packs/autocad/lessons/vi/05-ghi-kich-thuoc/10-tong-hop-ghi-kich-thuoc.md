---
id: ac-05-10
title: Bài tập tổng hợp ghi kích thước chi tiết cơ khí hoàn chỉnh
category: Ghi kích thước
tags: [tong-hop, dimension, bai-tap, co-khi, tieu-chuan]
level: intermediate
minutes: 30
needs: [ac-05-02, ac-05-04, ac-05-06]
appVersions: ['2024', '2025']
edition: all
---
# Bài tập tổng hợp ghi kích thước chi tiết cơ khí hoàn chỉnh

> **Mục tiêu:**
> - Áp dụng toàn bộ quy trình thiết lập Dimstyle và Text Style theo tiêu chuẩn kỹ thuật Việt Nam.
> - Bố trí hệ thống kích thước chi tiết cơ khí chuẩn xác, không trùng lặp, không thiếu sót.
> - Kết hợp Multileader để chỉ dẫn gia công và chèn bảng kê danh mục vật tư bằng Table.

## Dự án thực tế: Bản vẽ chi tiết gối đỡ trục có rãnh then

Ở các bài trước, bạn đã học từng lệnh ghi kích thước riêng lẻ (`DIMLINEAR`, `DIMALIGNED`, `DIMCONTINUE`, `MLEADER`, `TABLE`). Trong bài học tổng kết chặng này, bạn sẽ vào vai một kỹ sư thiết kế hoàn thiện hồ sơ kỹ thuật cho chi tiết gối đỡ cơ khí.

Một bản vẽ ghi kích thước chuẩn mực cần đạt được 3 tiêu chí vàng:
1. **Đủ thông tin gia công:** Người thợ đứng máy phay, tiện có thể đọc và gia công ngay mà không cần phải lấy thước đo mò trên bản vẽ.
2. **Không trùng lặp:** Không ghi kích thước khép kín vòng tròn (Over-dimensioning) gây mâu thuẫn chuỗi dung sai.
3. **Thẩm mỹ và ngăn nắp:** Kích thước nhỏ nằm trong, kích thước lớn bao ngoài; các đường gióng không cắt chéo nhau một cách hỗn loạn.

![Bản vẽ tổng hợp kích thước chi tiết gối đỡ](media/ac-05-10-tong-hop-dim.svg)

```hotspots
image: media/ac-05-10-tong-hop-dim.svg
alt: Bố cục kích thước chi tiết gối đỡ trục cơ khí
layout: central
points:
  - id: spot-1
    x: 49
    y: 84
    title: Kích thước bao tổng thể (Overall 140mm)
    text: Đo chiều rộng tổng phủ bì của mặt bích đáy bằng DIMLINEAR.
  - id: spot-2
    x: 26
    y: 75
    title: Chuỗi kích thước định vị lỗ (DIMCONTINUE)
    text: Định vị tâm lỗ khoan từ mép trái (20mm) và khoảng cách hai lỗ (100mm).
  - id: spot-3
    x: 18
    y: 45
    title: Chỉ dẫn lỗ bắt bu lông (MLEADER)
    text: Chú thích 2 lỗ khoan Ø12 thông suốt bằng Multileader.
  - id: spot-4
    x: 50
    y: 35
    title: Đo đường kính lỗ trục (DIMDIAMETER)
    text: Đo đường kính trong Ø50 của gối đỡ trục chính.
```

## Quy trình 4 bước hoàn thiện ghi kích thước

### Bước 1: Chuẩn bị hệ thống kiểu (Styles Setup)
- Tạo Text Style chuẩn `TCVN` dùng font `Arial`, chiều cao `0.0`.
- Tạo Dimstyle `TCVN-CO-KHI` dựa trên `ISO-25`:
  - `Arrow size`: 2.5mm.
  - `Text height`: 2.5mm, đặt `Above`, gióng `Aligned with dimension line`.
  - `Baseline spacing`: 8.0mm.
  - `Extend beyond dim lines`: 2.0mm; `Offset from origin`: 2.0mm.
  - `Zero suppression`: Trailing.
- Tạo MLeaderStyle `TCVN-MLD` với mũi tên `Closed filled` 2.5mm.

### Bước 2: Dựng hình chi tiết cơ bản
1. Đáy bích: Hình chữ nhật 140 x 20 mm bằng `RECTANG`.
2. Gối trụ phía trên: Hình chữ nhật 70 x 50 mm gắn trên đỉnh đáy bích.
3. Lỗ trục chính: Hình tròn bán kính 25mm (`CIRCLE`) ngay tâm gối trụ.
4. Lỗ bu lông: 2 hình tròn đường kính 12mm cách 2 mép ngoài 20mm.

### Bước 3: Triển khai đo kích thước theo thứ tự
1. **Đo từ trong ra ngoài:** Đo các kích thước nhỏ bên trong trước (bậc thang, rãnh khuyết).
2. **Kích thước định vị:** Dùng `DIMLINEAR` và `DIMCONTINUE` đo vị trí tâm các lỗ tròn so với mép chuẩn đáy và mép hông.
3. **Kích thước bao ngoài:** Đặt đường đo tổng chiều dài 140mm và tổng chiều cao 70mm ở tầng ngoài cùng, cách tầng trong 10mm.
4. **Kích thước cung tròn:** Đo `DIMRADIUS` cho các góc lượn bo R5 và `DIMDIAMETER` cho lỗ trục chính Ø50.
5. **Ghi chú kỹ thuật:** Dùng `MLEADER` chỉ vào lỗ bắt bu lông ghi: `2x%%c12 Thông suốt`.

### Bước 4: Chèn bảng kê vật tư và kiểm tra
1. Dùng lệnh `TABLE` chèn bảng gồm 3 cột: `STT | Tên chi tiết | Vật liệu`.
2. Điền thông tin: `1 | Thân gối đỡ | Gang xám GX15-32`.
3. Kiểm tra lại toàn bộ bản vẽ: Không có đường gióng nào đè lên số kích thước khác.

## Tuỳ chọn và mẹo kiểm tra bản vẽ trước khi xuất

> [!TIP]
> Sử dụng lệnh `DIMSPACE` để tự động dãn đều khoảng cách giữa các hàng kích thước song song bị lệch tay, giúp bản vẽ đạt tính thẩm mỹ cao nhất mà không cần kéo chuột căn chỉnh bằng mắt.

> [!TIP]
> Luôn khóa layer kích thước (`LAYLCK`) khi bạn muốn chọn lọc di chuyển hoặc chỉnh sửa các nét vẽ hình học, tránh làm xô lệch vị trí các đường kích thước đã gióng thẳng.

## Tự kiểm tra

```quiz
id: q-ac-05-10-1
type: single
question: "Quy tắc bố cục kích thước nào sau đây là CHÍNH XÁC trong bản vẽ kỹ thuật?"
options:
  - text: "Kích thước chi tiết nhỏ đặt ở tầng trong, kích thước bao lớn đặt ở tầng ngoài cùng"
    correct: true
    why: "Quy tắc này giúp các đường gióng không bị cắt chéo ngang qua các đường kích thước khác."
  - text: "Kích thước lớn nhất luôn phải nằm sát đối tượng nhất"
    correct: false
    why: "Nếu để kích thước lớn bên trong, các đường gióng của kích thước nhỏ sẽ cắt ngang qua nó."
  - text: "Phải đo khép kín 100% tất cả các đoạn không được chừa đoạn nào"
    correct: false
    why: "Đo khép kín vòng tròn là lỗi cấm kỵ trong dung sai cơ khí (Over-dimensioning)."
  - text: "Tất cả các kích thước đều phải in màu tím đậm"
    correct: false
    why: "Màu sắc quy định theo tiêu chuẩn công ty hoặc theo chiều dày nét in."
explain: "Luôn sắp xếp kích thước theo thứ tự bậc thang: từ nhỏ đến lớn, từ chi tiết đến bao quát."
```

```quiz
id: q-ac-05-10-2
type: single
question: "Lệnh nào trong AutoCAD giúp tự động căn đều khoảng cách giữa các đường kích thước song song bị lệch tầng?"
options:
  - text: "DIMSPACE"
    correct: true
    why: "DIMSPACE tự động căn chỉnh khoảng cách đều đặn giữa các tầng kích thước tuyến tính hoặc góc."
  - text: "DIMJOGLINE"
    correct: false
    why: "DIMJOGLINE tạo vết gãy dích dắc cho đường kích thước quá dài."
  - text: "DIMOVERRIDE"
    correct: false
    why: "DIMOVERRIDE ghi đè biến hệ thống kích thước."
  - text: "SPACEBAR"
    correct: false
    why: "Phím Spacebar chỉ đóng vai trò tương tự phím Enter."
explain: "Lệnh DIMSPACE là công cụ tuyệt vời để chuẩn hoá cự ly giữa các đường kích thước song song."
```

```quiz
id: q-ac-05-10-3
type: truefalse
question: "Không nên ghi chuỗi kích thước khép kín vòng tròn (Chain dimensioning) trên bản vẽ cơ khí để tránh tích lũy sai số chế tạo."
answer: false
explain: "Trong gia công cơ khí, luôn chừa lại kích thước của một đoạn kém quan trọng nhất để hấp thụ sai số tích lũy của các bước gia công."
```

## Lỗi thường gặp

- **Đường gióng kích thước cắt ngang qua chữ số đo khác:** Bố trí các tầng đo lộn xộn khiến chữ số bị đè nét. Khắc phục: Dùng `DIMTEDIT` hoặc di chuyển grip chữ dời ra vùng thoáng, hoặc dùng lệnh `DIMBREAK` để ngắt đường gióng tại giao điểm.
- **Quên ký hiệu %%c khi đo lỗ tròn:** Khi ghi chú bằng Multileader chỉ gõ số `12` thay vì `Ø12`. Luôn kiểm tra gõ `%%c` trước các kích thước đường kính.

## Bài tập thực hành

- [ ] Tạo bản vẽ mới, vẽ hình bích đáy 140 x 20 mm bằng `RECTANG`. <!-- expect: RECTANG -->
- [ ] Vẽ gối trụ 70 x 50 mm phía trên và lỗ trục bán kính 25mm bằng `CIRCLE`. <!-- expect: CIRCLE -->
- [ ] Dùng `DIMLINEAR` đo chiều rộng đáy 140mm và chiều cao gối trụ 50mm. <!-- expect: DIMLINEAR -->
- [ ] Dùng `DIMDIAMETER` đo đường kính lỗ trục Ø50. <!-- expect: DIMDIAMETER -->
- [ ] Dùng `MLEADER` tạo một ghi chú có mũi tên chỉ vào chi tiết ghi: "Mặt bích gia công mài phẳng Ra 1.6". <!-- expect: MLEADER -->
- [ ] Dùng `TABLE` chèn một bảng thống kê 2 dòng vào góc phải bản vẽ. <!-- expect: TABLE -->

## Nguồn tham khảo

```links
- title: "Quy chuẩn trình bày kích thước kỹ thuật từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=Dimensioning+Standards"
  kind: official
- title: "Lệnh DIMSPACE căn khoảng cách kích thước từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=DIMSPACE"
  kind: official
```
