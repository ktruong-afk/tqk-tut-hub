---
id: ac-04-04
title: Tỷ lệ hiển thị đường nét với LTSCALE và PSLTSCALE
category: Layer & Thuộc tính
tags: [ltscale, psltscale, celtscale, ti-le-duong, net-dut, hidden, center]
level: beginner
minutes: 15
needs: [ac-04-02]
appVersions: ['2024', '2025']
edition: all
---
# Tỷ lệ hiển thị đường nét với LTSCALE và PSLTSCALE

> **Mục tiêu:**
> - Sử dụng lệnh LTSCALE để điều chỉnh tỷ lệ hiển thị toàn cục của các đường nét đứt, nét gạch chấm trên bản vẽ.
> - Hiểu rõ sự tương tác giữa LTSCALE (Model Space) và PSLTSCALE (Paper Space / Layout in ấn).
> - Điều chỉnh tỷ lệ cục bộ cho từng đoạn nét cá biệt bằng biến CELTSCALE hoặc bảng Properties.

## Lệnh này làm gì và khi nào dùng

Đây là tình huống "huyền thoại" mà 100% người học AutoCAD đều từng gặp phải: Bạn đã nạp đúng kiểu đường `HIDDEN` (nét đứt) và gán cho Layer, nhưng khi vẽ ra màn hình, đường thẳng nhìn vẫn **liền tù tì như nét thẳng thông thường**! Hoặc ngược lại, nét đứt bị thưa tới mức một đoạn dài 100mm chỉ có đúng 1 khoảng hở to đùng.

Nguyên nhân nằm ở [[Tỷ lệ kiểu đường]] (Linetype Scale). Một mẫu nét đứt trong file định nghĩa có chiều dài gạch chuẩn khoảng 6mm đến 12mm:
- Nếu bạn vẽ chi tiết cơ khí dài 20mm thì khoảng gạch 12mm sẽ quá to (chỉ thấy nét liền).
- Nếu bạn vẽ toà nhà dài 50 mét (50,000mm) thì khoảng gạch 12mm lại quá bé như hạt cát (mắt người nhìn thấy liền).

AutoCAD cung cấp bộ 3 biến hệ thống để giải quyết triệt để vấn đề này:
- `LTSCALE` (phím tắt `LTS`): Hệ số tỷ lệ kiểu đường toàn cục (Global Scale Factor) áp dụng cho toàn bộ bản vẽ.
- `PSLTSCALE`: Điều khiển tỷ lệ nét đứt trong không gian Layout in ấn (bằng 1 thì in khổ nào nét cũng đều tăm tắp).
- `CELTSCALE`: Hệ số tỷ lệ riêng cho từng đối tượng cá biệt.

## Cách dùng từng bước

1. **Điều chỉnh tỷ lệ toàn cục bằng LTSCALE:**
   - Gõ lệnh `LTSCALE` hoặc phím tắt `LTS` rồi nhấn [Enter].
   - Dòng lệnh hiển thị giá trị hiện tại: `Enter new linetype scale factor <1.0000>:`.
   - Nhập một giá trị mới phù hợp với tầm nhìn bản vẽ:
     - Nếu nét đứt đang bị nhìn như nét liền trên bản vẽ cơ khí nhỏ: Thử giảm xuống `0.5` hoặc `0.2` rồi nhấn [Enter].
     - Nếu nét đứt đang bị nhìn như nét liền trên bản vẽ kiến trúc toà nhà lớn: Thử tăng lên `10`, `20` hoặc `50` rồi nhấn [Enter].
   - Quan sát các đường nét đứt và nét tâm trên màn hình: Các mắt gạch chấm sẽ lập tức co giãn vừa vặn tầm mắt!
2. **Làm mới hiển thị nếu chưa thấy đổi:**
   - Nếu sau khi đổi LTSCALE mà hình chưa đổi, hãy gõ lệnh `REGEN` (phím tắt `RE`) rồi nhấn [Enter] để AutoCAD vẽ lại đồ hoạ màn hình.
3. **Chỉnh tỷ lệ cục bộ cho 1 đoạn nét cá biệt:**
   - Nếu trong bản vẽ có một đoạn nét đứt quá ngắn mà bạn muốn nó dày mắt gạch hơn các đoạn khác:
   - Nhấp chọn riêng đoạn nét đó, mở bảng `PROPERTIES` ([Ctrl + 1]).
   - Tìm dòng *Linetype Scale* (mặc định là `1.0`), đổi thành `0.5` hoặc `0.3`.
   - Chỉ duy nhất đoạn nét đó đổi tỷ lệ, không làm ảnh hưởng đến các đường khác trong bản vẽ.

## Tuỳ chọn và mẹo

> [!TIP]
> Tỷ lệ LTSCALE tối ưu thường tỷ lệ thuận với tỷ lệ in của bản vẽ: Nếu bản vẽ dự kiến in tỷ lệ 1:100, giá trị LTSCALE thường dao động quanh mức 50 đến 100. Với bản vẽ cơ khí tỷ lệ 1:1, LTSCALE thường để từ 0.5 đến 1.0.

> [!TIP]
> Luôn đặt biến `PSLTSCALE = 1` khi làm việc với khung nhìn Layout. Biến này giúp nét đứt ở mọi khung nhìn viewport phóng to hay thu nhỏ đều tự động hiển thị kích thước gạch bằng nhau khi in ra giấy.

## Tự kiểm tra

