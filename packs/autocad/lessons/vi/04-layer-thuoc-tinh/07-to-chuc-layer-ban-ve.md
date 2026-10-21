---
id: ac-04-07
title: Quy chuẩn tổ chức hệ thống Layer cho bản vẽ kỹ thuật
category: Layer & Thuộc tính
tags: [to-chuc-layer, quy-chuan-cad, tieu-chuan-layer, quan-ly-du-an]
level: beginner
minutes: 20
needs: [ac-04-01, ac-04-03, ac-04-06]
appVersions: ['2024', '2025']
edition: all
---
# Quy chuẩn tổ chức hệ thống Layer cho bản vẽ kỹ thuật

> **Mục tiêu:**
> - Xây dựng bảng quy chuẩn hệ thống Layer hoàn chỉnh theo tiêu chuẩn TCVN và ISO cho bản vẽ cơ khí và kiến trúc.
> - Thiết lập nguyên tắc đặt tên Layer có tiền tố phân cấp chuyên nghiệp, dễ tra cứu và dễ lọc.
> - Đồng bộ hoá bộ thuộc tính Màu - Kiểu nét - Độ dày phục vụ công tác xuất hồ sơ in ấn sắc nét.

## Lệnh này làm gì và khi nào dùng

Một bản vẽ kỹ thuật chuyên nghiệp được đánh giá không chỉ qua hình vẽ đẹp mà trước hết qua **cách tổ chức hệ thống Layer**. Khi một kỹ sư khác mở file của bạn lên, nếu họ thấy tên layer là `layer1`, `layer2`, `111`, `net_ve` với màu sắc gán lộn xộn, bản vẽ đó sẽ bị đánh giá là thiếu chuyên nghiệp và không thể sử dụng để phối hợp dự án.

Ngược lại, một hệ thống [[Lớp bản vẽ]] quy chuẩn tuân theo nguyên tắc:
1. **Có tiền tố phân ngành:** Ví dụ `CK-` (Cơ khí), `KT-` (Kiến trúc), `KC-` (Kết cấu), `D-` (Điện).
2. **Có tên chức năng rõ ràng:** `Net-Thay`, `Net-Khuat`, `Net-Truc`, `Kich-Thuoc`, `Ghi-Chu`, `Khung-Ten`, `Mat-Cat`.
3. **Màu sắc và độ dày nét phân cấp tương phản:** Nét chính in đậm để làm nổi bật hình dáng, nét phụ in mảnh để không đè chữ số kích thước.

## Cách dùng từng bước

Bảng quy chuẩn hệ thống Layer cơ bản đề xuất cho một bộ hồ sơ thiết kế cơ khí / kiến trúc tiêu chuẩn:

| Tên Layer | Màu sắc (Color) | Kiểu nét (Linetype) | Độ dày nét in (Lineweight) | Chức năng quy ước |
|---|---|---|---|---|
| `01_NET_THAY` | White (Trắng) | `Continuous` | `0.35 mm` | Đường bao thấy, cạnh thấy của chi tiết |
| `02_NET_KHUAT` | Yellow (Vàng) | `HIDDEN` | `0.18 mm` | Cạnh khuất, đường bao bị che khuất |
| `03_NET_TRUC` | Red (Đỏ) | `CENTER` | `0.15 mm` | Đường tâm, trục đối xứng của chi tiết |
| `04_KICH_THUOC` | Cyan (Xanh lơ) | `Continuous` | `0.13 mm` | Đường kích thước, đường gióng và mũi tên |
| `05_GHI_CHU` | Green (Xanh lá) | `Continuous` | `0.18 mm` | Chữ viết ghi chú yêu cầu kỹ thuật |
| `06_MAT_CAT` | Color 8 (Xám) | `Continuous` | `0.13 mm` | Hoa văn mặt cắt Hatch vật liệu |
| `07_KHUNG_TEN` | Magenta (Tím) | `Continuous` | `0.50 mm` | Đường viền khung bản vẽ và khung tên |
| `Defpoints` | Mặc định | `Continuous` | `Default` | Layer hệ thống (không bao giờ in ra giấy) |

### Các bước thiết lập nhanh cho bản vẽ mới:
1. Mở bản vẽ trắng hoặc mở bảng `LAYER` (`LA`).
2. Bấm tạo lần lượt 7 layer theo đúng danh sách bảng chuẩn ở trên.
3. Gán đúng Color, Linetype và Lineweight cho từng lớp. Đảm bảo mọi thứ luôn là [[Thuộc tính ByLayer]].
4. Sau khi thiết lập xong một lần hoàn chỉnh, lưu file thành mẫu template `.dwt` (ví dụ `TCVN_CoKhi.dwt`) để dùng mãi mãi cho mọi dự án sau này mà không bao giờ phải tạo lại từ đầu!

## Tuỳ chọn và mẹo

> [!TIP]
> Sử dụng số thứ tự `01_`, `02_` ở đầu tên layer: Bảng Layer trong AutoCAD sắp xếp theo thứ tự bảng chữ cái alphabet. Đánh số thứ tự giúp các layer quan trọng nhất luôn nằm ngay ngắn ở trên cùng danh sách.

> [!TIP]
> **Layer Defpoints:** Là layer đặc biệt tự sinh ra khi bạn ghi kích thước đầu tiên. Mọi thứ vẽ trên layer Defpoints sẽ **không bao giờ bị in ra giấy**. Người vẽ chuyên nghiệp thường tận dụng Defpoints để vẽ các đường gióng phụ, ghi chú nội bộ mà không sợ bị lộ khi in hồ sơ.

