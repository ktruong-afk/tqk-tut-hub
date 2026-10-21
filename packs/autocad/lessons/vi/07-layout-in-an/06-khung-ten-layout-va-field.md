---
id: ac-07-06
title: Thiết kế khung tên thông minh trên Layout kết hợp Field
category: Layout và In ấn
tags: [khung-ten, layout, field, attribute, tieu-chuan]
level: intermediate
minutes: 25
needs: [ac-07-01, ac-06-06]
appVersions: ['2024', '2025']
edition: all
---
# Thiết kế khung tên thông minh trên Layout kết hợp Field

> **Mục tiêu:**
> - Thiết kế khung bản vẽ và khung tên tiêu chuẩn Việt Nam (TCVN) trên không gian giấy Layout.
> - Kết hợp thuộc tính Block Attribute (`ATTDEF`) để nhập liệu thông tin dự án linh hoạt.
> - Ứng dụng trường dữ liệu `FIELD` để tự động cập nhật ngày tháng, tên tệp và số hiệu trang bản vẽ.

## Khung tên: Bộ mặt nhận diện của hồ sơ thiết kế

Khung tên bản vẽ (Title Block) không đơn thuần chỉ là một cái bảng chữ nhật ghi thông tin. Nó là tài liệu pháp lý bắt buộc của mọi công trình xây dựng và cơ khí, chứa đựng:
- Tên chủ đầu tư, tên công ty tư vấn thiết kế, tên công trình.
- Chữ ký và họ tên của người thiết kế, người kiểm tra, chủ nhiệm đồ án.
- Giai đoạn thiết kế (Thiết kế cơ sở, Thiết kế bản vẽ thi công).
- Tên bản vẽ, số hiệu bản vẽ, tỉ lệ và ngày xuất bản.

Trong không gian [[Layout]], khung tên được vẽ với đúng kích thước thật bằng milimet và đóng gói thành một **khối Block thông minh** kết hợp giữa thuộc tính tĩnh, thuộc tính thay đổi ([[Attribute]]) và các biến tự động tính toán ([[Field]]).

## Tiêu chuẩn kích thước lề khung bản vẽ (TCVN 3821:2008)

Khi in bản vẽ ra giấy để đóng thành tập hồ sơ:
- Mép ngoài cùng: Đúng kích thước khổ giấy tiêu chuẩn (ví dụ khổ A3 là `420 x 297` mm).
- **Lề trái (Gáy đóng tập hồ sơ):** Cách mép giấy **`20 mm`** (chừa khoảng trống để dập ghim hoặc khoan lỗ đóng còng mà không bấm vào hình vẽ).
- **Ba lề còn lại (Trên, Dưới, Phải):** Cách mép giấy **`5 mm`** (đối với khổ A3, A4) hoặc `10 mm` (đối với khổ A2, A1, A0).
- **Khung tên chính:** Thường được đặt cố định ở góc dưới cùng bên phải của khung bản vẽ, chiều rộng tiêu chuẩn là `140 mm` đến `180 mm`.

## Cách tạo khung tên thông minh từng bước

### Bước 1: Dựng khung viền trên Layout
1. Chuyển sang tab `Layout` đã cấu hình khổ A3 Full Bleed ở bài 2.
2. Chuyển sang layer `KHUNG_TEN` (nét đậm 0.35mm hoặc 0.50mm).
3. Gõ `RECTANG`, vẽ khung bao ngoài cùng từ toạ độ `0,0` đến `@420,297`.
4. Vẽ khung viền trong: Góc dưới bên trái cách toạ độ gốc (20, 5), góc trên bên phải cách toạ độ gốc (415, 292).
5. Vẽ các đường chia ô khung tên ở góc dưới bên phải bằng `LINE` và `OFFSET`.

### Bước 2: Phân loại dữ liệu và gán thuộc tính ATTDEF
Hãy phân chia các thông tin trong khung tên thành 3 nhóm rõ ràng:
1. **Thông tin cố định (Vẽ chữ thường):** Logo công ty, tên công ty thiết kế, các dòng tiêu đề chữ nhỏ như "Chủ trì thiết kế:", "Người vẽ:", "Tên dự án:".
2. **Thông tin thay đổi theo từng bản vẽ (Dùng lệnh ATTDEF):**
   - Tạo thuộc tính `TEN_BAN_VE`: Prompt là "Nhập tên bản vẽ", Default là "MẶT BẰNG TẦNG 1".
   - Tạo thuộc tính `SO_HIEU_BV`: Prompt là "Nhập số hiệu", Default là "KT-01".
   - Tạo thuộc tính `TI_LE`: Prompt là "Nhập tỉ lệ", Default là "1:100".
3. **Thông tin tự động hóa 100% (Lồng trường dữ liệu FIELD):**
   - **Tên trang Layout tự động:** Trong hộp thoại `ATTDEF`, ở ô Default nhấp chuột phải chọn **Insert Field...** > chọn Category `Other` > chọn `SystemVariable` > chọn biến `ctab`. Khi bạn đổi tên tab Layout thành `KT-01`, chữ trên khung tên tự nhảy thành `KT-01` theo!
   - **Ngày lưu bản vẽ:** Chèn Field `SaveDate` với định dạng `dd/MM/yyyy`.

### Bước 3: Đóng gói thành Block thư viện
1. Gõ lệnh `BLOCK`, đặt tên là `KHUNG-TEN-A3-TCVN`.
2. Bấm nút **Pick Point**: Bắt điểm chính xác vào góc dưới cùng bên trái của tờ giấy (toạ độ `0,0`).
3. Bấm **Select Objects**: Quét chọn toàn bộ khung viền, đường kẻ và các nhãn thuộc tính vừa tạo.
4. Bấm **OK**.

