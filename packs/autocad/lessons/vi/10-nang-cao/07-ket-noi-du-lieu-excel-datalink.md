---
id: ac-10-07
title: Liên kết dữ liệu bảng tính Excel với Data Link
category: Nâng cao và Tự động hoá
tags: [datalink, excel, table, du-lieu, nang-cao]
level: advanced
minutes: 20
needs: [ac-05-08, ac-06-07]
appVersions: ['2024', '2025']
edition: all
---
# Liên kết dữ liệu bảng tính Excel với Data Link

> **Mục tiêu:**
> - Thiết lập đường kết nối trực tiếp (`Data Link`) giữa bảng tính Microsoft Excel (`.xlsx` / `.xls`) và bản vẽ AutoCAD.
> - Tạo đối tượng [[Table]] liên kết sống, tự động đồng bộ số liệu khối lượng, dự toán và danh mục kỹ thuật.
> - Làm chủ cơ chế đồng bộ hai chiều, quản lý mở khóa ô (`Cell Locking`) và lệnh cập nhật `DATALINKUPDATE`.

## Sức mạnh của liên kết động Data Link: Tạm biệt nhập liệu thủ công

Trong quy trình thiết kế kỹ thuật, số liệu dự toán, bảng thống kê cốt thép hay danh mục thiết bị thường được kỹ sư tính toán trong bảng tính **Microsoft Excel**. Nếu bạn sao chép và dán ảnh tĩnh (OLE) hoặc gõ lại từng con số vào bảng vẽ AutoCAD:
- Mọi chỉnh sửa bên Excel sẽ buộc bạn phải ngồi gõ lại toàn bộ trong CAD.
- Nguy cơ sai sót số liệu cực kỳ lớn khi dự án bước vào giai đoạn nước rút thay đổi thiết kế liên tục.

Tính năng **Data Link** sinh ra để giải quyết triệt để vấn đề này. Nó tạo ra một "đường ống kết nối sống" giữa dải ô tính Excel (hoặc toàn bộ Sheet) với đối tượng [[Table]] trong AutoCAD:
- Khi kỹ sư cập nhật khối lượng trong Excel, AutoCAD sẽ hiện thông báo khay hệ thống nhắc nhở cập nhật chỉ bằng một cú nhấp chuột.
- Khi được cấp quyền, bạn thậm chí có thể sửa số liệu ngay trên bảng vẽ CAD rồi ghi ngược trở lại tệp Excel gốc (`Write back to Excel`).

```
[ Tệp Excel: Bang-khoi-luong.xlsx ]
             │   ▲
             ▼   │   (Data Link: Đồng bộ hai chiều)
[ Đối tượng Table trong AutoCAD ]
```

## Các bước thiết lập Data Link kết nối file Excel

Để tạo đường nối dữ liệu, bạn thực hiện qua hộp thoại quản trị **Data Link Manager**:

1. **Khởi động lệnh**: Gõ lệnh `DATALINK` (hoặc vào ribbon **Annotate** $\to$ nhóm **Tables** $\to$ bấm biểu tượng **Data Link**).
2. **Tạo liên kết mới**:
   - Trong cây thư mục bên trái hộp thoại, chọn dòng `Create a new Excel Data Link`.
   - Đặt tên gợi nhớ cho liên kết, ví dụ: `ThongKeThep` hoặc `DanhSachCua` (viết liền không dấu để tránh lỗi đường dẫn). Nhấn **OK**.
3. **Chỉ định tệp nguồn**:
   - Tại ô **Browse for a file** (`...`), duyệt đến vị trí tệp Excel trên máy tính của bạn.
   - Chọn kiểu đường dẫn: Nên tích chọn `Relative path` (đường dẫn tương đối) nếu tệp Excel nằm cùng thư mục hoặc thư mục con của bản vẽ DWG để tránh mất liên kết khi sao chép cả thư mục dự án sang máy khác.
4. **Chọn vùng dữ liệu**:
   - `Link entire sheet`: Lấy toàn bộ nội dung của trang tính được chọn.
   - `Link to a range`: Chỉ định chính xác dải ô cần lấy, ví dụ `A1:F25` hoặc tên vùng đã đặt trước trong Excel (`Named Range`).
