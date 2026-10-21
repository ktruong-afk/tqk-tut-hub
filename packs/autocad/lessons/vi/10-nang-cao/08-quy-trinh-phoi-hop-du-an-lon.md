---
id: ac-10-08
title: Quy trình phối hợp dự án lớn và Sheet Set nâng cao
category: Nâng cao và Tự động hoá
tags: [du-an-lon, sheet-set, xref, phoi-hop, nang-cao]
level: advanced
minutes: 25
needs: [ac-06-05, ac-07-07]
appVersions: ['2024', '2025']
edition: all
---
# Quy trình phối hợp dự án lớn và Sheet Set nâng cao

> **Mục tiêu:**
> - Xây dựng mô hình tổ chức dữ liệu dự án chuyên nghiệp theo chuẩn BIM/CAD: Phân tách rõ ràng giữa tệp mô hình (`Base Model`) và tệp bản vẽ trình bày (`Sheet DWG`).
> - Khai thác sức mạnh nâng cao của [[Sheet Set Manager]] (`SHEETSET`): Đánh số thứ tự bản vẽ tự động, phân chia chuyên ngành và tạo bảng mục lục sống (`Sheet List Table`).
> - Đóng gói toàn bộ hồ sơ thiết kế kèm phông chữ, xref và nét in thành tệp nén an toàn với lệnh `ETRANSMIT`.

## Tư duy quản lý dự án lớn: Tách biệt Model và Bản vẽ hoàn thiện (Sheets)

Trong các dự án quy mô lớn (tòa nhà cao tầng, nhà máy, hạ tầng đô thị), có hàng chục kỹ sư cùng tham gia thiết kế đồng thời trên nhiều bộ môn: Kiến trúc, Kết cấu, Cơ điện (MEP), Cảnh quan.

Nếu tất cả mọi người cùng vẽ vào một file duy nhất hoặc copy qua lại các bản vẽ tĩnh:
- File sẽ phình to hàng trăm Megabyte, mở lên mất cả chục phút và rất dễ bị hỏng file (crash/corrupt).
- Xung đột thiết kế không thể kiểm soát: Kỹ sư cơ điện đi ống thông gió đâm xuyên dầm kết cấu mà không hề hay biết.

Quy chuẩn quốc tế giải quyết vấn đề này bằng triết lý **Tách biệt dữ liệu**:
1. **Tệp Mô hình Cơ sở (Base/Model Files)**:
   - Chỉ vẽ hình học thuần túy ở tỉ lệ 1:1 trong không gian Model (ví dụ: `KT-Tang01.dwg`, `KC-Cot-Tang01.dwg`).
   - Tuyệt đối không đặt khung tên hay ghi chú kích thước hoàn thiện tại đây.
2. **Tệp Bản vẽ Trình bày (Sheet Files)**:
   - Các file này chỉ chứa không gian Layout với khung tên chuẩn, ghi chú hoàn thiện, bảng thống kê.
   - Toàn bộ mặt bằng được liên kết vào qua [[XREF]] chế độ `Overlay` để các chuyên ngành tham chiếu lẫn nhau mà không gây vòng lặp luẩn quẩn.

```
[ Model Files: Kiến trúc ] ──┐
[ Model Files: Kết cấu  ] ──┼─ (Xref Overlay) ──► [ Sheet DWG: Bản vẽ In ấn ]
[ Model Files: Cơ điện  ] ──┘                               ▲
                                                            │ Quản lý & In hàng loạt
                                                   [ Sheet Set (.dst) ]
```

## Khai thác Sheet Set Manager cho dự án quy mô hàng trăm bản vẽ

Lệnh `SHEETSET` (hoặc phím tắt `Ctrl + 4`) mở ra bảng điều khiển quyền lực nhất của AutoCAD dành cho người chủ trì dự án:

### 1. Cấu trúc cây thư mục phân nhánh (Subsets)
Thay vì để danh sách hàng trăm bản vẽ lộn xộn, bạn tạo các phân nhóm con (`New Subset`) đại diện cho từng chuyên ngành hoặc từng giai đoạn:
- `01-KienTruc`
- `02-KetCau`
- `03-Dien-CapThoatNuoc`

