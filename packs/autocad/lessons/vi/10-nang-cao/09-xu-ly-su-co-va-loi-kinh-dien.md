---
id: ac-10-09
title: "Xử lý sự cố và các lỗi kinh điển trong AutoCAD"
category: Nâng cao và Tự động hoá
tags: [su-co, sua-loi, font-shx, xref, audit, recover, kinh-nghiem]
level: advanced
minutes: 25
needs: [ac-08-04]
appVersions: ['2024', '2025']
edition: all
---
# Xử lý sự cố và các lỗi kinh điển trong AutoCAD

> **Mục tiêu:**
> - Nhận diện nguyên nhân gốc rễ và xử lý triệt để các lỗi kỹ thuật phổ biến nhất: Chữ biến thành dấu `???`, mất thanh dòng lệnh, hộp thoại mở file không hiện ra, và nét đứt biến thành nét liền.
> - Làm chủ các biến hệ thống "cứu nguy" quan trọng nhất của AutoCAD (`FILEDIA`, `PICKFIRST`, `LTSCALE`, `ANNOALLVISIBLE`).
> - Nắm vững quy trình phục hồi bản vẽ bị hỏng hoặc bị văng đột ngột (Crash / Fatal Error) bằng bộ ba lệnh `AUDIT`, `RECOVER` và công cụ khôi phục sao lưu tự động.

## Lỗi 1: Chữ tiếng Việt biến thành dấu hỏi `???` hoặc ô vuông

Đây là lỗi phổ biến nhất khi bạn mở một bản vẽ nhận từ đối tác hoặc cơ quan thẩm tra:

