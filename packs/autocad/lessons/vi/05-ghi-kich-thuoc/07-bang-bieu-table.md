---
id: ac-05-07
title: Lập bảng biểu và thống kê vật liệu với lệnh TABLE
category: Ghi kích thước
tags: [table, tablestyle, thong-ke, bom, bang-bieu]
level: intermediate
minutes: 20
needs: [ac-05-05]
appVersions: ['2024', '2025']
edition: all
---
# Lập bảng biểu và thống kê vật liệu với lệnh TABLE

> **Mục tiêu:**
> - Sử dụng lệnh `TABLE` để tạo bảng biểu thống kê khối lượng, vật liệu và danh mục bản vẽ.
> - Định dạng kiểu bảng bằng `TABLESTYLE` để tùy chỉnh phông chữ, chiều cao hàng và đường viền.
> - Thực hiện các phép tính số học cơ bản (SUM, AVERAGE) trực tiếp trong các ô của bảng CAD.

## Bảng biểu trong bản vẽ kỹ thuật

Mỗi bộ hồ sơ kỹ thuật hoàn chỉnh đều cần có các bảng thống kê: bảng thống kê cửa sổ, bảng thống kê thép, danh mục bản vẽ hoặc bảng kê phụ tùng lắp xiết (BOM - Bill of Materials).

Trước đây, người vẽ CAD thường phải vẽ từng ô bằng `LINE` rồi gõ từng chữ cái `TEXT`. Khi cần chèn thêm một dòng mới, việc kéo dãn các đường thẳng và dời chữ vô cùng cực nhọc. Đối tượng **[[Table]]** ra đời giải quyết trọn vẹn vấn đề này: nó hoạt động tương tự một trang tính Microsoft Excel thu nhỏ ngay trong lòng AutoCAD.

Bạn có thể thêm bớt hàng, cột, gộp ô (Merge cells), đổi màu nền và thậm chí viết công thức tính tổng tự động (`=SUM(A1:A10)`).

## Cách dùng từng bước

### 1. Tạo bảng với lệnh TABLE
1. Gõ `TABLE` rồi nhấn [Enter]. Hộp thoại **Insert Table** xuất hiện.
2. Tại mục **Table creation options**, chọn `Start from empty table` (bắt đầu từ bảng trống).
3. Tại mục **Table dimensions**:
   - `Columns`: Nhập số cột (ví dụ: `4` cột: STT, Tên Chi Tiết, Số Lượng, Ghi Chú).
   - `Column width`: Nhập chiều rộng cột (ví dụ: `30` mm).
   - `Data rows`: Nhập số dòng dữ liệu (ví dụ: `5` dòng).
   - `Row height`: Nhập chiều cao dòng (ví dụ: `1` dòng chữ).
4. Bấm nút **OK**.
5. Di chuột và bấm chuột trái để đặt góc trên bên trái của bảng vào vị trí mong muốn trong bản vẽ.
6. Con trỏ tự động nhảy vào ô tiêu đề (Title). Gõ tên bảng: "BẢNG KÊ VẬT TƯ CƠ KHÍ".

### 2. Nhập dữ liệu và điều hướng ô
- Nhấn phím [Tab] để nhảy sang ô bên phải.
- Nhấn [Enter] để xuống ô bên dưới.
- Dùng các phím mũi tên [↑] [↓] [←] [→] để di chuyển qua lại giữa các ô.
- Nhấp đúp chuột vào ô bất kỳ để sửa nội dung văn bản.

### 3. Thiết lập kiểu bảng với TABLESTYLE
1. Gõ `TABLESTYLE` rồi nhấn [Enter].
2. Bấm **New** để tạo một kiểu bảng riêng (ví dụ: `BANG-TCVN`).
3. Trong hộp thoại, bạn có thể chỉnh thuộc tính riêng biệt cho 3 loại ô:
   - **Title (Tiêu đề):** Chữ to, in đậm, căn giữa.
   - **Header (Tiêu đề cột):** Chữ in hoa, nền xám nhạt.
   - **Data (Dữ liệu):** Chữ thường, căn lề trái hoặc căn giữa.
4. Bấm **OK** và **Close** để lưu thiết lập.

## Tuỳ chọn và công thức tính toán tự động