### 2. Thuộc tính tự động hóa toàn dự án (Custom Properties)
Trong phần thuộc tính Sheet Set (`Sheet Set Properties`), bạn có thể khai báo các thông tin dùng chung cho toàn bộ dự án:
- Tên công trình: *Bệnh viện Đa khoa Quốc tế*
- Tên chủ đầu tư: *Tập đoàn ABC*
- Giai đoạn: *Thiết kế Bản vẽ Thi công (TCTC)*
- Mã hợp đồng: *HD-2026-XD01*

Khi một thông tin thay đổi (ví dụ: đổi tên chủ đầu tư), bạn chỉ cần gõ lại một lần duy nhất trong thuộc tính Sheet Set, toàn bộ 200 bản vẽ trong dự án sẽ tự động cập nhật ngay lập tức nhờ các trường [[Field]] được liên kết trong khung tên!

## Tạo bảng mục lục tự động (Sheet List Table) từ Sheet Set

Mục lục bản vẽ luôn là trang đầu tiên của bộ hồ sơ và là nơi người vẽ ngại cập nhật nhất mỗi khi thêm bớt một bản vẽ giữa chừng. Với Sheet Set Manager, bạn tạo bảng mục lục chỉ bằng một cú nhấp:

1. Trong bảng **Sheet Set Manager**, nhấp chuột phải vào nút gốc cao nhất của dự án (hoặc một Subset cụ thể).
2. Chọn lệnh **Insert Sheet List Table...**
3. Trong hộp thoại cấu hình:
   - Chọn kiểu bảng [[Table]] Style.
   - Chọn các cột thông tin cần xuất hiện: `Sheet Number` (Số hiệu), `Sheet Title` (Tên bản vẽ), `Revision Number` (Lần phát hành).
4. Nhấn **OK** và đặt bảng vào Layout trang bìa.

Bảng mục lục này liên kết sống với Sheet Set. Nếu bạn kéo thả đổi vị trí bản vẽ từ trang số 5 xuống trang số 9, bạn chỉ cần nhấp chuột phải vào bảng và chọn `Update Table Data Links` để số thứ tự tự nhảy lại hoàn hảo!

## Đóng gói và bàn giao dự án hoàn hảo với eTransmit

Khi dự án hoàn thành hoặc cần gửi file phối hợp cho đơn vị thẩm tra, việc chỉ gửi file DWG qua email là sai lầm nghiêm trọng vì máy người nhận sẽ thiếu:
- Các file [[XREF]] tham chiếu ngoài.
- Các tệp phông chữ kỹ thuật `.shx`.
- Bảng quy định nét in `.ctb` / `.stb`.
- Các file ảnh logo, bản đồ vệ tinh chèn vào bản vẽ.

Lệnh `ETRANSMIT` giải quyết triệt để vấn đề này:

1. Gõ lệnh `ETRANSMIT` (hoặc nhấp chuột phải vào tên Sheet Set $\to$ chọn `eTransmit...`).
2. Hộp thoại **Create Transmittal** sẽ tự động rà soát toàn bộ cây dữ liệu dự án và liệt kê tất cả các file phụ thuộc đi kèm.
3. Bấm **Transmittal Setups...** để tùy chỉnh:
   - Kiểu đóng gói: Tệp nén `.zip` hoặc tạo một thư mục độc lập.
   - Chuyển đổi đường dẫn Xref: Tự động chuyển toàn bộ về đường dẫn tương đối (`Make all paths relative`).
   - Tùy chọn bảo tồn: Tích chọn `Include fonts` (kèm theo toàn bộ font chữ AutoCAD đang dùng).
   - Tự động thanh lọc: Tích chọn `Purge drawings` để giảm tối đa dung lượng tệp nén.
4. Bấm **OK** để tạo tệp ZIP gói gọn toàn bộ dự án sẵn sàng chuyển giao.

## Tự kiểm tra

