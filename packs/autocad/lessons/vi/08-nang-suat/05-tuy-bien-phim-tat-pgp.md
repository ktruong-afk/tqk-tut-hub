---
id: ac-08-05
title: Tăng tốc độ vẽ 200% với tuỳ biến phím tắt lệnh acad.pgp
category: Nâng cao năng suất
tags: [pgp, aliasedit, reinit, phim-tat, toc-do-ve, meo-ve]
level: intermediate
minutes: 20
needs: [ac-08-01]
appVersions: ['2024', '2025']
edition: all
---
# Tăng tốc độ vẽ 200% với tuỳ biến phím tắt lệnh acad.pgp

> **Mục tiêu:**
> - Hiểu cấu trúc và nguyên lý định nghĩa phím tắt trong tệp tin [[PGP]] (`acad.pgp`).
> - Sử dụng công cụ `ALIASEDIT` hoặc chỉnh sửa trực tiếp tệp PGP để tùy biến phím tắt theo thói quen cá nhân.
> - Áp dụng quy tắc "Bàn tay trái" (Left-hand rule) và lệnh `REINIT` để cập nhật phím tắt tức thì mà không cần khởi động lại AutoCAD.

## Bí mật tốc độ của các cao thủ AutoCAD

Khi quan sát một kỹ sư CAD chuyên nghiệp làm việc, bạn sẽ thấy:
- Tay phải của họ **gắn chặt vào con chuột**, liên tục lia chuột và bấm bắt điểm cực kỳ chuẩn xác, không bao giờ rời chuột ra.
- Tay trái của họ **đặt cố định trên bàn phím**, ngón cái đè lên phím `Spacebar`, các ngón tay còn lại lướt thoăn thoắt trên các phím chữ bên nửa trái bàn phím (`Q, W, E, R, A, S, D, F, Z, X, C, V`).
- Họ hầu như không bao giờ ngước mắt lên thanh Ribbon để tìm nút bấm!

Nhưng trong thiết lập mặc định của AutoCAD, có rất nhiều lệnh hay dùng lại có phím tắt nằm ở tận bên phải bàn phím:
- Lệnh `MIRROR` (Lấy đối xứng) phím tắt là `MI` $\to$ Chữ `I` nằm bên phải!
- Lệnh `OFFSET` (Song song) phím tắt là `O` $\to$ Chữ `O` nằm bên phải!
- Lệnh `FILLET` (Bo góc) phím tắt là `F` $\to$ Tốt, nhưng `CHAMFER` lại là `CHA`!

Để giải phóng tối đa tốc độ vẽ, mọi kỹ sư đều tùy biến lại hệ thống phím tắt thông qua **Tệp định nghĩa phím tắt ([[PGP]] - `acad.pgp`)**.

## Quy tắc vàng "Bàn tay trái" (Left-Hand Rule)

Nguyên lý của quy tắc bàn tay trái là: **Đưa toàn bộ các lệnh thường dùng nhất về các phím chữ nằm ở nửa bên trái bàn phím (quanh các phím Q-W-E-R, A-S-D-F, Z-X-C-V)**.

Dưới đây là một số gợi ý phím tắt tay trái kinh điển giúp tăng gấp đôi tốc độ vẽ:

| Phím tắt mới | Lệnh thực thi | Gốc mặc định | Lợi ích |
|---|---|:---:|---|
| **`1`** hoặc **`Q`** | `LINE` | `L` | Không cần với tay sang chữ L |
| **`2`** hoặc **`W`** | `PLINE` | `PL` | Gọi nét Polyline cực nhanh |
| **`3`** hoặc **`E`** | `TRIM` | `TR` | Cắt tỉa nét chỉ bằng 1 ngón |
| **`4`** hoặc **`R`** | `EXTEND` | `EX` | Phóng dài nét cực nhanh |
| **`FF`** | `FILLET` | `F` | Gõ đúp phím F siêu tốc |
| **`CC`** | `COPY` | `CO / CP` | Gõ đúp phím C bằng ngón trỏ |
| **`MM`** | `MOVE` | `M` | Thao tác di chuyển thuận tay |
| **`D`** | `DIMLINEAR` | `DLI` | Đo kích thước chỉ với 1 chữ D |
| **`SD`** | `DIMSTYLE` | `D` | Nhường chữ D cho lệnh đo kích thước |

## Cách chỉnh sửa phím tắt từng bước

### Cách 1: Sử dụng công cụ đồ họa ALIASEDIT (Khuyên dùng)
Nếu bạn có cài đặt bộ công cụ *Express Tools* (tích hợp sẵn trong bản AutoCAD đầy đủ):
1. Gõ lệnh `ALIASEDIT` rồi nhấn [Enter] (hoặc vào menu *Express Tools* > cụm *Tools* > chọn **Command Aliases**).
2. Hộp thoại **acad.pgp - AutoCAD Command Aliases** xuất hiện với danh sách hàng trăm phím tắt.
3. Bấm nút **Add** để thêm phím tắt mới:
   - *Alias:* Nhập phím tắt mong muốn (ví dụ: `CC`).
   - *AutoCAD Command:* Nhập tên lệnh chuẩn (ví dụ: `COPY`).
4. Bấm **OK** > bấm **Apply**.
5. Một thông báo hỏi bạn có muốn cập nhật lại bộ nhớ không: Bấm **Yes**. Phím tắt mới có hiệu lực ngay lập tức!