5. **Xem trước và hoàn tất**: Kiểm tra bảng xem trước ở nửa dưới hộp thoại, sau đó nhấn **OK** hai lần để lưu cấu hình liên kết.

> [!TIP]
> Luôn đặt tên vùng ô tính trong Excel (**Name Box**, ví dụ đặt tên vùng là `BangTongHop`) thay vì trích xuất theo toạ độ cứng `A1:D30`. Khi bạn chèn thêm hàng hoặc cột trong Excel, Named Range sẽ tự động co giãn theo, giúp liên kết AutoCAD không bao giờ bị cắt cụt dữ liệu!

## Tạo AutoCAD Table từ Data Link và quy tắc cập nhật hai chiều

Sau khi đã có đường liên kết trong bộ nhớ bản vẽ, bạn tiến hành chèn bảng vào không gian vẽ:

1. Gõ lệnh `TABLE`.
2. Trong hộp thoại **Insert Table**, tại mục **Insert options**, thay vì chọn `Start from empty table`, bạn tích chọn **From a data link**.
3. Bấm vào menu thả xuống và chọn tên liên kết bạn vừa tạo (`ThongKeThep`).
4. Nhấn **OK** và bấm một điểm trên màn hình đồ họa để đặt bảng.

### Cơ chế cập nhật và đồng bộ

Dữ liệu không tự ý thay đổi trong lúc bạn đang vẽ dở để tránh giật lag phần mềm. Khi file Excel bị người khác chỉnh sửa và lưu lại:
- AutoCAD sẽ xuất hiện bong bóng thông báo màu vàng ở góc dưới bên phải màn hình: *"Data link has changed"*.
- Bạn chỉ cần bấm vào dòng chữ liên kết trong bong bóng thông báo, hoặc gõ lệnh `DATALINKUPDATE` $\to$ chọn tuỳ chọn `Update data link` $\to$ chọn bảng để nạp tức thì dữ liệu mới nhất.
- Ngược lại, nếu bạn chỉnh sửa ô tính trên CAD và muốn ghi đè vào Excel: Dùng lệnh `DATALINKUPDATE` $\to$ chọn tuỳ chọn `Write data link to external file` (ghi ngược vào file ngoài).

## Tuỳ chọn và mẹo khóa ô dữ liệu (Cell Locking)

Theo mặc định an toàn của AutoCAD, mọi ô tính được tạo từ Data Link đều bị khóa cứng (**Locked**) để người vẽ không vô tình sửa đè làm lệch số liệu so với bảng tính Excel gốc.

Khi bạn bấm chọn một ô tính liên kết, biểu tượng ổ khóa màu xanh lá hoặc màu vàng sẽ xuất hiện:
- **Khóa định dạng và dữ liệu (Format and Content Locked)**: Không cho phép sửa chữ số cũng như đổi màu nền, phông chữ.
- **Mở khóa để chỉnh sửa tại chỗ**:
  1. Chọn ô tính hoặc quét chọn một dải ô cần sửa.
  2. Nhấp chuột phải $\to$ chọn **Locking** $\to$ chọn **Unlocked**.
  3. Lúc này bạn có thể gõ nội dung mới vào ô tính như một bảng CAD thông thường.
  4. Sau khi sửa xong, nếu muốn đồng bộ ngược lại file Excel, hãy dùng lệnh `DATALINKUPDATE` với tùy chọn `Write`.

> [!NOTE]
> Trong hộp thoại cài đặt nâng cao của Data Link (mục **More Options**), bạn có thể tích chọn `Use Excel formatting` nếu muốn giữ nguyên màu sắc, độ rộng cột và phông chữ từ Excel, hoặc bỏ tích để bảng hiển thị thuần khiết theo kiểu dáng [[Table]] Style chuẩn của AutoCAD.

## Tự kiểm tra