## Tự kiểm tra

```quiz
id: q-ac-04-07-1
type: single
question: Trong tiêu chuẩn bản vẽ kỹ thuật, tỷ lệ độ dày nét giữa "đường bao thấy" (nét đậm) và "đường kích thước / nét gióng" (nét mảnh) thường có tỷ lệ chênh lệch tối thiểu là bao nhiêu?
options:
  - text: Khoảng 2:1 (nét thấy đậm gấp đôi nét mảnh)
    correct: true
    why: Quy chuẩn TCVN và ISO yêu cầu nét đậm phải gấp khoảng 2 lần nét mảnh để tạo độ tương phản rõ ràng
  - text: Bằng nhau (1:1)
    why: Bằng nhau sẽ làm bản vẽ bị dính nét, rối rắm khó đọc
  - text: Nét kích thước đậm hơn nét thấy
    why: Kích thước đậm hơn sẽ lấn át hình học chính
  - text: Nét thấy đậm gấp 10 lần nét mảnh
    why: Chênh lệch quá lớn làm nét thấy bị nhoè mực
explain: "Theo tiêu chuẩn ISO 128 và TCVN, tỷ lệ độ rộng giữa nét đậm và nét mảnh luôn là 2:1 (ví dụ nét thấy chọn 0.35mm thì nét kích thước và đường tâm chọn 0.15 - 0.18mm)."
tags: [to-chuc-layer, lineweight, tieu-chuan]
```

```quiz
id: q-ac-04-07-2
type: single
question: Layer "Defpoints" trong AutoCAD có đặc tính kỹ thuật đặc biệt nào dưới đây?
options:
  - text: Mọi đối tượng vẽ trên layer Defpoints sẽ không bao giờ được in ra giấy (Non-printable)
    correct: true
    why: Defpoints là layer cố định không in của hệ thống kích thước AutoCAD
  - text: Tự động đổi màu sau mỗi 10 phút
    why: Defpoints không tự đổi màu
  - text: Luôn luôn có màu đỏ
    why: Màu của Defpoints có thể đổi được
  - text: Tự động xoá đối tượng khi lưu file
    why: Defpoints lưu giữ đối tượng bình thường
explain: "Layer Defpoints (Definition Points) là layer hệ thống tự sinh ra cùng với kích thước Dimension, có đặc tính cố định là không bao giờ xuất hiện khi in ấn hay xuất PDF."
tags: [layer, defpoints, in-an]
```

```quiz
id: q-ac-04-07-3
type: truefalse
question: Việc lưu một hệ thống layer đã chuẩn hoá thành file mẫu Template (.dwt) giúp bạn tái sử dụng cho mọi dự án sau này mà không cần tạo lại layer từ đầu.
answer: true
explain: "Tạo file template .dwt chứa sẵn hệ thống layer, kiểu chữ và kiểu kích thước chuẩn là phương pháp làm việc thông minh và tiết kiệm thời gian nhất trong AutoCAD."
tags: [template, dwt, quy-chuan]
```

## Lỗi thường gặp

- **Triệu chứng:** In bản vẽ ra giấy thấy nét thấy và nét kích thước đều đậm xì như nhau, rất khó đọc số đo.
  - *Nguyên nhân:* Khi tạo layer đã quên không cài đặt cột *Lineweight* (để mặc định Default cho tất cả các layer).
  - *Cách sửa:* Mở bảng `LAYER`, chỉnh lại độ dày: nét thấy là `0.35 mm`, nét kích thước là `0.13 mm`.
- **Triệu chứng:** Đặt tên layer có dấu tiếng Việt bị lỗi font biến thành các ký tự lạ khi mở trên máy tính khác.
  - *Nguyên nhân:* Tên layer trong AutoCAD không nên chứa ký tự dấu tiếng Việt phức tạp hoặc khoảng trắng để tránh lỗi tương thích khi trao đổi file.
  - *Cách sửa:* Đặt tên layer dạng không dấu nối gạch dưới (ví dụ `NET_THAY`, `KICH_THUOC`, `COT_THEP`).

## Bài tập thực hành

- [ ] Gõ `LAYER` mở bảng Layer Properties Manager. <!-- expect: LAYER -->
- [ ] Tạo layer `01_NET_THAY` (Color: White, Lineweight: 0.35 mm).
- [ ] Tạo layer `02_NET_KHUAT` (Color: Yellow, Linetype: HIDDEN, Lineweight: 0.18 mm).
- [ ] Tạo layer `03_NET_TRUC` (Color: Red, Linetype: CENTER, Lineweight: 0.15 mm).
- [ ] Gõ `LINE` vẽ một đường trục tâm trên layer `03_NET_TRUC` để kiểm tra màu đỏ và kiểu đường gạch chấm. <!-- expect: LINE -->

## Nguồn tham khảo

```links
- title: Tiêu chuẩn tổ chức Layer CAD chuyên nghiệp (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Layer+Standards
  kind: official
  lang: en
  note: Hướng dẫn chính thức về tiêu chuẩn AIA, ISO 13567 và quy chuẩn đặt tên layer
- title: Quản lý độ tương phản đường nét in ấn (Autodesk Support)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Lineweight+Settings
  kind: official
  lang: en
  note: Bảng tra cứu độ dày nét vẽ tiêu chuẩn cho các khổ giấy A4, A3, A1
```
