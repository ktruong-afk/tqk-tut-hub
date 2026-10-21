---
id: ac-04-02
title: Màu sắc, kiểu đường Linetype và độ dày Lineweight
category: Layer & Thuộc tính
tags: [color, linetype, lineweight, mau-sac, kieu-duong, do-day-net]
level: beginner
minutes: 15
needs: [ac-04-01]
appVersions: ['2024', '2025']
edition: all
---
# Màu sắc, kiểu đường Linetype và độ dày Lineweight

> **Mục tiêu:**
> - Sử dụng bảng màu ACI (AutoCAD Color Index) và gán màu sắc trực quan theo tiêu chuẩn kỹ thuật.
> - Nạp thêm các kiểu đường nét (Linetype) như Hidden, Center, Phantom từ tệp thư viện `acadiso.lin`.
> - Cài đặt độ dày nét in (Lineweight) và bật chế độ hiển thị độ dày nét thực trên màn hình (LWT).

## Lệnh này làm gì và khi nào dùng

Một bản vẽ kỹ thuật đạt chuẩn không bao giờ là một mớ đường nét trắng đồng nhất. Để mắt người có thể phân biệt được đâu là đường bao thấy, đâu là đường tâm, đâu là nét khuất bên trong vật thể, bản vẽ cần 3 yếu tố nhận diện:
1. **Màu sắc (Color):** Phân biệt đối tượng trên màn hình máy tính (giúp người vẽ đỡ mỏi mắt và phân biệt hạng mục).
2. [[Kiểu đường nét]] (Linetype): Thể hiện quy ước bản vẽ quốc tế:
   - `Continuous`: Đường nét liền (đường bao thấy, khung viền).
   - `Hidden` / `Dashed`: Đường nét đứt (cạnh khuất, lỗ khuất bên trong).
   - `Center`: Đường nét gạch chấm (đường tâm, trục đối xứng của hình tròn, ống trụ).
   - `Phantom`: Đường nét hai chấm gạch (vị trí chuyển động giới hạn, đường bao phôi).
3. [[Độ dày nét]] (Lineweight): Thể hiện chiều rộng thực của nét khi in ra giấy: nét thấy in đậm (0.35 - 0.50mm), nét khuất in vừa (0.18 - 0.25mm), đường gióng kích thước in mảnh (0.13 - 0.15mm).

```hotspots
image: media/ac-04-01-layer-manager.svg
alt: Sơ đồ cấu hình các cột Color, Linetype và Lineweight trong bảng Layer Properties Manager
layout: central
points:
  - id: col-color
    x: 55
    y: 40
    title: Cột Màu sắc (Color)
    text: Bảng 255 màu chuẩn ACI. Thường quy ước Red cho nét trục, Yellow cho nét khuất, White cho nét thấy.
    quiz: q-ac-04-02-1
  - id: col-linetype
    x: 70
    y: 40
    title: Cột Kiểu đường (Linetype)
    text: Chọn kiểu nét Continuous, Hidden, Center từ tệp acadiso.lin.
    quiz: q-ac-04-02-2
  - id: col-lineweight
    x: 88
    y: 40
    title: Cột Độ dày nét (Lineweight)
    text: Đặt bề dày tính bằng mm (0.15mm đến 0.50mm) quyết định độ đậm nhạt khi in bản vẽ.
```

## Cách dùng từng bước

1. **Nạp thêm kiểu đường nét mới (LINETYPE):**
   - Mặc định bản vẽ mới chỉ có sẵn 1 kiểu đường duy nhất là `Continuous` (nét liền).
   - Gõ lệnh `LINETYPE` hoặc phím tắt `LT` rồi nhấn [Enter]. Hộp thoại *Linetype Manager* xuất hiện.
   - Bấm vào nút **Load...**
   - Một danh sách kiểu đường từ file `acadiso.lin` hiện ra. Cuộn chuột tìm:
     - Chọn `CENTER` (hoặc `CENTER2` nét dày hơn) cho đường tâm trục.
     - Đè giữ phím [Ctrl] và chọn thêm `HIDDEN` (hoặc `HIDDEN2`) cho nét khuất.
   - Bấm **OK** để nạp chúng vào bản vẽ.
2. **Gán kiểu đường vào Layer:**
   - Mở bảng `LAYER` (`LA`), nhấp vào ô Linetype của layer cần gán (ví dụ layer `Net-Truc`).
   - Chọn kiểu đường `CENTER` vừa nạp rồi bấm OK.
3. **Cài đặt độ dày nét vẽ (LINEWEIGHT):**
   - Gõ `LINEWEIGHT` hoặc phím tắt `LW` rồi nhấn [Enter].
   - Tích chọn ô **Display Lineweight** (Hiển thị độ dày nét). Nếu không tích ô này, trên màn hình mọi nét vẽ sẽ hiển thị mảnh như nhau (chỉ khi in mới thấy đậm nhạt).
   - Nhấn **OK**.
4. **Bật tắt nhanh hiển thị độ dày nét:**
   - Trên thanh trạng thái ở đáy màn hình, tìm biểu tượng **Show/Hide Lineweight** (hình các vạch kẻ ngang đậm nhạt) để bật tắt tức thời.

## Tuỳ chọn và mẹo

> [!TIP]
> Luôn nạp kiểu đường nét từ file mẫu hệ mét `acadiso.lin` (chứ không phải `acad.lin`). Kiểu đường của `acadiso.lin` được thiết kế tỷ lệ khoảng cách gạch chấm chuẩn xác theo milimet.

> [!TIP]
> Khi vẽ chi tiết dày đặc, hãy tắt biểu tượng hiển thị độ dày nét Lineweight trên thanh trạng thái để các nét đậm không đè che mất các điểm bắt điểm hình học nhỏ.