```quiz
id: q-ac-10-07-1
type: single
question: "Khi liên kết một tệp Excel nằm trong cùng thư mục dự án với bản vẽ DWG, bạn nên chọn loại đường dẫn nào để tránh lỗi mất liên kết khi chuyển thư mục sang máy khác?"
options:
  - text: "Full path (đường dẫn tuyệt đối từ ổ đĩa C:\\...)"
    why: "Đường dẫn tuyệt đối sẽ hỏng ngay khi chuyển sang máy khác có cấu trúc ổ đĩa khác."
  - text: "Relative path (đường dẫn tương đối)"
    correct: true
    why: "Chính xác. Relative path giúp dự án linh hoạt và độc lập với ký tự ổ đĩa máy cá nhân."
  - text: "No path (không lưu đường dẫn)"
    why: "No path chỉ dùng khi file nằm trong thư mục cài đặt hệ thống của AutoCAD."
  - text: "URL web path"
    why: "Không áp dụng cho file bảng tính nội bộ trên ổ đĩa."
explain: "Đường dẫn tương đối (Relative path) lưu vị trí file Excel dựa trên tương quan vị trí của file bản vẽ DWG hiện tại. Nhờ đó, khi copy toàn bộ thư mục dự án sang máy tính khác hoặc sang ổ đĩa khác, AutoCAD vẫn tìm thấy file Excel chính xác."
tags: [datalink, path, excel]
```

```quiz
id: q-ac-10-07-2
type: single
question: "Lệnh nào trong AutoCAD dùng để cập nhật lại dữ liệu từ tệp Excel bên ngoài vào bản vẽ hoặc ghi dữ liệu từ bảng vẽ ngược lại tệp Excel?"
options:
  - text: "REGEN"
    why: "REGEN chỉ vẽ lại màn hình đồ họa, không nạp lại dữ liệu tệp ngoài."
  - text: "DATALINKUPDATE"
    correct: true
    why: "Chính xác. DATALINKUPDATE có hai chiều là Update (từ file vào CAD) và Write (từ CAD ra file)."
  - text: "XREF"
    why: "XREF dùng cho bản vẽ DWG, hình ảnh hoặc PDF tham chiếu, không quản lý bảng tính."
  - text: "ATTEDIT"
    why: "ATTEDIT dùng để sửa giá trị thuộc tính block."
explain: "DATALINKUPDATE là lệnh chuyên trách việc đồng bộ dữ liệu hai chiều giữa đối tượng Table trong AutoCAD và tệp dữ liệu nguồn bên ngoài (Excel)."
tags: [datalinkupdate, table, excel]
```

```quiz
id: q-ac-10-07-3
type: truefalse
question: "Mặc định khi chèn bảng từ Data Link, các ô tính trong AutoCAD sẽ bị khóa (Locked) để bảo vệ số liệu gốc không bị chỉnh sửa vô tình."
answer: true
explain: "Đúng. AutoCAD mặc định bật tính năng Cell Locking cho các ô liên kết để đảm bảo tính toàn vẹn của dữ liệu kỹ thuật từ nguồn Excel. Người dùng có thể chủ động mở khóa (Unlocked) khi cần."
tags: [cell-locking, datalink, table]
```

```quiz
id: q-ac-10-07-4
type: multi
question: "Những lý do nào khiến việc sử dụng Named Range (vùng đặt tên) trong Excel tốt hơn là chỉ định toạ độ ô cứng (ví dụ A1:F20) khi làm Data Link? (Chọn 2 phương án)"
options:
  - text: "Khi chèn thêm hàng hoặc cột trong Excel, Named Range tự động co giãn kích thước mà không làm mất dữ liệu trong AutoCAD"
    correct: true
    why: "Chính xác. Bạn thoải mái thêm hàng trong Excel mà bảng CAD không bị mất dòng cuối."
  - text: "Named Range giúp giảm 50% dung lượng tệp bản vẽ DWG"
    why: "Dung lượng bản vẽ DWG hầu như không bị ảnh hưởng bởi việc đặt tên vùng."
  - text: "Dễ quản lý và nhận diện mục đích dữ liệu (ví dụ BangKhoiLuongThep thay vì A1:F50)"
    correct: true
    why: "Chính xác. Tên gợi nhớ giúp việc chọn vùng dữ liệu chính xác và trực quan."
  - text: "Named Range tự động dịch toàn bộ chữ tiếng Anh sang tiếng Việt"
    why: "AutoCAD và Excel không tự động dịch ngôn ngữ chữ viết."
explain: "Đặt tên vùng trong Excel (Named Range) giúp dữ liệu linh hoạt khi mở rộng thêm dòng cột và giúp người thiết kế dễ quản lý dữ liệu trực quan theo tên gọi nghiệp vụ."
tags: [excel, named-range, meo]
```

