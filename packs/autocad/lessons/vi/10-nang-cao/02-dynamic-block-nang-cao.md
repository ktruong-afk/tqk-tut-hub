---
id: ac-10-02
title: Làm chủ Dynamic Block nâng cao với Block Properties Table và Lookup
category: Nâng cao và Tự động hoá
tags: [dynamic-block, lookup, block-properties-table, array-action, nang-cao]
level: advanced
minutes: 25
needs: [ac-10-01]
appVersions: ['2024', '2025']
edition: all
---
# Làm chủ Dynamic Block nâng cao với Block Properties Table và Lookup

> **Mục tiêu:**
> - Sử dụng bảng thuộc tính khối [[Block]] Properties Table để quản lý ma trận kích thước chuẩn kỹ thuật.
> - Kết hợp tham số Lookup để tạo menu chọn nhanh các mã hiệu sản phẩm catalog (Cửa D800, D900, D1000).
> - Áp dụng hành động mảng Array Action để tạo các khối động thông minh tự động nhân bản chi tiết khi kéo dài (bậc cầu thang, hàng rào).

## Nâng tầm trí thông minh cho khối Dynamic Block

Ở chặng 6, bạn đã làm quen với các thao tác khối động cơ bản: kéo dãn (`Stretch`) và lật đối xứng (`Flip`). Tuy nhiên, trong các bộ hồ sơ thiết kế tiêu chuẩn quốc tế, các khối động còn đòi hỏi độ thông minh phức tạp hơn nhiều:
- Một khối thép hình I: Khi bạn chọn mã hiệu `I200x100`, chiều cao bụng, chiều rộng cánh và độ dày bản thép phải **đồng loạt thay đổi theo bảng tra tiêu chuẩn** của nhà sản xuất.
- Một chiếc bàn hội trường: Khi bạn kéo dài chiếc bàn từ 1.2 mét ra 3.6 mét, số lượng ghế xung quanh phải **tự động mọc thêm đều đặn** theo bước nhảy 600mm mà không cần lệnh copy thủ công!

Hai công cụ cao cấp trong môi trường Block Editor (`BEDIT`) giúp hiện thực hóa điều này là **Block Properties Table** và **Array Action**.

## 1. Ma trận kích thước với Block Properties Table

Block Properties Table là một bảng trang tính tích hợp ngay bên trong Block: Nó cho phép bạn liên kết nhiều tham số khác nhau (ví dụ: Chiều rộng $W$, Chiều cao $H$, Chiều sâu $D$) vào từng hàng mã hiệu sản phẩm duy nhất.

### Cách thiết lập trong Block Editor:
1. Mở khối trong môi trường `BEDIT`.
2. Tạo 2 tham số `Linear`: `ChieuRong` và `ChieuDai`, gán các hành động `Stretch` tương ứng.
3. Trên bảng Block Authoring Palettes > thẻ *Parameters*, chọn **Block Properties Table**. Bấm chuột đặt bảng vào bản vẽ.
4. Hộp thoại **Block Properties Table** mở ra:
   - Bấm nút **Add Properties...** ở góc trên bên phải.
   - Chọn đưa 2 biến `ChieuRong` và `ChieuDai` vào cột của bảng.
5. Giờ bạn điền các hàng kích thước chuẩn sản xuất:
   - Hàng 1: `ChieuRong = 800`, `ChieuDai = 1200`
   - Hàng 2: `ChieuRong = 900`, `ChieuDai = 1600`
   - Hàng 3: `ChieuRong = 1000`, `ChieuDai = 2000`
6. Đánh dấu tick vào ô **Block properties must match a row in the table** (bắt buộc người vẽ chỉ được chọn các kích thước có sẵn trong catalog, không được kéo kích thước tùy tiện).
7. Bấm **OK**, lưu khối lại (`BCLOSE` & `BSAVE`).

### Trải nghiệm ngoài bản vẽ:
- Bấm chọn khối ngoài bản vẽ: Một mũi tên menu xổ xuống màu xanh nhỏ xuất hiện.
- Bạn bấm vào mũi tên: Danh sách các bộ kích thước chuẩn hiện ra. Bấm chọn hàng nào, cả chiều rộng và chiều dài của khối sẽ tự động nhảy số đồng bộ cùng một lúc!

## 2. Tự động nhân bản chi tiết với Array Action

Hãy tưởng tượng bạn thiết kế một cái thang leo thoát hiểm hoặc một hàng rào song sắt: Khi kéo dài hàng rào ra thêm 5 mét, bạn muốn các song sắt tự động sinh thêm và cách đều nhau đúng 150mm.

### Cách thiết lập:
1. Trong `BEDIT`, đặt một tham số `Linear` chạy dọc theo chiều dài hàng rào (ví dụ tên là `ChieuDaiHangRao`).
2. Chuyển sang thẻ *Actions*, chọn **Array**.
3. AutoCAD yêu cầu:
   - *Select parameter:* Bấm chọn chữ `ChieuDaiHangRao`.
   - *Select objects:* Bấm chọn nét vẽ của 1 thanh song sắt mẫu, nhấn [Enter].
   - *Enter the distance between columns:* Nhập khoảng cách bước nhảy giữa 2 song sắt: ví dụ `150` mm rồi nhấn [Enter].
