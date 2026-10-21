---
id: ac-07-07
title: Quản lý hồ sơ dự án và in ấn hàng loạt với Sheet Set Manager
category: Layout và In ấn
tags: [sheetset, publish, batch-plot, in-hang-loat, ssm]
level: advanced
minutes: 30
needs: [ac-07-05, ac-07-06]
appVersions: ['2024', '2025']
edition: all
---
# Quản lý hồ sơ dự án và in ấn hàng loạt với Sheet Set Manager

> **Mục tiêu:**
> - Sử dụng bảng điều khiển Sheet Set Manager (`SHEETSET` / `SSM`) để quản lý tập hợp toàn bộ các trang bản vẽ của một dự án lớn.
> - Tạo bảng danh mục bản vẽ tự động (Sheet List Table) liên kết động với danh sách các trang.
> - Thực hiện lệnh xuất và in ấn hàng loạt (`PUBLISH`) toàn bộ 50 - 100 trang bản vẽ thành 1 file PDF duy nhất chỉ bằng 1 cú nhấp chuột.

## Nỗi ám ảnh in ấn thủ công và giải pháp đỉnh cao Sheet Set

Hãy hình dung một dự án thiết kế chung cư cao tầng:
- Bộ hồ sơ có tổng cộng 80 bản vẽ (Kiến trúc 30 bản vẽ, Kết cấu 25 bản vẽ, Điện nước 25 bản vẽ).
- Các bản vẽ này được phân chia nằm rải rác trong 15 tệp DWG khác nhau.
- Đến ngày nộp bài lúc 5 giờ chiều, sếp yêu cầu: "In cho anh toàn bộ 80 bản vẽ này ra một file PDF duy nhất!".

Nếu làm theo cách thủ công: Bạn sẽ phải mở từng file một, bấm `Ctrl + P`, chọn máy in, bấm Save, rồi lặp lại 80 lần! Bạn sẽ mất đứt 2 tiếng đồng hồ và hoa mắt chóng mặt. Sau đó bạn lại phải lên mạng tìm phần mềm nối 80 file PDF lẻ thành 1 file!

**[[Sheet Set]] Manager (Lệnh tắt `SSM` hoặc `SHEETSET`)** là công cụ quản lý dự án cấp cao nhất của AutoCAD:
- Nó gom toàn bộ các trang Layout từ hàng chục file DWG khác nhau vào chung một cây thư mục duy nhất.
- Tự động đánh số thứ tự trang, tự động cập nhật tên dự án trên toàn bộ các khung tên.
- Tự động xuất **Bảng danh mục bản vẽ (Sheet List Table)**.
- Và với lệnh **`PUBLISH`**, chỉ cần 1 cú click chuột, AutoCAD sẽ âm thầm chạy ngầm và xuất toàn bộ 80 bản vẽ thành **MỘT FILE PDF DUY NHẤT (Multi-page PDF)** hoàn hảo!

## Cách dùng từng bước

### 1. Khởi tạo một bộ Sheet Set mới (SSM)
1. Gõ `SSM` hoặc `SHEETSET` rồi nhấn [Enter]. Bảng **Sheet Set Manager** mở ra bên trái màn hình.
2. Bấm vào menu danh sách xổ xuống trên cùng > chọn **New Sheet Set...**.
3. Cửa sổ thuật sĩ mở ra:
   - Chọn `An example sheet set` (sử dụng mẫu có sẵn) hoặc `Existing drawings` (quét các tệp bản vẽ đã có sẵn). Bấm **Next**.
   - Đặt tên cho bộ hồ sơ: ví dụ `DU-AN-BIET-THU-VUON`.
   - Chọn thư mục lưu file cấu hình `.dst` (file này rất nhẹ, chỉ vài chục KB).
4. Bấm **Next** và duyệt đến thư mục chứa các tệp bản vẽ DWG của dự án.
5. AutoCAD sẽ tự động liệt kê toàn bộ các tab Layout có trong các file DWG đó. Bạn chỉ việc tick chọn những trang cần đưa vào hồ sơ. Bấm **Finish**.

### 2. Tổ chức cây thư mục và danh mục bản vẽ
Trên cây thư mục của Sheet Set Manager:
- Bạn có thể nhấp chuột phải chọn **New Subset** để tạo các nhánh thư mục con: `01_KIEN_TRUC`, `02_KET_CAU`, `03_MEP`.
- Kéo thả các trang bản vẽ vào từng nhánh chuyên môn tương ứng.
- **Tạo bảng danh mục bản vẽ tự động:** Nhấp chuột phải vào tên dự án ở đỉnh cây thư mục > chọn **Insert Sheet List Table...**. Một bảng `Table` danh mục liệt kê đầy đủ: Số thứ tự, Tên bản vẽ, Ngày xuất bản sẽ được chèn ngay ngắn vào trang bìa!

### 3. In ấn hàng loạt (Batch Plot) với lệnh PUBLISH
1. Trong bảng Sheet Set Manager, nhấp chuột phải vào tên dự án trên cùng (hoặc gõ lệnh `PUBLISH`).
2. Menu ngữ cảnh xuất hiện:
   - Rê chuột vào mục **Publish to PDF**.