## Tự kiểm tra

```quiz
id: q-ac-04-02-1
type: single
question: Khi bản vẽ mới khởi tạo chỉ có sẵn duy nhất kiểu đường nét liền Continuous, bạn cần làm gì để có thể sử dụng kiểu đường nét đứt HIDDEN và đường tâm CENTER?
options:
  - text: Dùng lệnh LINETYPE và bấm nút "Load" để nạp thêm kiểu đường từ thư viện acadiso.lin
    correct: true
    why: AutoCAD yêu cầu phải Load các kiểu đường nét từ tệp thư viện .lin vào bản vẽ
  - text: Tự vẽ từng nét đứt bằng tay bằng lệnh LINE
    why: Không ai vẽ nét đứt thủ công vì sẽ mất hàng giờ và sai tiêu chuẩn
  - text: Cài đặt lại phần mềm AutoCAD
    why: Thư viện kiểu đường có sẵn trong phần mềm, không cần cài lại
  - text: Đổi màu đường thẳng sang màu vàng
    why: Đổi màu không làm đổi kiểu đường nét
explain: "Mặc định để tiết kiệm dung lượng, AutoCAD chỉ nạp sẵn nét Continuous. Người dùng cần vào Linetype Manager (lệnh LT) và bấm Load để tải các mẫu Hidden và Center vào bản vẽ."
tags: [linetype, load, hidden, center]
```

```quiz
id: q-ac-04-02-2
type: single
question: Đã gán độ dày nét vẽ Lineweight là 0.50mm cho layer nét thấy nhưng trên màn hình các nét vẽ trông vẫn mảnh như sợi chỉ. Nguyên nhân là gì?
options:
  - text: Chế độ hiển thị độ dày nét (Display Lineweight / nút LWT) đang bị tắt trên thanh trạng thái
    correct: true
    why: Phải bật Display Lineweight thì màn hình đồ hoạ mới hiển thị độ đậm nhạt thực tế
  - text: Máy tính bị hỏng card màn hình
    why: Đây là tính năng hiển thị mặc định của AutoCAD để tránh rối mắt
  - text: Layer bị đóng băng Freeze
    why: Đóng băng thì nét sẽ biến mất hoàn toàn
  - text: Nhập nhầm đơn vị milimet thành mét
    why: Lineweight luôn đo bằng milimet
explain: "Mặc định AutoCAD tắt chế độ hiển thị độ dày nét để màn hình vẽ sắc nét, dễ bắt điểm. Bạn chỉ cần bấm nút Show/Hide Lineweight trên thanh trạng thái hoặc gõ lệnh LINEWEIGHT và tích ô Display Lineweight."
tags: [lineweight, hien-thi, lwt]
```

```quiz
id: q-ac-04-02-3
type: truefalse
question: Kiểu đường CENTER trong bản vẽ kỹ thuật được quy ước dùng để biểu diễn đường tâm và trục đối xứng của các chi tiết hình trụ, lỗ tròn.
answer: true
explain: "Quy chuẩn vẽ kỹ thuật quốc tế (ISO) và Việt Nam (TCVN) đều quy định đường nét gạch chấm mảnh (CENTER) dùng để chỉ vị trí trục đối xứng và tâm đường tròn."
tags: [linetype, center, tieu-chuan]
```

## Lỗi thường gặp

- **Triệu chứng:** Đã chọn kiểu đường HIDDEN nhưng đường thẳng trên màn hình nhìn vẫn liền tù tì như nét thẳng thông thường.
  - *Nguyên nhân:* Tỷ lệ kiểu đường `LTSCALE` đang quá lớn hoặc quá bé so với chiều dài đoạn thẳng, khiến các khoảng gạch đứt không hiển thị vừa mắt nhìn.
  - *Cách sửa:* Gõ lệnh `LTSCALE` và thay đổi hệ số tỷ lệ phù hợp (sẽ học kỹ ở bài 04-ltscale).
- **Triệu chứng:** Màn hình hiển thị các nét vẽ dày cộm che kín cả hình, rất khó nhìn thấy các góc chi tiết.
  - *Nguyên nhân:* Tính năng Display Lineweight đang bật và con trỏ trượt điều chỉnh tỷ lệ hiển thị trong hộp thoại LINEWEIGHT đang kéo về mức tối đa.
  - *Cách sửa:* Gõ `LINEWEIGHT`, kéo thanh trượt *Adjust Display Scale* về mức trung bình hoặc tắt nút hiển thị độ dày nét trên thanh trạng thái khi đang vẽ dựng hình.

## Bài tập thực hành

- [ ] Gõ `LINETYPE` (hoặc `LT`) để mở bảng Linetype Manager. <!-- expect: LINETYPE -->
- [ ] Bấm nút **Load...**, chọn kiểu đường `CENTER` và `HIDDEN` rồi bấm OK để nạp vào bản vẽ.
- [ ] Gõ `LINEWEIGHT` (hoặc `LW`), tích chọn ô *Display Lineweight* để bật hiển thị độ dày nét thực tế trên màn hình. <!-- expect: LINEWEIGHT -->
- [ ] Gõ `COLOR`, chọn thử màu số 1 (Red) rồi vẽ một đoạn thẳng bằng lệnh `LINE`. <!-- expect: LINE -->

## Nguồn tham khảo

```links
- title: Lệnh LINETYPE và quản lý kiểu đường nét (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=LINETYPE+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về nạp kiểu đường từ file acadiso.lin và tạo kiểu đường tuỳ biến
- title: Lệnh LINEWEIGHT và kiểm soát độ dày nét in (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=LINEWEIGHT+Command
  kind: official
  lang: en
  note: Hướng dẫn cài đặt độ dày nét hiển thị và quy chuẩn in ấn bản vẽ
```
