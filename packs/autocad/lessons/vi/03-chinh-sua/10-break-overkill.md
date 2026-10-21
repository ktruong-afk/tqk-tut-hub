---
id: ac-03-10
title: Bẻ gãy với BREAK và làm sạch bản vẽ với OVERKILL
category: Chỉnh sửa
tags: [break, overkill, lam-sach, xoa-net-trung, be-gay, chinh-sua]
level: beginner
minutes: 15
needs: [ac-03-05]
appVersions: ['2024', '2025']
edition: all
---
# Bẻ gãy với BREAK và làm sạch bản vẽ với OVERKILL

> **Mục tiêu:**
> - Sử dụng lệnh BREAK để bẻ đôi đoạn thẳng tại một điểm hoặc khoét một khoảng hở giữa hai điểm mốc.
> - Sử dụng lệnh OVERKILL để tự động quét tìm và xoá sạch hàng nghìn nét vẽ thừa, nét trùng đè lên nhau.
> - Dọn dẹp bản vẽ kỹ thuật nhẹ nhàng, tăng tốc độ xử lý và ngăn ngừa lỗi khi in ấn hoặc cắt CNC.

## Lệnh này làm gì và khi nào dùng

Khi làm việc với các bản vẽ cơ khí hoặc nhận file bản vẽ từ đối tác gửi tới, có hai vấn đề rất hay gặp phải:
1. Bạn muốn ngắt đôi một đoạn thẳng tại đúng một điểm (Break at Point) để gán layer khác hoặc khoét một khe hở để chèn ký hiệu thiết bị. Lệnh `TRIM` đòi hỏi phải có đường dao cắt chéo qua, còn lệnh `BREAK` (phím tắt `BR`) cho phép bạn bẻ gãy tự do tại bất kỳ vị trí nào mà không cần dao cắt phụ.
2. Bản vẽ bị vẽ ẩu: nhiều đoạn thẳng bị vẽ đè chồng lên nhau 2-3 lớp, hoặc một đường thẳng dài bị đứt vụn thành hàng chục mẩu con xếp thẳng hàng. Lỗi này làm file rất nặng, khi in nét sẽ bị nhoè mực đen xì và máy cắt CNC sẽ chạy đi chạy lại cắt nát phôi. Lệnh cứu tinh ở đây là `OVERKILL`.

## Cách dùng từng bước

1. **Bẻ gãy một khoảng hở bằng BREAK:**
   - Gõ `BREAK` hoặc phím tắt `BR` rồi nhấn [Enter].
   - Nhấp chuột chọn đối tượng tại điểm bắt đầu muốn cắt (First break point).
   - Nhấp chuột vào điểm thứ hai (Second break point): Khoảng thân giữa hai điểm bấm sẽ bị cắt đứt khoét rỗng và biến mất.
2. **Bẻ đôi đoạn thẳng tại đúng 1 điểm (Break at Point):**
   - Gõ `BR` [Enter], nhấp chọn đoạn thẳng.
   - Gõ chữ `F` (First point) rồi [Enter].
   - Dùng Osnap nhấp chính xác vào điểm muốn chia đôi (ví dụ giao điểm Intersection hoặc Midpoint).
   - Khi dòng lệnh hỏi `Specify second break point:`, gõ ký tự `@` rồi nhấn [Enter].
   - Kết quả: Đoạn thẳng bị chặt đôi thành 2 đoạn độc lập ngay tại điểm đó mà không có bất kỳ khoảng hở nào bị mất!
3. **Làm sạch nét trùng đè bằng OVERKILL:**
   - Gõ lệnh `OVERKILL` rồi nhấn [Enter].
   - Quét chọn toàn bộ bản vẽ (hoặc nhấn [Ctrl + A]) rồi nhấn [Enter]. Hộp thoại *Delete Duplicate Objects* xuất hiện.
   - Giữ nguyên các tuỳ chọn mặc định:
     - Tích chọn *Ignore object property* (Color, Layer, Linetype...) nếu muốn xoá cả nét trùng khác màu.
     - Tích chọn *Optimize segments within polylines* (Làm sạch các mẩu vụn trong đa tuyến).
     - Tích chọn *Combine colinear objects that partially overlap* (Gộp các đoạn thẳng trùng một phần).
   - Bấm **OK**. Quan sát dòng thông báo dưới dòng lệnh (ví dụ: *"45 duplicate objects deleted, 28 overlapping objects combined"*).

## Tuỳ chọn và mẹo

> [!TIP]
> Luôn chạy lệnh `OVERKILL` trước khi gửi bản vẽ đi xuất file cắt laser CNC hoặc gửi cho đối tác. Lệnh này giúp giảm tới 30% dung lượng file và loại bỏ hoàn toàn các đường vẽ rác tiềm ẩn.

> [!TIP]
> Trên Ribbon (*Home > Modify flyout*), có nút bấm riêng mang tên **Break at Point** giúp bạn bẻ đôi đối tượng tại 1 điểm chỉ bằng 2 cú nhấp chuột mà không cần gõ mẹo `@`.

## Tự kiểm tra