```quiz
id: q-ac-10-08-1
type: single
question: "Khi phối hợp nhiều bộ môn (Kiến trúc, Kết cấu, Cơ điện) bằng liên kết XREF, kiểu liên kết nào nên được ưu tiên sử dụng để tránh hiện tượng vòng lặp tham chiếu luẩn quẩn (Circular Reference)?"
options:
  - text: "Attach"
    why: "Attach sẽ tự động kéo theo toàn bộ các Xref lồng nhau, rất dễ gây ra vòng lặp tham chiếu và nặng file."
  - text: "Overlay"
    correct: true
    why: "Chính xác. Overlay là tiêu chuẩn bắt buộc trong quản lý mô hình dự án lớn."
  - text: "Bind"
    why: "Bind sẽ biến Xref thành Block vĩnh viễn, làm mất tính liên kết sống."
  - text: "Insert"
    why: "Insert là lệnh chèn block thông thường."
explain: "Chế độ Overlay chỉ nạp trực tiếp file được chọn vào bản vẽ hiện hành mà không tự động kéo theo các file Xref con lồng bên trong nó. Điều này ngăn chặn hiện tượng vòng lặp vô tận khi bộ môn A và B tham chiếu chéo lẫn nhau."
tags: [xref, overlay, du-an-lon]
```

```quiz
id: q-ac-10-08-2
type: single
question: "Lệnh nào trong AutoCAD giúp thu thập và đóng gói toàn bộ bản vẽ cùng tất cả các tệp phụ thuộc (Xref, font chữ SHX, bảng nét in CTB, ảnh) thành một tệp ZIP duy nhất?"
options:
  - text: "ETRANSMIT"
    correct: true
    why: "Chính xác. ETRANSMIT thu gom mọi tài nguyên liên quan vào file zip."
  - text: "PUBLISH"
    why: "PUBLISH dùng để in hàng loạt ra PDF hoặc máy in vật lý."
  - text: "WBLOCK"
    why: "WBLOCK dùng để xuất một nhóm đối tượng ra file DWG độc lập."
  - text: "EXPORT"
    why: "EXPORT dùng để xuất sang các định dạng đồ họa khác (DWF, DGN, FBX)."
explain: "ETRANSMIT là công cụ tiêu chuẩn để tạo gói phân phối và bàn giao bản vẽ, đảm bảo người nhận mở file lên không bị lỗi mất font, thiếu xref hay in sai nét."
tags: [etransmit, ban-giao, du-an]
```

```quiz
id: q-ac-10-08-3
type: truefalse
question: "Khi sử dụng Sheet Set Manager, bạn có thể tạo bảng mục lục bản vẽ tự động (Sheet List Table) có khả năng cập nhật lại số thứ tự trang khi có bản vẽ được thêm hoặc xóa bớt."
answer: true
explain: "Đúng. Bảng mục lục Sheet List Table được đồng bộ trực tiếp với cơ sở dữ liệu tệp .dst của Sheet Set, cho phép cập nhật tức thì danh sách và số hiệu bản vẽ."
tags: [sheetset, table, muc-luc]
```

```quiz
id: q-ac-10-08-4
type: multi
question: "Trong mô hình quản lý dự án lớn chuyên nghiệp, tệp Mô hình Cơ sở (Base Model) có đặc điểm nào dưới đây? (Chọn 2 phương án)"
options:
  - text: "Chỉ vẽ hình học thuần túy tỉ lệ 1:1 trong không gian Model"
    correct: true
    why: "Chính xác. Bản vẽ kỹ thuật luôn dựng 1:1 trong Model Space."
  - text: "Chứa toàn bộ khung tên in ấn và bìa hồ sơ"
    why: "Khung tên trình bày thuộc về tệp Sheet Layout."
  - text: "Thường không chứa khung tên và được liên kết sang các tệp bản vẽ trình bày qua XREF"
    correct: true
    why: "Chính xác. Tách rời hình học và trình bày là triết lý cốt lõi của CAD/BIM."
  - text: "Luôn được lưu dưới dạng tệp ảnh JPEG để tăng tốc độ mở"
    why: "Bản vẽ cơ sở là file định dạng DWG chuẩn, không phải ảnh JPEG."
explain: "Base Model là nơi chứa dữ liệu hình học gốc ở tỉ lệ 1:1, không chứa khung tên trình bày nhằm giữ cho mô hình sạch sẽ và cho phép nhiều bản vẽ in ấn khác nhau tham chiếu dùng chung qua Xref."
tags: [base-model, quy-trinh, du-an-lon]
```