## Lỗi thường gặp

### 1. Thông báo lỗi đường dẫn màu đỏ trong Data Link Manager
- **Triệu chứng**: Cột trạng thái trong hộp thoại `DATALINK` hiện dấu tam giác vàng cảnh báo hoặc đường dẫn bị báo lỗi `File not found`.
- **Nguyên nhân**: File Excel đã bị đổi tên, bị chuyển sang thư mục khác, hoặc tệp CAD được mở trên máy tính khác trong khi đang dùng đường dẫn tuyệt đối (`Full path`).
- **Cách sửa**: Mở lệnh `DATALINK`, nhấp chuột phải vào tên liên kết $\to$ chọn `Edit` $\to$ bấm nút `...` để duyệt lại đường dẫn đến vị trí tệp Excel mới. Đổi kiểu đường dẫn sang `Relative path`.

### 2. Không thể sửa số liệu trong bảng AutoCAD
- **Triệu chứng**: Nhấp đúp chuột vào ô tính trong bảng nhưng con trỏ soạn thảo không xuất hiện, hoặc thanh ribbon hiện biểu tượng ổ khóa màu vàng.
- **Nguyên nhân**: Tính năng bảo vệ dữ liệu `Cell Locking` đang kích hoạt trên các ô liên kết nguồn ngoại vi.
- **Cách sửa**: Quét chọn các ô cần sửa $\to$ bấm chuột phải $\to$ chọn **Locking** $\to$ chọn **Unlocked**. Sau đó bạn có thể nhấp đúp để nhập số liệu bình thường.

### 3. Công thức tính toán Excel hiển thị thành số 0 hoặc chữ rỗng
- **Triệu chứng**: Các ô chứa hàm tính tổng `=SUM(...)` trong Excel khi sang bảng CAD không hiển thị kết quả.
- **Nguyên nhân**: Tệp Excel vừa được sửa đổi nhưng chưa được nhấn lưu (`Ctrl + S`) trong phần mềm Excel trước khi cập nhật sang AutoCAD, hoặc trong tùy chọn Data Link chưa tích chọn nạp công thức.
- **Cách sửa**: Lưu tệp Excel lại để Excel tính toán xong giá trị công thức. Trong AutoCAD, mở `DATALINK` $\to$ `Edit` $\to$ bấm nút mũi tên mở rộng góc dưới phải $\to$ tích chọn `Allow changes to source file` và kiểm tra mục chuyển đổi dữ liệu.

## Bài tập thực hành

- [ ] Tạo bản vẽ mới từ template `acadiso.dwt`. Khởi động trình quản lý liên kết dữ liệu bằng lệnh `DATALINK`. <!-- expect: DATALINK -->
- [ ] Quan sát hộp thoại Data Link Manager, tìm dòng `Create a new Excel Data Link` và đóng hộp thoại.
- [ ] Khởi động lệnh tạo bảng `TABLE` để kiểm tra tuỳ chọn chèn bảng từ dữ liệu liên kết. <!-- expect: TABLE -->
- [ ] Trong hộp thoại Insert Table, chuyển đổi mục Insert options sang `From a data link` để xem danh sách liên kết.
- [ ] Nhấn Cancel để đóng hộp thoại, sau đó gõ lệnh cập nhật liên kết `DATALINKUPDATE` trên dòng lệnh để kiểm tra các tùy chọn Update và Write. <!-- expect: DATALINKUPDATE -->

## Nguồn tham khảo

```links
- title: "Lệnh DATALINK - Tạo và quản trị liên kết dữ liệu ngoài (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACD/2025/ENU/?guid=GUID-E5FB750E-E7D4-47FA-A049-FB654A9684C2"
  kind: official
- title: "Lệnh DATALINKUPDATE - Cập nhật đồng bộ dữ liệu hai chiều (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACD/2025/ENU/?guid=GUID-BDBBF44A-B5B3-4DF7-BFA8-E5031DFE94EB"
  kind: official
- title: "Khái niệm và cách liên kết dữ liệu ngoài với bản vẽ (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACD/2025/ENU/?guid=GUID-5C3FA7F6-559D-460B-8837-EF792510A0A1"
  kind: official
```