- **Hiện tượng**: Toàn bộ ghi chú, cao độ, kích thước biến thành hàng loạt dấu `????????` hoặc các ký tự kỳ lạ.
- **Nguyên nhân**: Bản vẽ sử dụng các phông chữ dạng đơn dòng kỹ thuật của AutoCAD (đuôi tệp `.shx`, ví dụ `vntime.shx`, `vn_vni.shx`, `cadfont.shx`) mà trên máy tính của bạn chưa được chép vào thư mục Fonts của phần mềm.
- **Cách xử lý đúng**:
  1. Khi mở file, nếu AutoCAD hiện hộp thoại cảnh báo `Missing SHX Files`, hãy nhìn kỹ tên tệp phông chữ bị thiếu.
  2. Xin người gửi tệp phông chữ `.shx` tương ứng và chép vào thư mục: `C:\Program Files\Autodesk\AutoCAD 2025\Fonts\`.
  3. Khởi động lại AutoCAD và gõ lệnh `REGEN` để tải lại màn hình.
  4. Nếu không thể xin lại phông, mở bảng kiểu chữ `STYLE` $\to$ chọn kiểu chữ đang bị lỗi $\to$ đổi phông chữ sang phông TrueType quốc tế phổ thông như `Arial` hoặc `Times New Roman`.

## Lỗi 2: Mất dòng lệnh hoặc hộp thoại mở file không xuất hiện (`FILEDIA`)

Đôi khi sau khi cài lại máy, chạy một lisp lạ, hoặc vô tình bấm nhầm phím tắt, bạn sẽ gặp hai hiện tượng "dở khóc dở cười":

### 1. Bấm Open / Save nhưng không thấy hộp thoại duyệt file
- **Hiện tượng**: Bạn gõ lệnh `OPEN` hoặc bấm `Ctrl + O` nhưng không có cửa sổ chọn file hiện ra, mà dòng lệnh bên dưới lại yêu cầu gõ đường dẫn bằng chữ: `Enter name of drawing to open:`.
- **Nguyên nhân**: Biến hệ thống `FILEDIA` (File Dialogue) bị chuyển từ giá trị `1` (bật hộp thoại) về `0` (tắt hộp thoại). Rất nhiều lisp cũ thường tắt biến này khi chạy nhưng khi gặp lỗi giữa chừng thì quên không bật lại.
- **Cách sửa**: Gõ trực tiếp trên bàn phím: `FILEDIA` $\to$ nhấn [Enter] $\to$ nhập giá trị `1` $\to$ nhấn [Enter]. Hộp thoại sẽ lập tức hoạt động lại bình thường!

### 2. Dòng lệnh Command Line biến mất hoàn toàn
- **Hiện tượng**: Dưới đáy màn hình không còn thanh gõ lệnh, không biết phần mềm đang ở bước nào.
- **Cách sửa**: Nhấn tổ hợp phím kinh điển **[Ctrl + 9]** (bật/tắt thanh Command Line) hoặc gõ lệnh `COMMANDLINE`.

## Lỗi 3: Đối tượng biến mất hoặc không chọn được trước khi gọi lệnh (`PICKFIRST`)

### 1. Phải gõ lệnh trước mới được chọn đối tượng
- **Hiện tượng**: Bạn quét chọn một đối tượng rồi nhấn phím [Delete] hoặc gõ lệnh `MOVE`, nhưng đối tượng bỗng bị bỏ chọn và AutoCAD lại hỏi `Select objects:`.
- **Nguyên nhân**: Biến hệ thống `PICKFIRST` (cho phép chọn trước khi gọi lệnh) bị đổi giá trị thành `0`.
- **Cách sửa**: Gõ `PICKFIRST` $\to$ nhấn [Enter] $\to$ nhập `1` $\to$ nhấn [Enter].

### 2. Kích thước và chữ biến mất khi đổi tỉ lệ bản vẽ
- **Hiện tượng**: Chữ và đường gióng kích thước trong Model bỗng biến mất khi bạn chuyển tỉ lệ hiển thị ở thanh trạng thái.
- **Nguyên nhân**: Đối tượng đó được gán thuộc tính [[Annotative]] nhưng chưa được thêm tỉ lệ hiện hành, trong khi chế độ hiển thị mọi kích thước đang bị tắt.
- **Cách sửa**: Gõ biến hệ thống `ANNOALLVISIBLE` $\to$ nhập `1` để ép AutoCAD hiển thị toàn bộ đối tượng Annotative dù ở bất kỳ tỉ lệ nào.

## Lỗi 4: Đường nét đứt (Hidden/Center) hiển thị thành đường liền mạch

- **Hiện tượng**: Bạn đã gán linetype là `HIDDEN` hoặc `CENTER` nhưng trên màn hình (hoặc sang bên trang Layout) các đường nét vẫn thẳng đuột như nét liền `Continuous`.
- **Nguyên nhân**: Hệ số tỉ lệ hiển thị nét vẽ `LTSCALE` quá lớn hoặc quá nhỏ so với kích thước thực tế của công trình; hoặc tỉ lệ nét bên Layout không đồng bộ với tỉ lệ Viewport.
- **Cách sửa**:
  1. Gõ lệnh `LTSCALE` $\to$ thử điều chỉnh giá trị lên (ví dụ `10`, `50`) hoặc giảm xuống (ví dụ `0.1`, `0.01`) rồi gõ `REGEN` để quan sát khoảng hở nét đứt.
  2. Đối với trang in ấn Layout: Gõ lệnh `PSLTSCALE` $\to$ đặt giá trị bằng `1` để tỉ lệ nét đứt tự động quy đổi đồng nhất theo tỉ lệ của từng cổng nhìn Viewport.

## Lỗi 5: Bản vẽ bị crash, báo Fatal Error và quy trình cấp cứu phục hồi

Khi AutoCAD bị đóng đột ngột (Fatal Error / Crash) do mất điện hoặc xung đột phần cứng:

```
[ Sự cố sập phần mềm ]
          │
          ▼
   1. Kiểm tra Drawing Recovery Manager (Lệnh DRAWINGRECOVERY)
          │
          ▼
   2. Tìm tệp tự lưu trong Temp: %TEMP% (Đổi đuôi .sv$ thành .dwg)
          │
          ▼
   3. Mở file sao lưu lân cận: Đổi đuôi .bak thành .dwg
          │
          ▼
   4. Quét sửa lỗi cấu trúc: Lệnh RECOVER và AUDIT
          │
          ▼
   5. Thanh lọc tệp rác: Lệnh PURGE
