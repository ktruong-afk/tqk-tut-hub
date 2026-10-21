---
id: ac-08-06
title: Tự động hoá công việc lặp lại với Action Recorder và Script (.scr)
category: Nâng cao năng suất
tags: [action-recorder, script, tu-dong-hoa, actrecord, actstop, scr]
level: advanced
minutes: 25
needs: [ac-08-05]
appVersions: ['2024', '2025']
edition: all
---
# Tự động hoá công việc lặp lại với Action Recorder và Script (.scr)

> **Mục tiêu:**
> - Sử dụng bộ ghi thao tác [[Action Recorder]] (`ACTRECORD`, `ACTSTOP`) để biến chuỗi thao tác thủ công thành một lệnh macro tự động.
> - Soạn thảo và thực thi tệp kịch bản [[Script]] (`.scr`) để tự động hóa hàng loạt câu lệnh dòng lệnh.
> - Áp dụng quy trình chạy script hàng loạt để mở, dọn dẹp (Audit, Purge), zoom extents và lưu hàng trăm file bản vẽ tự động.

## Giải phóng sức lao động khỏi các tác vụ lặp đi lặp lại

Trong thực tế sản xuất, có những công việc nhàm chán lặp đi lặp lại hàng ngày:
- Cứ mỗi lần vẽ xong một chi tiết, bạn lại phải: Đổi layer sang `KICH_THUOC` $\to$ Gọi lệnh `DIMLINEAR` $\to$ Đo xong lại phải đổi layer về `NET_THAY`.
- Hoặc trước khi bàn giao dự án có 100 file bản vẽ, sếp yêu cầu: "Mở từng file ra, chạy lệnh `AUDIT`, chạy lệnh `PURGE`, nhấp đúp chuột giữa `Zoom Extents`, rồi bấm `SAVE`!".

Nếu bạn ngồi làm thủ công bằng tay 100 lần, bạn sẽ mất cả ngày làm việc và kiệt sức.

AutoCAD cung cấp 2 vũ khí tự động hóa cực mạnh mà **không đòi hỏi bạn phải biết viết code lập trình**:
1. **[[Action Recorder]] (Bộ ghi macro thao tác):** Hoạt động giống như máy quay phim. Bạn bấm "Record", làm các thao tác vẽ mẫu 1 lần, rồi bấm "Stop". Từ lần sau, bạn chỉ cần gõ tên macro đó, phần mềm sẽ **tự động vẽ lại y hệt trong chớp mắt**!
2. **[[Script]] (Kịch bản dòng lệnh đuôi `.scr`):** Một file văn bản chứa danh sách các lệnh liên tiếp. Bạn chỉ việc ném file script vào AutoCAD, phần mềm sẽ tự động mở file, dọn dẹp, lưu và đóng file cho hàng trăm bản vẽ hoàn toàn tự động!

## 1. Tự động hóa với Action Recorder (ACTRECORD / ACTSTOP)

### Quy trình ghi macro
1. Chuyển sang thẻ **Manage** trên thanh Ribbon > tìm đến cụm **Action Recorder**.
2. Bấm vào nút tròn màu đỏ **Record** (hoặc gõ lệnh `ACTRECORD` rồi nhấn [Enter]).
3. Một vòng tròn màu đỏ nhỏ sẽ xuất hiện cạnh con trỏ chuột, báo hiệu AutoCAD đang ghi lại từng thao tác của bạn.
4. Giờ bạn thực hiện chuỗi công việc mẫu (ví dụ: tạo layer nét cắt, đổi màu sang đỏ, gán nét dày 0.50mm, và vẽ một hình chữ nhật).
5. Sau khi làm xong, bấm nút **Stop** trên Ribbon (hoặc gõ lệnh `ACTSTOP`).
6. Hộp thoại **Action Macro** xuất hiện:
   - *Action Macro Command Name:* Đặt tên cho lệnh tự động mới của bạn (ví dụ: `TAO_KHUNG_CAT`).
   - Bấm **OK**.

### Thực thi macro vừa tạo
Từ nay trở đi, tại bất kỳ bản vẽ nào:
- Bạn chỉ việc gõ `TAO_KHUNG_CAT` vào dòng lệnh rồi nhấn [Enter].
- Toàn bộ chuỗi thao tác đổi layer, gán nét và vẽ khung sẽ tự động thực thi trong 0.1 giây mà bạn không cần chạm tay vào thanh công cụ!

## 2. Tự động hóa hàng loạt với tệp kịch bản Script (.scr)

Một tệp kịch bản Script là một tệp văn bản thông thường lưu với đuôi `.scr`. Mỗi dòng trong file tương ứng với một lệnh bạn gõ vào thanh dòng lệnh, và phím [Enter] được đại diện bằng một dấu xuống dòng hoặc một dấu cách trắng.

### Ví dụ soạn thảo một kịch bản dọn dẹp và lưu file tự động:
Mở phần mềm Notepad của Windows, gõ nội dung sau:
```text
AUDIT Y
-PURGE ALL * N
-PURGE REGAPPS * N
ZOOM E
QSAVE
```
*Giải thích kịch bản:*
- Dòng 1: Chạy lệnh `AUDIT` và đồng ý sửa lỗi (`Y`).
- Dòng 2: Chạy `-PURGE` dọn toàn bộ các đối tượng rác (`*`) mà không hỏi xác nhận (`N`).
- Dòng 3: Dọn sạch rác tàng hình `REGAPPS`.
- Dòng 4: Thực hiện `ZOOM` toàn cảnh (`Extents`).
- Dòng 5: Lưu đè bản vẽ lại (`QSAVE`).