## Lỗi thường gặp

### 1. Lỗi vòng lặp tham chiếu (Circular reference detected)
- **Triệu chứng**: Khi gắn thêm file Xref, AutoCAD hiện cảnh báo `Circular reference` và máy bị đơ hoặc tải file rất chậm.
- **Nguyên nhân**: File A gắn File B bằng chế độ `Attach`, sau đó bên File B ai đó lại gắn File A cũng bằng chế độ `Attach`. AutoCAD bị cuốn vào vòng lặp tải đệ quy vô tận.
- **Cách sửa**: Mở bảng `XREF`, nhấp vào các liên kết tham chiếu và chuyển toàn bộ kiểu liên kết từ `Attach` sang `Overlay`.

### 2. Bảng mục lục bản vẽ không cập nhật số trang mới
- **Triệu chứng**: Bạn vừa đổi tên hoặc đổi số hiệu của 5 bản vẽ trong Sheet Set Manager nhưng bảng mục lục trên bản vẽ bìa vẫn hiển thị tên cũ.
- **Nguyên nhân**: Bảng AutoCAD Table không tự quét lại tệp `.dst` liên tục để tiết kiệm tài nguyên vi xử lý.
- **Cách sửa**: Nhấp chuột phải vào bất kỳ ô nào của bảng mục lục $\to$ chọn `Update Table Data Links` (hoặc gõ lệnh `REGENALL` để làm mới các trường Field).

### 3. Đối tác nhận file báo lỗi chữ biến thành dấu hỏi hoặc nét in đậm đặc
- **Triệu chứng**: File gửi cho khách hàng bị vỡ font chữ kỹ thuật (`.shx`) hoặc khi in ra tất cả các nét đều đen xì không phân biệt được nét mảnh nét đậm.
- **Nguyên nhân**: Người gửi chỉ gửi mỗi file `.dwg` trần mà không gửi kèm thư mục font chữ nội bộ của công ty và tệp bảng nét in `.ctb`.
- **Cách sửa**: Luôn luôn dùng lệnh `ETRANSMIT` trước khi bàn giao file. Trong cài đặt của eTransmit, tích chọn `Include fonts` và kiểm tra bảng nét in đã được đóng gói trong tệp `.zip`.

## Bài tập thực hành

- [ ] Tạo bản vẽ mới từ template `acadiso.dwt`. Khởi động bảng điều khiển Sheet Set Manager bằng lệnh `SHEETSET` hoặc tổ hợp phím `Ctrl + 4`. <!-- expect: SHEETSET -->
- [ ] Quan sát giao diện quản lý cây thư mục của Sheet Set Manager, tìm hiểu nút thả xuống để tạo `New Sheet Set...` hoặc mở tập tin `.dst`.
- [ ] Mở trình quản lý tham chiếu ngoài bằng lệnh `XREF` để kiểm tra các tùy chọn gắn tệp Attach và Overlay. <!-- expect: XREF -->
- [ ] Khởi động công cụ đóng gói dự án bằng lệnh `ETRANSMIT` trên thanh lệnh để quan sát hộp thoại Create Transmittal. <!-- expect: ETRANSMIT -->
- [ ] Bấm nút `Transmittal Setups...` để xem trước các tùy chọn đóng gói font chữ, đường dẫn relative và nén tệp zip.

## Nguồn tham khảo

```links
- title: "Quản trị tập hợp bản vẽ với Sheet Set Manager (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACD/2025/ENU/?guid=GUID-E500BF26-30E8-41AA-9CE4-CD4FE35F9217"
  kind: official
- title: "Lệnh ETRANSMIT - Đóng gói dự án để chia sẻ và lưu trữ (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACD/2025/ENU/?guid=GUID-96D69F82-D07E-4464-B3DC-E16314A292C6"
  kind: official
- title: "Khái niệm và phương pháp sử dụng tệp tham chiếu ngoài XREF (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACD/2025/ENU/?guid=GUID-9F9C3401-4475-4309-96AA-D4122CD2EB74"
  kind: official
```