```

1. **Khôi phục từ tệp sao lưu `.bak`**:
   - Ngay tại thư mục chứa file vẽ, AutoCAD luôn tạo một tệp có cùng tên nhưng mang đuôi mở rộng `.bak`. Đây chính là trạng thái của bản vẽ ở lần lưu thủ công gần nhất trước đó.
   - Bạn chỉ cần đổi tên đuôi từ `.bak` thành `.dwg` là có thể mở lại bình thường.
2. **Khôi phục từ tệp tự lưu Autosave `.sv$`**:
   - Vào hộp thoại cài đặt `OPTIONS` $\to$ thẻ **Files** $\to$ kiểm tra đường dẫn thư mục `Automatic Save File Location` (mặc định là thư mục tạm `%temp%`).
   - Vào thư mục đó, tìm tệp có đuôi `.sv$` có ngày giờ gần nhất $\to$ đổi đuôi thành `.dwg`.
3. **Sửa chữa file lỗi cấu trúc dữ liệu**:
   - Dùng lệnh `RECOVER`: Mở trực tiếp và quét phục hồi các khối dữ liệu bị hỏng trong tệp DWG.
   - Sau khi đã mở được file, luôn chạy tiếp lệnh `AUDIT` (chọn `Y` để sửa toàn bộ lỗi được phát hiện) và lệnh `PURGE` để dọn sạch rác phát sinh.

## Tự kiểm tra

```quiz
id: q-ac-10-09-1
type: single
question: "Khi bạn bấm Ctrl + O để mở bản vẽ nhưng AutoCAD không hiện cửa sổ duyệt file mà lại yêu cầu gõ đường dẫn trên dòng lệnh, bạn cần đổi giá trị của biến hệ thống nào thành 1?"
options:
  - text: "PICKFIRST"
    why: "PICKFIRST quản lý việc chọn đối tượng trước hay sau khi gọi lệnh."
  - text: "FILEDIA"
    correct: true
    why: "Chính xác. FILEDIA = 1 là giải pháp khắc phục sự cố mất hộp thoại mở file."
  - text: "LTSCALE"
    why: "LTSCALE quản lý tỉ lệ khoảng hở của các nét đứt."
  - text: "OSMODE"
    why: "OSMODE lưu trữ cấu hình bắt điểm truy bắt đối tượng."
explain: "Biến hệ thống FILEDIA kiểm soát việc hiển thị các hộp thoại tập tin (File Dialogues). Khi FILEDIA = 1, hộp thoại mở và lưu file sẽ hiển thị; khi = 0, lệnh sẽ hỏi đường dẫn dạng văn bản trên thanh Command."
tags: [filedia, bien-he-thong, sua-loi]
```

```quiz
id: q-ac-10-09-2
type: single
question: "Để hiển thị lại thanh gõ lệnh (Command Line) bị ẩn mất trên màn hình làm việc, bạn dùng tổ hợp phím tắt nào?"
options:
  - text: "Ctrl + 1"
    why: "Ctrl + 1 dùng để bật tắt bảng Properties."
  - text: "Ctrl + Z"
    why: "Ctrl + Z dùng để hoàn tác lệnh vừa thực hiện."
  - text: "Ctrl + 9"
    correct: true
    why: "Chính xác. Ctrl + 9 là phím tắt bật tắt Command Line kinh điển."
  - text: "Ctrl + 0"
    why: "Ctrl + 0 dùng để bật tắt chế độ toàn màn hình Clean Screen."
explain: "Tổ hợp phím Ctrl + 9 dùng để bật hoặc tắt nhanh thanh giao diện dòng lệnh Command Line trong AutoCAD."
tags: [commandline, phim-tat, giao-dien]
```

```quiz
id: q-ac-10-09-3
type: truefalse
question: "Khi một bản vẽ DWG bị lỗi cấu trúc nghiêm trọng khiến lệnh OPEN thông thường không thể mở được, bạn có thể dùng lệnh RECOVER để AutoCAD vừa mở vừa tự động quét sửa lỗi."
answer: true
explain: "Đúng. Lệnh RECOVER mở một tệp bản vẽ bị hư hại và thực hiện quá trình chẩn đoán, sửa chữa các bảng dữ liệu khối bị hỏng bên trong tệp trước khi nạp vào bộ nhớ."
tags: [recover, audit, cap-cuu-file]
```

```quiz
id: q-ac-10-09-4
type: multi
question: "Khi chữ tiếng Việt trong bản vẽ bị biến thành các dấu hỏi '????' do thiếu phông chữ kỹ thuật SHX, những cách xử lý nào sau đây là đúng đắn? (Chọn 2 phương án)"
options:
  - text: "Xóa toàn bộ chữ đó đi và gõ lại bằng tay"
    why: "Xóa đi gõ lại là cách thủ công và cực kỳ tốn công sức đối với bản vẽ lớn."
  - text: "Tìm tệp phông chữ .shx bị thiếu và chép vào thư mục Fonts của phần mềm AutoCAD rồi khởi động lại"
    correct: true
    why: "Chính xác. Chép file .shx vào thư mục Fonts của AutoCAD giúp chữ hiển thị chuẩn xác như máy người gửi."
  - text: "Dùng lệnh STYLE để đổi kiểu chữ đó sang các phông chữ hệ thống phổ biến như Arial hoặc Times New Roman"
    correct: true
    why: "Chính xác. Đổi sang phông TrueType Arial giúp bản vẽ hiển thị tiếng Việt rõ ràng trên mọi máy tính."
  - text: "Chuyển hệ điều hành Windows sang giao diện tiếng Anh"
    why: "Ngôn ngữ hiển thị của Windows không ảnh hưởng đến việc thiếu phông SHX trong AutoCAD."