Lưu tệp văn bản này lại với tên: **`DON_DEP.scr`** (chọn *Save as type: All Files*).

### Chạy kịch bản với lệnh SCRIPT
1. Mở bản vẽ cần xử lý trong AutoCAD.
2. Gõ lệnh `SCRIPT` (hoặc `SCR`) rồi nhấn [Enter].
3. Duyệt tìm và chọn file `DON_DEP.scr` vừa tạo. Bấm **Open**.
4. Bạn sẽ thấy màn hình nhấp nháy trong 1 giây: Lỗi được sửa, rác được dọn sạch, bản vẽ được zoom vừa vặn màn hình và tự động lưu lại tinh tươm!

## Chạy Script tự động cho hàng trăm bản vẽ (ScriptPro)

Để áp dụng file `DON_DEP.scr` cho cùng lúc 100 tệp DWG trong thư mục dự án mà không cần mở từng file:
- Sử dụng tiện ích miễn phí **ScriptPro** (hoặc **Autodesk Batch Script Runner**).
- Bạn chỉ việc chọn danh sách 100 file DWG, chọn file `DON_DEP.scr`, và bấm nút **Run**.
- Máy tính sẽ tự động mở từng file, thực thi kịch bản, lưu lại và đóng file. Bạn chỉ việc ngồi uống trà thưởng thức thành quả công nghệ tự động hóa!

> [!TIP]
> Trong khi ghi Action Recorder, bạn có thể nhấp chuột phải vào một bước trong danh sách hành động > chọn **Pause for User Input** để macro tạm dừng cho bạn bấm chuột chọn điểm trên màn hình, sau đó tự động chạy tiếp các bước sau.

## Tự kiểm tra

```quiz
id: q-ac-08-06-1
type: single
question: "Định dạng phần mở rộng (đuôi tệp) của tệp kịch bản dòng lệnh tự động hóa trong AutoCAD là gì?"
options:
  - text: ".scr"
    correct: true
    why: "SCR viết tắt của Script File."
  - text: ".bat"
    why: "BAT là tệp thực thi Batch của hệ điều hành Windows."
  - text: ".lsp"
    why: "LSP là tệp mã nguồn ngôn ngữ lập trình AutoLISP."
  - text: ".txt"
    why: "TXT là văn bản thuần túy, AutoCAD không nhận diện là kịch bản nếu chưa đổi đuôi .scr."
explain: "Tệp đuôi .scr là định dạng kịch bản chuỗi lệnh dòng lệnh tiêu chuẩn được thực thi qua lệnh SCRIPT."
```

```quiz
id: q-ac-08-06-2
type: single
question: "Cặp lệnh nào dùng để bắt đầu và kết thúc quá trình ghi lại chuỗi thao tác chuột thành macro tự động trong Action Recorder?"
options:
  - text: "ACTRECORD và ACTSTOP"
    correct: true
    why: "ACTRECORD bắt đầu ghi và ACTSTOP dừng ghi để lưu macro."
  - text: "REC và STOP"
    why: "REC và STOP không phải lệnh chuẩn của Action Recorder."
  - text: "START và END"
    why: "START/END không phải lệnh macro trong AutoCAD."
  - text: "RECORD và PAUSE"
    why: "PAUSE chỉ tạm dừng thao tác."
explain: "Sử dụng ACTRECORD để bật máy quay thao tác và ACTSTOP để đóng gói thành lệnh gõ tắt tự động."
```

```quiz
id: q-ac-08-06-3
type: truefalse
question: "Trong tệp kịch bản Script (.scr), một dấu xuống dòng (Enter) hoặc một khoảng trắng tương đương với việc người dùng nhấn phím Enter trên thanh dòng lệnh."
answer: true
explain: "Cơ chế đọc của trình thông dịch Script AutoCAD coi mỗi khoảng trắng hoặc ký tự ngắt dòng là một thao tác Enter chấp nhận thông số."
```

## Lỗi thường gặp

- **Chạy Script bị dừng giữa chừng:** Do trong file `.scr` bị thiếu một phím Enter (dấu ngắt dòng) hoặc bị thừa một khoảng trắng khiến lệnh chờ nhập liệu vô tận. Khắc phục: Mở Notepad kiểm tra kỹ từng dòng lệnh tương ứng với các bước nhắc trên CLI.
- **Tệp Script bị lưu thành đuôi .scr.txt:** Do khi lưu bằng Notepad người dùng để mặc định đuôi `.txt`. Khắc phục: Bật hiển thị đuôi file trong Windows và đổi tên bỏ phần `.txt`.

## Bài tập thực hành

- [ ] Gõ lệnh `ACTRECORD` để bắt đầu ghi lại chuỗi thao tác macro. <!-- expect: ACTRECORD -->
- [ ] Dùng `RECTANG` vẽ một hình chữ nhật kích thước 200 x 100 mm. <!-- expect: RECTANG -->
- [ ] Gõ lệnh `ACTSTOP` để dừng ghi và đặt tên macro là `TEST_MACRO`. <!-- expect: ACTSTOP -->
- [ ] Gõ lệnh `SCRIPT` để mở hộp thoại thực thi tệp kịch bản tự động hóa. <!-- expect: SCRIPT -->
- [ ] Bấm nút hủy hoặc đóng hộp thoại Script.

## Nguồn tham khảo

```links
- title: "Ghi và thực thi Action Macros từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Action+Macros"
  kind: official
- title: "Tự động hóa với Script Files từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=SCRIPT"
  kind: official
```