### Cách 2: Chỉnh sửa trực tiếp tệp văn bản acad.pgp
1. Vào menu **Manage** trên thanh Ribbon > tại cụm *Customization* > bấm vào nút **Edit Aliases** (hoặc chọn *Edit Aliases* trong Application Menu).
2. Tệp tin văn bản `acad.pgp` sẽ được mở ra bằng phần mềm Notepad của Windows.
3. Cuộn chuột xuống tận đáy cùng của tệp tin (phần *User Defined Command Aliases*).
4. Thêm các dòng định nghĩa theo đúng cú pháp chuẩn:
   ```text
   <Phím tắt>, *<TÊN LỆNH CHUẨN>
   ```
   *Ví dụ minh họa:*
   ```text
   CC,   *COPY
   MM,   *MOVE
   FF,   *FILLET
   1,    *LINE
   2,    *PLINE
   ```
5. Lưu tệp Notepad lại ([Ctrl + S]) và đóng cửa sổ.

### Cập nhật phím tắt mới không cần khởi động lại AutoCAD (REINIT)
Thông thường khi sửa file văn bản PGP ngoài Windows, bạn phải tắt AutoCAD đi mở lại thì phần mềm mới nhận phím tắt mới. Nhưng bạn có thể nạp lại ngay lập tức với lệnh **`REINIT`**:
1. Gõ lệnh `REINIT` rồi nhấn [Enter].
2. Hộp thoại **Re-initialization** hiện ra: Đánh dấu tick vào ô **PGP file**.
3. Bấm **OK**. Toàn bộ phím tắt mới đã được nạp vào bộ nhớ RAM ngay tức khắc!

> [!TIP]
> Hãy sao lưu (copy) tệp `acad.pgp` của bạn lưu lên Google Drive hoặc USB. Bất cứ khi nào sang công ty mới hoặc dùng máy tính của người khác, bạn chỉ cần nạp file PGP quen thuộc của mình vào là có thể vẽ với tốc độ ánh sáng ngay lập tức!

## Tự kiểm tra

```quiz
id: q-ac-08-05-1
type: single
question: "Tệp tin văn bản nào trong hệ thống AutoCAD lưu trữ toàn bộ các định nghĩa phím tắt lệnh của phần mềm?"
options:
  - text: "acad.pgp"
    correct: true
    why: "PGP viết tắt của Program Parameters, lưu toàn bộ Command Aliases của AutoCAD."
  - text: "acad.cuix"
    why: "CUIX lưu cấu hình giao diện Ribbon và thanh công cụ."
  - text: "acad.lin"
    why: "LIN lưu định nghĩa các kiểu đường nét đứt Linetype."
  - text: "acad.pat"
    why: "PAT lưu định nghĩa các mẫu hoa văn mặt cắt Hatch."
explain: "Tệp acad.pgp là trái tim quản lý hệ thống phím tắt lệnh gõ tắt của mọi phiên bản AutoCAD."
```

```quiz
id: q-ac-08-05-2
type: single
question: "Lệnh nào cho phép nạp lại (Re-initialize) tệp acad.pgp vào bộ nhớ để phím tắt mới có hiệu lực ngay lập tức mà không cần tắt đi mở lại AutoCAD?"
options:
  - text: "REINIT"
    correct: true
    why: "REINIT khởi tạo lại driver và nạp lại cấu hình file PGP tức thì."
  - text: "REGEN"
    why: "REGEN chỉ làm mới bộ nhớ hiển thị đồ họa màn hình."
  - text: "RELOAD"
    why: "RELOAD dùng cho cập nhật tệp tham chiếu ngoài XREF."
  - text: "RESET"
    why: "RESET đưa các thiết lập về mặc định xuất xưởng."
explain: "Sử dụng REINIT sau khi sửa file acad.pgp để áp dụng ngay phím tắt mới mà không làm gián đoạn công việc."
```

```quiz
id: q-ac-08-05-3
type: truefalse
question: "Quy tắc 'Bàn tay trái' khuyến khích chuyển các lệnh vẽ hay dùng nhất về các phím chữ bên nửa trái bàn phím để tay phải không phải rời chuột."
answer: true
explain: "Quy tắc này giúp tối ưu hóa công thái học, giúp một tay rê chuột một tay gõ phím nhịp nhàng tăng gấp đôi hiệu suất làm việc."
```

## Lỗi thường gặp

- **Gõ phím tắt mới nhưng AutoCAD không nhận:** Do quên chưa chạy lệnh `REINIT` sau khi sửa file PGP, hoặc gõ sai cú pháp (quên dấu phẩy `,` hoặc dấu sao `*` trước tên lệnh).
- **Trùng phím tắt với lệnh mặc định:** Khi bạn gán chữ `D` cho `DIMLINEAR`, lệnh gốc `DIMSTYLE` sẽ bị ghi đè. Cần gán cho `DIMSTYLE` một phím tắt khác như `SD` để không bị mất lệnh.

## Bài tập thực hành

- [ ] Gõ lệnh `ALIASEDIT` để mở trình quản lý phím tắt đồ họa acad.pgp. <!-- expect: ALIASEDIT -->
- [ ] Quan sát danh sách các phím tắt lệnh hiện có trong hệ thống.
- [ ] Bấm nút đóng hoặc Cancel để thoát khỏi hộp thoại.
- [ ] Mở ứng dụng Notepad xem nội dung file `acad.pgp` qua Application Menu.
- [ ] Gõ lệnh `OPTIONS` để kiểm tra các tùy chọn cấu hình hệ thống. <!-- expect: OPTIONS -->

## Nguồn tham khảo

```links
- title: "Tùy biến phím tắt Command Aliases (PGP) từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Command+Aliases"
  kind: official
- title: "Lệnh ALIASEDIT quản lý phím tắt từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=ALIASEDIT"
  kind: official
```