explain: "Cách xử lý triệt để nhất là bổ sung đúng file phông chữ .shx bị thiếu vào thư mục Fonts của AutoCAD, hoặc chuyển đổi định dạng Style sang phông chữ Unicode TrueType tiêu chuẩn như Arial."
tags: [font-shx, style, sua-loi]
```

## Bảng tổng hợp các biến hệ thống cứu nguy khẩn cấp

| Tên biến hệ thống | Giá trị chuẩn | Ý nghĩa & Tác dụng khi gặp sự cố |
| :--- | :---: | :--- |
| `FILEDIA` | `1` | Hiện hộp thoại mở và lưu file đồ họa (thay vì gõ văn bản). |
| `PICKFIRST` | `1` | Cho phép quét chọn đối tượng trước rồi mới bấm lệnh/phím xóa. |
| `COMMANDLINE` | *(Lệnh)* | Bật lại thanh gõ lệnh dưới đáy màn hình (Phím tắt `Ctrl + 9`). |
| `ANNOALLVISIBLE` | `1` | Ép hiển thị tất cả các kích thước Annotative dù sai lệch tỉ lệ. |
| `LTSCALE` | *(Tùy tỉ lệ)* | Điều chỉnh khoảng cách mắt lưới và độ thưa của nét đứt. |
| `PSLTSCALE` | `1` | Đồng bộ tỉ lệ nét đứt giữa không gian Giấy (Layout) và Model. |
| `REGENMODE` | `1` | Tự động làm mới màn hình đồ họa khi phóng to thu nhỏ. |

## Bài tập thực hành

- [ ] Tạo bản vẽ mới từ template `acadiso.dwt`. Khởi động công cụ kiểm toán và sửa lỗi bản vẽ hiện hành bằng lệnh `AUDIT`. <!-- expect: AUDIT -->
- [ ] Khi dòng lệnh hỏi `Fix any errors detected? [Yes/No] <N>:`, nhập `Y` và nhấn Enter để phần mềm quét và báo cáo số lỗi đã sửa.
- [ ] Khởi động công cụ cứu hộ tập tin từ ổ đĩa bằng lệnh `RECOVER` để mở hộp thoại Select File. <!-- expect: RECOVER -->
- [ ] Nhấn nút Cancel để đóng hộp thoại cứu hộ, sau đó gõ lệnh thanh lọc bản vẽ `PURGE`. <!-- expect: PURGE -->
- [ ] Trong hộp thoại Purge, bấm nút `Purge All` để làm sạch toàn bộ các layer, block và kiểu chữ rác không còn sử dụng trong bản vẽ.

## Nguồn tham khảo

```links
- title: "Lệnh AUDIT - Kiểm tra và sửa chữa toàn vẹn bản vẽ (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACD/2025/ENU/?guid=GUID-D96F0FE6-136C-45B0-B536-2EE035DF31CD"
  kind: official
- title: "Lệnh RECOVER - Phục hồi bản vẽ bị hư hại hoặc crash (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACD/2025/ENU/?guid=GUID-D9A3B053-C7B4-4B33-B972-2CFB683BE632"
  kind: official
- title: "Khắc phục hiện tượng thiếu phông chữ SHX trong AutoCAD (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACD/2025/ENU/?guid=GUID-827F3841-3F71-44DC-9D23-A0A6DA14470C"
  kind: official
```