Bảng trong AutoCAD hỗ trợ các công thức toán học cơ bản:
- Chọn một ô trống ở cuối cột số lượng.
- Trên thanh Ribbon ngữ cảnh của Table, chọn biểu tượng **Formula** > chọn **Sum**.
- Quét chọn dải các ô phía trên. AutoCAD sẽ tự động tính tổng giống hệt Excel!
- Khi bạn thay đổi số liệu trong các ô phía trên, con số tổng sẽ tự động cập nhật lại.

> [!TIP]
> Bạn có thể sao chép dữ liệu từ bảng tính Microsoft Excel và dán trực tiếp vào bảng AutoCAD bằng lệnh `PASTECLIP` hoặc kết nối động bằng tính năng `Data Link` (sẽ học chuyên sâu ở chặng nâng cao).

## Tự kiểm tra

```quiz
id: q-ac-05-07-1
type: single
question: "Để tạo một bảng thống kê vật tư trong AutoCAD, lệnh chuẩn là gì?"
options:
  - text: "TABLE"
    correct: true
    why: "TABLE là lệnh chính quy để khởi tạo bảng dữ liệu dạng ô lưới."
  - text: "TAB"
    correct: false
    why: "TAB không phải lệnh AutoCAD độc lập."
  - text: "GRID"
    correct: false
    why: "GRID là lưới toạ độ trợ giúp vẽ trên màn hình."
  - text: "EXCEL"
    correct: false
    why: "Không có lệnh EXCEL độc lập trong thanh dòng lệnh của AutoCAD."
explain: "Sử dụng TABLE để mở hộp thoại cấu hình số hàng, số cột và chèn bảng biểu."
```

```quiz
id: q-ac-05-07-2
type: single
question: "Khi đang nhập dữ liệu trong bảng của AutoCAD, phím nào giúp nhảy nhanh sang ô tiếp theo bên phải?"
options:
  - text: "Phím Tab"
    correct: true
    why: "Phím Tab là chuẩn điều hướng giữa các cột trong hầu hết các phần mềm bảng biểu."
  - text: "Phím Space"
    correct: false
    why: "Phím Space chỉ thêm khoảng trắng vào nội dung chữ."
  - text: "Phím Esc"
    correct: false
    why: "Phím Esc sẽ huỷ chế độ nhập văn bản và thoát khỏi ô."
  - text: "Phím F1"
    correct: false
    why: "Phím F1 mở tài liệu trợ giúp Help của Autodesk."
explain: "Nhấn Tab để sang cột phải, nhấn Shift + Tab để lùi về cột trái, nhấn Enter để xuống hàng dưới."
```

```quiz
id: q-ac-05-07-3
type: truefalse
question: "Bảng biểu trong AutoCAD có khả năng tính tổng các ô dữ liệu bằng công thức =SUM như Microsoft Excel."
answer: false
explain: "Khả năng tính toán trực tiếp với công thức giúp tránh sai sót nhầm lẫn số học khi thống kê khối lượng bản vẽ."
```

## Lỗi thường gặp

- **Chữ trong ô bảng quá to khiến hàng bị phình to bất thường:** Do kiểu chữ gán trong `TABLESTYLE` có thiết lập chiều cao cố định quá lớn. Khắc phục: Sửa lại Text Height của cell style `Data` về khoảng `2.5` mm.
- **Không xoá được đường viền ô:** Do chưa vào chế độ sửa Border trong Ribbon ngữ cảnh của Table.

## Bài tập thực hành

- [ ] Gõ `TABLESTYLE`, kiểm tra danh sách kiểu bảng có sẵn trên bản vẽ. <!-- expect: TABLESTYLE -->
- [ ] Gõ lệnh `TABLE`, thiết lập bảng gồm 3 cột và 3 hàng dữ liệu. <!-- expect: TABLE -->
- [ ] Chèn bảng vào toạ độ 0,0 trên màn hình bản vẽ.
- [ ] Điền tiêu đề cột lần lượt là: "STT", "Tên Vât Tư", "Số Lượng". <!-- expect: TABLE -->

## Nguồn tham khảo

```links
- title: "Tài liệu tạo và hiệu chỉnh Tables từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=TABLE"
  kind: official
- title: "Quản lý Table Styles từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=TABLESTYLE"
  kind: official
```