4. Đóng Block Editor và lưu lại.

### Kết quả kỳ diệu:
Bấm vào khối hàng rào ngoài bản vẽ, nắm mũi tên tam giác kéo dãn sang phải:
Cứ mỗi khi bạn kéo chuột qua một nấc 150mm, một thanh song sắt mới sẽ tự động mọc thêm ngay ngắn thẳng tắp! Khi co ngắn lại, các thanh thừa tự động biến mất!

> [!TIP]
> Bạn có thể kết hợp hành động `Stretch` và `Array` vào cùng một mũi tên kéo Grip: Khung bao ngoài bị kéo dãn bằng Stretch, trong khi các nan chớp bên trong tự động nhân mảng bằng Array!

## Tự kiểm tra

```quiz
id: q-ac-10-02-1
type: single
question: "Tính năng Block Properties Table trong môi trường Block Editor mang lại lợi ích nổi bật nào?"
options:
  - text: "Cho phép quản lý đồng bộ nhiều kích thước (rộng, dài, cao) theo từng hàng mã hiệu catalog chuẩn của nhà sản xuất"
    correct: true
    why: "Block Properties Table liên kết ma trận nhiều biến số vào một menu chọn duy nhất."
  - text: "Tự động đổi màu chữ sang màu tím"
    correct: false
    why: "Màu sắc do Layer quản lý."
  - text: "Chuyển bản vẽ 2D thành bộ phim hoạt hình"
    correct: false
    why: "Không liên quan đến làm phim hoạt hình."
  - text: "Xóa toàn bộ bản vẽ khi chọn sai kích thước"
    correct: false
    why: "Block Properties Table chỉ kiểm soát kích thước hình học."
explain: "Block Properties Table biến khối động thành một catalog sản phẩm thông minh, ngăn chặn triệt để người vẽ nhập các kích thước phi thực tế."
```

```quiz
id: q-ac-10-02-2
type: single
question: "Hành động (Action) nào trong Block Editor giúp tự động nhân bản thêm các chi tiết cách đều nhau (như bậc thang, nan chớp, bu lông) khi kéo dãn chiều dài?"
options:
  - text: "Array Action"
    correct: true
    why: "Array Action tự động sao chép đối tượng theo cự ly bước nhảy chỉ định khi thay đổi tham số Linear."
  - text: "Rotate Action"
    correct: false
    why: "Rotate Action dùng để xoay góc đối tượng."
  - text: "Flip Action"
    correct: false
    why: "Flip Action dùng để lật đối xứng gương."
  - text: "Scale Action"
    correct: false
    why: "Scale Action phóng to thu nhỏ toàn bộ khối theo tỉ lệ đồng dạng."
explain: "Sử dụng Array Action để tạo các khối động dạng hàng rào, bậc thang, kệ giá đỡ có số lượng phần tử tự co giãn theo chiều dài."
```

```quiz
id: q-ac-10-02-3
type: truefalse
question: "Bạn có thể gán đồng thời cả hành động Stretch (kéo dãn khung bao) và hành động Array (nhân bản nan bên trong) vào cùng một tham số Linear duy nhất."
answer: true
explain: "Một tham số có thể điều khiển nhiều hành động khác nhau cùng một lúc để tạo nên các khối động đa năng cực kỳ tinh vi."
```

## Lỗi thường gặp

- **Kéo Array nhưng các chi tiết bị đè chồng lên nhau:** Do nhập khoảng cách *Distance between columns* bằng 0 hoặc quá bé so với bề rộng của chi tiết mẫu. Hãy kiểm tra nhập cự ly bước nhảy lớn hơn bề rộng chi tiết.
- **Mũi tên menu xổ xuống của Block Properties Table không hiện ra ngoài bản vẽ:** Do bạn chưa gán ít nhất một hàng dữ liệu trong bảng. Hãy mở lại `BEDIT` và kiểm tra bảng đã có dữ liệu chưa.

## Bài tập thực hành

- [ ] Dùng `RECTANG` vẽ một khung kệ sách 800 x 300 mm và đóng gói thành block bằng lệnh `BLOCK`. <!-- expect: BLOCK -->
- [ ] Gõ `BEDIT`, mở khối kệ sách vừa tạo trong môi trường Block Editor. <!-- expect: BEDIT -->
- [ ] Gán tham số `Linear` theo chiều dài kệ sách. <!-- expect: BEDIT -->
- [ ] Gán hành động `Array` cho một đợt ngăn chia sách với khoảng cách bước nhảy 350 mm. <!-- expect: BEDIT -->
- [ ] Đóng và lưu khối bằng `BCLOSE` & `BSAVE`. Thử kéo dãn kệ sách ngoài bản vẽ để quan sát các ngăn sách tự động sinh thêm. <!-- expect: BCLOSE -->

## Nguồn tham khảo

```links
- title: "Block Properties Table từ Autodesk Knowledge Network"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=Block+Properties+Table"
  kind: official
- title: "Gán hành động Array Action trong Dynamic Block từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=Array+Action+Dynamic+Block"
  kind: official
```