```quiz
id: q-ac-03-010-1
type: single
question: Lệnh OVERKILL trong AutoCAD có tác dụng chính là gì?
options:
  - text: Tự động tìm và xoá bỏ các nét vẽ trùng lặp, gộp các đoạn thẳng thẳng hàng đè lên nhau
    correct: true
    why: OVERKILL là công cụ dọn rác nét vẽ trùng lặp cực kỳ mạnh mẽ
  - text: Xoá toàn bộ bản vẽ chỉ trong một lệnh duy nhất
    why: Xoá tất cả dùng lệnh ERASE kết hợp ALL
  - text: Tắt máy tính sau khi lưu bản vẽ
    why: AutoCAD không có chức năng tắt máy tính
  - text: Phá vỡ toàn bộ khối Block
    why: Phá vỡ khối là lệnh EXPLODE
explain: "Lệnh OVERKILL tự động quét toàn bộ bản vẽ để phát hiện và triệt tiêu các đối tượng hình học vẽ đè chồng lên nhau, đồng thời nối gộp các đoạn thẳng thẳng hàng bị cắt vụn."
tags: [overkill, don-rac, lam-sach]
```

```quiz
id: q-ac-03-010-2
type: single
question: Để bẻ đôi một đoạn thẳng tại đúng một điểm mốc bằng lệnh BREAK mà không làm mất đi bất kỳ milimet khoảng hở nào, bạn nhập ký tự nào ở bước chọn điểm thứ hai?
options:
  - text: Ký tự "@"
    correct: true
    why: Ký tự @ quy định điểm thứ hai trùng khít 100% với điểm thứ nhất
  - text: Ký tự "#"
    why: Ký tự # dùng cho toạ độ tuyệt đối
  - text: Ký tự "$"
    why: Ký tự $ không có ý nghĩa trong lệnh BREAK
  - text: Phím số 0
    why: Số 0 sẽ bị hiểu là toạ độ gốc
explain: "Mẹo kinh điển của lệnh BREAK: Sau khi chọn điểm cắt First point, gõ ký tự @ ở Second point sẽ giúp chia đôi đoạn thẳng thành hai nửa tiếp giáp khít nhau."
tags: [break, at-point, meo]
```

```quiz
id: q-ac-03-010-3
type: truefalse
question: Chạy lệnh OVERKILL lên bản vẽ sẽ làm thay đổi kích thước và hình dáng của các chi tiết kỹ thuật.
answer: false
explain: "Lệnh OVERKILL chỉ loại bỏ các nét vẽ dư thừa, nét trùng khít lên nhau hoặc gộp các đoạn thẳng thẳng hàng, hoàn toàn không làm thay đổi hình dáng hay kích thước của bản vẽ."
tags: [overkill, an-toan]
```

## Lỗi thường gặp

- **Triệu chứng:** Dùng lệnh BREAK nhưng khoảng hở bị khoét quá rộng không đúng vị trí.
  - *Nguyên nhân:* Nhấp chuột chọn đối tượng ở đâu thì AutoCAD mặc định lấy luôn cú nhấp đó làm điểm cắt thứ nhất (First point).
  - *Cách sửa:* Sau khi chọn đối tượng, hãy gõ ngay chữ `F` (First point) để chỉ định lại chính xác điểm bắt đầu cắt bằng Osnap.
- **Triệu chứng:** Chạy lệnh OVERKILL xong nhưng một số nét trùng vẫn còn nguyên.
  - *Nguyên nhân:* Các nét đó thuộc hai layer khác nhau hoặc màu khác nhau và trong bảng OVERKILL chưa tích chọn mục *Ignore Layer / Color*.
  - *Cách sửa:* Gõ lại `OVERKILL`, tích chọn vào các ô kiểm trong mục *Ignore Object Properties* rồi bấm OK.

## Bài tập thực hành

- [ ] Gõ `LINE` vẽ một đoạn thẳng dài 150mm. <!-- expect: LINE -->
- [ ] Gõ `LINE` vẽ đè một đoạn thẳng khác dài 80mm trùng khít lên thân đoạn thẳng ban đầu. <!-- expect: LINE -->
- [ ] Gõ `OVERKILL`, quét chọn cả khu vực và bấm OK. Quan sát dòng lệnh báo 1 đối tượng trùng đã được xoá sạch. <!-- expect: OVERKILL -->
- [ ] Gõ `LINE` vẽ một đoạn thẳng mới dài 120mm. <!-- expect: LINE -->
- [ ] Gõ `BREAK`, chọn đoạn thẳng, gõ `F`, bắt điểm Midpoint làm điểm cắt và gõ `@` để bẻ đôi đoạn thẳng thành 2 nửa. <!-- expect: BREAK -->

## Nguồn tham khảo

```links
- title: Lệnh OVERKILL dọn dẹp nét vẽ trùng (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=OVERKILL+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về các tuỳ chọn dung sai Tolerance và lọc thuộc tính của OVERKILL
- title: Lệnh BREAK bẻ gãy đối tượng hình học (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=BREAK+Command
  kind: official
  lang: en
  note: Hướng dẫn thao tác bẻ đôi và khoét khoảng hở trên Line, Arc, Polyline
```