3. Một hộp thoại hỏi vị trí lưu file PDF xuất hiện: Chọn thư mục lưu và bấm **Select**.
4. AutoCAD sẽ hiển thị một biểu tượng máy in nhỏ nhấp nháy ở góc dưới bên phải màn hình: *"Publish job in progress..."*.
5. Bạn hoàn toàn có thể tiếp tục làm việc khác hoặc lướt web trong khi AutoCAD âm thầm in toàn bộ các trang ở chế độ chạy ngầm (Background Plotting).
6. Khi hoàn tất, một bong bóng thông báo vang lên: *"Plot and Publish Job Complete"*. Mở file PDF ra, toàn bộ 80 trang bản vẽ đã được gom gộp thành một tệp duy nhất, sắc sảo và thứ tự hoàn hảo!

## Tuỳ chọn và mẹo nâng cao hiệu suất

> [!TIP]
> Nhấp đúp chuột vào bất kỳ trang bản vẽ nào trong cây thư mục Sheet Set Manager, AutoCAD sẽ tự động mở tệp DWG chứa trang đó và nhảy thẳng đến tab Layout tương ứng ngay lập tức mà bạn không cần phải lục tìm file trong Windows Explorer!

> [!TIP]
> Khi cần đổi tên dự án từ "Biệt thự ông Hùng" thành "Biệt thự bà Lan": Thay vì đi sửa 80 khung tên, bạn chỉ cần nhấp chuột phải vào tên Sheet Set > chọn **Properties** > sửa tên dự án. Toàn bộ 80 bản vẽ sẽ tự động cập nhật tức thì nhờ các trường `Field` đã liên kết!

## Tự kiểm tra

```quiz
id: q-ac-07-07-1
type: single
question: "Lệnh tắt tiêu chuẩn trong AutoCAD để mở bảng điều khiển quản lý hồ sơ dự án Sheet Set Manager là gì?"
options:
  - text: "SSM (hoặc SHEETSET)"
    correct: true
    why: "SSM là chữ viết tắt của Sheet Set Manager."
  - text: "SET"
    why: "SET không phải lệnh quản lý bản vẽ."
  - text: "PDF"
    why: "PDF không phải alias của Sheet Set."
  - text: "PRINT"
    why: "PRINT mở hộp thoại in PLOT thông thường."
explain: "Gõ SSM là thói quen của mọi quản lý dự án CAD để kiểm soát toàn bộ cây danh mục hồ sơ công trình."
```

```quiz
id: q-ac-07-07-2
type: single
question: "Ưu điểm vượt trội nhất của lệnh PUBLISH khi kết hợp với Sheet Set Manager là gì?"
options:
  - text: "Cho phép xuất toàn bộ hàng chục trang bản vẽ từ nhiều tệp DWG khác nhau thành một file PDF duy nhất ở chế độ chạy ngầm"
    correct: true
    why: "Tính năng Batch Plotting đa tệp giúp tiết kiệm hàng giờ đồng hồ so với việc in thủ công từng trang."
  - text: "Tự động sửa các bức tường bị vẽ cong thành thẳng"
    correct: false
    why: "PUBLISH là lệnh xuất bản vẽ, không can thiệp sửa hình học."
  - text: "Miễn phí toàn bộ tiền giấy in"
    correct: false
    why: "Không liên quan đến chi phí vật tư máy in thực tế."
  - text: "Chỉ in được trên hệ điều hành Linux"
    correct: false
    why: "AutoCAD hoạt động trên nền tảng Windows và macOS."
explain: "Lệnh PUBLISH tự động gom gộp nhiều trang thành tệp Multi-sheet PDF duy nhất mà không đòi hỏi người vẽ phải mở từng file DWG."
```

```quiz
id: q-ac-07-07-3
type: truefalse
question: "Bạn có thể tự động chèn bảng danh mục bản vẽ liên kết động (Sheet List Table) vào trang bìa thông qua Sheet Set Manager."
answer: true
explain: "Tính năng Insert Sheet List Table giúp bảng mục lục bản vẽ luôn tự động cập nhật số trang và tên bản vẽ khi có sự thay đổi trong hồ sơ."
```

## Lỗi thường gặp

- **Chấm than màu vàng hoặc đỏ xuất hiện trên trang bản vẽ trong SSM:** Báo hiệu tệp DWG chứa trang đó đã bị di dời sang thư mục khác ngoài ổ cứng máy tính. Khắc phục: Nhấp chuột phải vào trang đó chọn *Properties* và chỉ định lại đường dẫn tệp mới.
- **In PUBLISH bị chậm hoặc báo lỗi thiếu bộ nhớ:** Do bật quá nhiều phần mềm nặng cùng lúc. Khắc phục: Vào Options thẻ Plot and Publish kiểm tra tùy chọn *Background plotting* được bật để giải phóng tài nguyên.

## Bài tập thực hành

- [ ] Gõ lệnh `SHEETSET` (hoặc `SSM`) để mở bảng điều khiển Sheet Set Manager. <!-- expect: SHEETSET -->
- [ ] Quan sát giao diện và các tuỳ chọn tạo mới Sheet Set trên bảng điều khiển.
- [ ] Gõ lệnh `PUBLISH` để mở hộp thoại xuất bản vẽ hàng loạt. <!-- expect: PUBLISH -->
- [ ] Quan sát danh sách các trang Layout hiện có trong danh sách in hàng loạt.
- [ ] Bấm nút đóng hộp thoại Publish.

## Nguồn tham khảo

```links
- title: "Quản lý dự án với Sheet Set Manager từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Sheet+Sets"
  kind: official
- title: "In hàng loạt với lệnh PUBLISH từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=PUBLISH"
  kind: official
```