```quiz
id: q-ac-04-04-1
type: single
question: Khi đã chọn đúng kiểu đường HIDDEN nhưng đường nét trên màn hình Model vẫn hiển thị như nét liền, lệnh nào dùng để khắc phục nhanh nhất?
options:
  - text: LTSCALE (phím tắt LTS) và thay đổi hệ số tỷ lệ phù hợp
    correct: true
    why: LTSCALE điều chỉnh kích thước hiển thị của các khoảng gạch nét đứt trên toàn bản vẽ
  - text: ERASE và vẽ lại từ đầu
    why: Vẽ lại vẫn bị nét liền nếu không chỉnh LTSCALE
  - text: EXPLODE
    why: EXPLODE không chỉnh được kiểu đường
  - text: UNITS
    why: UNITS chỉnh đơn vị đo, không trực tiếp phóng to mắt nét đứt
explain: "Lệnh LTSCALE (gõ tắt LTS) thay đổi hệ số tỷ lệ hiển thị toàn cục cho tất cả các kiểu đường nét đứt và gạch chấm, giúp mắt gạch hiển thị vừa vặn với kích thước vùng vẽ."
tags: [ltscale, net-dut, linetype]
```

```quiz
id: q-ac-04-04-2
type: single
question: Để thay đổi tỷ lệ kiểu đường nét đứt riêng cho một đoạn thẳng duy nhất mà không làm ảnh hưởng đến toàn bộ bản vẽ, bạn chỉnh sửa thông số nào?
options:
  - text: Mục "Linetype Scale" trong bảng thuộc tính Properties (Ctrl + 1) của đối tượng đó
    correct: true
    why: Linetype Scale trong bảng Properties chỉ áp dụng cục bộ cho đối tượng được chọn
  - text: Lệnh LTSCALE
    why: LTSCALE thay đổi toàn bộ bản vẽ
  - text: Lệnh ZOOM
    why: ZOOM chỉ thay đổi góc nhìn camera
  - text: Lệnh REGEN
    why: REGEN chỉ tính toán lại đồ hoạ
explain: "Trong bảng Properties ([Ctrl + 1]), trường thông tin Linetype Scale cho phép bạn tuỳ chỉnh hệ số co giãn nét đứt cục bộ cho riêng từng đối tượng cụ thể."
tags: [properties, linetype-scale, cuc-bo]
```

```quiz
id: q-ac-04-04-3
type: truefalse
question: Biến hệ thống PSLTSCALE đặt bằng 1 giúp các nét đứt trên bản vẽ in ấn (Layout) hiển thị đồng nhất kích thước dù khung nhìn Viewport có tỷ lệ phóng to hay thu nhỏ khác nhau.
answer: true
explain: "PSLTSCALE = 1 (Paper Space Linetype Scale) là chuẩn mực in ấn trong AutoCAD, tự động bù trừ tỷ lệ viewport để mọi nét đứt khi in ra giấy đều có cự ly gạch chấm chuẩn xác như nhau."
tags: [psltscale, layout, in-an]
```

## Lỗi thường gặp

- **Triệu chứng:** Thay đổi giá trị LTSCALE từ 1 sang 10 nhưng trên màn hình các nét vẽ không hề thay đổi chút nào.
  - *Nguyên nhân:* Bộ nhớ đồ hoạ của AutoCAD chưa kịp tính toán lại hiển thị.
  - *Cách sửa:* Gõ ngay lệnh `REGEN` (phím tắt `RE`) rồi nhấn [Enter] để ép AutoCAD vẽ lại màn hình.
- **Triệu chứng:** Trên không gian Model nhìn nét đứt rất đẹp, nhưng khi chuyển sang không gian Layout giấy in thì nét lại biến thành nét liền.
  - *Nguyên nhân:* Biến `PSLTSCALE` đang đặt bằng 0 hoặc chưa đồng bộ biến `MSLTSCALE`.
  - *Cách sửa:* Gõ `PSLTSCALE` đặt bằng `1`, gõ `MSLTSCALE` đặt bằng `1`, sau đó gõ `REGENALL` để làm mới toàn bộ các khung nhìn.

## Bài tập thực hành

- [ ] Gõ `LINE` vẽ một đoạn thẳng dài `500`mm. <!-- expect: LINE -->
- [ ] Chọn đoạn thẳng và gán kiểu đường là `HIDDEN` từ bảng Properties.
- [ ] Gõ `LTSCALE` và quan sát giá trị hiện tại (mặc định 1.0). <!-- expect: LTSCALE -->
- [ ] Nhập giá trị mới là `10` rồi nhấn [Enter].
- [ ] Gõ `REGEN` để làm mới màn hình và quan sát các mắt nét đứt hiện rõ mồn một. <!-- expect: REGEN -->

## Nguồn tham khảo

```links
- title: Lệnh LTSCALE và tỷ lệ hiển thị nét đứt (Autodesk Help chính thức)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=LTSCALE+Command
  kind: official
  lang: en
  note: Hướng dẫn chính thức về LTSCALE, PSLTSCALE, MSLTSCALE và CELTSCALE
- title: Đồng bộ nét đứt giữa Model và Layout (Autodesk Support)
  url: https://help.autodesk.com/view/ACD/2024/ENU/?query=Linetypes+in+Paper+Space
  kind: official
  lang: en
  note: Phương pháp chuẩn hoá tỷ lệ đường nét khi xuất bản vẽ in ấn chuyên nghiệp
```