### Bước 4: Tận hưởng sự tiện lợi khi sử dụng
- Từ nay, khi tạo một trang Layout mới: Bạn chỉ việc gõ `I` (`INSERT`), bấm chèn block `KHUNG-TEN-A3-TCVN` vào toạ độ `0,0`.
- Hộp thoại thuộc tính lập tức hiện ra: Bạn chỉ cần gõ tên bản vẽ "MẶT CẮT 1-1" rồi nhấn [Enter].
- Khung tên hoàn chỉnh xuất hiện sắc sảo, ngay ngắn từng milimet, không cần vẽ lại dù chỉ một nét!

> [!TIP]
> Sử dụng trường dữ liệu `SheetSet` (sẽ học ở bài 7) trong khung tên để số thứ tự trang bản vẽ tự động nhảy số theo chuỗi: trang 1/50, trang 2/50, trang 3/50... cực kỳ chuyên nghiệp!

## Tự kiểm tra

```quiz
id: q-ac-07-06-1
type: single
question: "Theo tiêu chuẩn bản vẽ kỹ thuật TCVN, lề mép bên trái của khung bản vẽ thường được chừa khoảng cách bao nhiêu milimet để phục vụ đóng ghim còng hồ sơ?"
options:
  - text: "20 mm"
    correct: true
    why: "Lề trái 20mm là khoảng cách chuẩn quốc gia để đóng bìa hồ sơ mà không che mất nét vẽ."
  - text: "5 mm"
    why: "5mm là khoảng cách dành cho 3 mép còn lại (trên, dưới, phải)."
  - text: "50 mm"
    why: "50mm quá rộng làm lãng phí diện tích vẽ của trang giấy."
  - text: "0 mm"
    why: "0mm sẽ khiến gáy hồ sơ kẹp đè lên nội dung bản vẽ khi đóng ghim."
explain: "Quy tắc lề trái 20mm và các lề còn lại 5mm là tiêu chuẩn bắt buộc trong mọi hồ sơ thiết kế xây dựng và cơ khí tại Việt Nam."
```

```quiz
id: q-ac-07-06-2
type: single
question: "Để giá trị trong khung tên tự động hiển thị đúng theo tên của tab Layout hiện hành, bạn chèn trường Field liên kết với biến hệ thống nào?"
options:
  - text: "Biến ctab (Current Tab)"
    correct: true
    why: "Biến ctab luôn lưu trữ tên chuỗi ký tự của tab Layout hiện hành trong AutoCAD."
  - text: "Biến date"
    why: "Biến date lưu trữ thời gian ngày tháng năm."
  - text: "Biến dwgname"
    why: "Biến dwgname lưu tên của tệp bản vẽ DWG."
  - text: "Biến clayer"
    why: "Biến clayer lưu tên của layer hiện hành."
explain: "Trường Field liên kết với biến 'ctab' là mẹo kinh điển giúp tên bản vẽ trên khung tên tự động đồng bộ mỗi khi bạn đổi tên tab Layout."
```

```quiz
id: q-ac-07-06-3
type: truefalse
question: "Điểm chèn Base Point khi đóng gói Block khung tên nên chọn chính xác vào góc tọa độ gốc (0,0) của khổ giấy để dễ dàng căn khớp viền trang in."
answer: true
explain: "Chọn Base Point tại góc (0,0) giúp việc chèn khung tên vào bất kỳ trang Layout nào cũng khớp viền 100% chỉ bằng cách nhập tọa độ 0,0."
```

## Lỗi thường gặp

- **Chèn khung tên vào toạ độ 0,0 nhưng bị lệch khỏi tờ giấy trắng:** Do cấu hình trong Page Setup của Layout đó chưa đặt lề *Plot offset* về `0,0`, hoặc chưa chọn khổ giấy `Full Bleed`. Khắc phục: Chạy lại lệnh `PAGESETUP` chỉnh lại lề in.
- **Sửa chữ trong khung tên làm các trang khác bị đổi theo:** Do người vẽ dùng chữ tĩnh viết trực tiếp trong Block thay vì dùng thuộc tính `ATTDEF`. Hãy dùng thuộc tính để mỗi trang có nội dung độc lập.

## Bài tập thực hành

- [ ] Trong tab Layout, dùng lệnh `RECTANG` vẽ khung viền giấy 420 x 297 mm. <!-- expect: RECTANG -->
- [ ] Dùng `RECTANG` vẽ tiếp khung lề bên trong cách lề trái 20mm, các lề khác 5mm. <!-- expect: RECTANG -->
- [ ] Dùng lệnh `ATTDEF`, tạo một thuộc tính có Tag là `TEN_BV`, Prompt là `Nhap ten ban ve:` và đặt vào ô tiêu đề khung tên. <!-- expect: ATTDEF -->
- [ ] Dùng lệnh `BLOCK`, đóng gói toàn bộ khung vừa vẽ thành khối có tên `KHUNG-A3-CHUAN` với điểm chèn tại toạ độ 0,0. <!-- expect: BLOCK -->
- [ ] Gõ `INSERT`, chèn lại khối khung tên vừa tạo và kiểm tra việc nhập tên bản vẽ. <!-- expect: INSERT -->

## Nguồn tham khảo

```links
- title: "Thiết kế Title Blocks cho Layout từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=Title+Blocks"
  kind: official
- title: "Chèn trường Field vào Block thuộc tính từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=Fields+in+Attributes"
  kind: official
```
