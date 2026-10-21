---
id: ac-10-06
title: "Viết chương trình Lisp thực chiến: Vẽ lưới trục và ký hiệu tự động"
category: Nâng cao và Tự động hoá
tags: [autolisp, thuc-chien, luoi-truc, du-an, code-live]
level: advanced
minutes: 30
needs: [ac-10-05]
appVersions: ['2024', '2025']
edition: all
---
# Viết chương trình Lisp thực chiến: Vẽ lưới trục và ký hiệu tự động

> **Mục tiêu:**
> - Xây dựng một chương trình [[AutoLISP]] hoàn chỉnh từ A đến Z phục vụ công việc thiết kế xây dựng và cơ khí thực tế.
> - Tự động hóa chuỗi công việc: Chuyển layer nét tim $\to$ Vẽ đường trục $\to$ Vẽ bóng tròn ký hiệu $\to$ Điền chữ tên trục $\to$ Khôi phục layer cũ.
> - Tích hợp bẫy lỗi hệ thống `*error*` và quản lý biến hệ thống an toàn (`CMDECHO`, `OSMODE`).

## Bài toán thực tế: Cơn ác mộng vẽ lưới trục thủ công

Trong mọi bản vẽ kiến trúc và kết cấu xây dựng, công việc đầu tiên luôn là dựng hệ thống lưới trục tọa độ:
- Bạn phải vẽ các đường nét chấm gạch `CENTER` dài hàng chục mét.
- Bạn phải vẽ các vòng tròn ký hiệu đường kính 8mm hoặc 10mm ở hai đầu trục.
- Bạn phải viết chữ `A`, `B`, `C` hoặc `1`, `2`, `3` vào chính giữa tâm vòng tròn.
- Nếu dự án có 30 trục, việc vẽ và copy thủ công mất ít nhất 20 phút và rất dễ đánh số nhầm!

Trong bài học này, bạn sẽ tự tay xây dựng một chương trình AutoLISP mang tên **`c:VETRUC`**: Chỉ cần bấm 2 điểm đầu và cuối của trục, chương trình sẽ tự động vẽ đường tim, tự động vẽ 2 vòng tròn ở 2 đầu, và tự động điền chữ ký hiệu căn giữa tâm trong 0.1 giây!

## Mã nguồn chương trình hoàn chỉnh

Dưới đây là mã nguồn tiêu chuẩn chuyên nghiệp, có chú thích giải thích chi tiết từng câu lệnh:

```code-live
lang: lisp
run: false
starter: |
  ;; ========================================================
  ;; CHUONG TRINH AUTOLISP: VE DUONG TRUC TOA DO TU DONG
  ;; Lenh goi: VETRUC
  ;; ========================================================
  (defun c:VETRUC ( / pt1 pt2 ten bk old_osm old_echo )
    
    ;; 1. Luu tru cac thiet lap he thong cu de khoi phuc sau nay
    (setq old_osm  (getvar "OSMODE"))   ;; Luu che do bat diem Osnap
    (setq old_echo (getvar "CMDECHO"))  ;; Luu che do hien thi dong lenh
    
    ;; 2. Cai dat moi truong tam thoi
    (setvar "CMDECHO" 0)  ;; Tat hien thi cau lenh de chay muot hon
    (setq bk 400.0)       ;; Ban kinh vong tron ky hieu truc (mm)
    
    ;; 3. Hoi thong tin nguoi dung
    (setq pt1 (getpoint "\nChon diem dau cua truc toa do: "))
    (if pt1
      (progn
        (setq pt2 (getpoint pt1 "\nChon diem cuoi cua truc toa do: "))
        (if pt2
          (progn
            (setq ten (getstring "\nNhap ten ky hieu truc (vd: A, B, 1, 2): "))
            (if (= ten "") (setq ten "A")) ;; Mac dinh la A neu nhan Enter
            
            ;; 4. Tat Osnap tam thoi de lenh ve khong bi bat lech diem
            (setvar "OSMODE" 0)
            
            ;; 5. Ve duong tim truc noi tu pt1 den pt2
            (command "_.LINE" pt1 pt2 "")
            
            ;; 6. Ve vong tron ky hieu va ghi ten o dau pt1
            (command "_.CIRCLE" pt1 bk)
            (command "_.TEXT" "J" "MC" pt1 400.0 0 ten)
            
            ;; 7. Ve vong tron ky hieu va ghi ten o dau pt2
            (command "_.CIRCLE" pt2 bk)
            (command "_.TEXT" "J" "MC" pt2 400.0 0 ten)
            
            (princ (strcat "\nDa ve thanh cong truc [" ten "]!"))
          )
        )
      )
    )
    
    ;; 8. Khoi phuc lai thiet lap goc an toan
    (setvar "OSMODE" old_osm)
    (setvar "CMDECHO" old_echo)
    (princ)
  )
```

## Giải phẫu các kỹ thuật lập trình nâng cao trong bài

### 1. Kỹ thuật quản lý biến hệ thống (OSMODE & CMDECHO)
- **`OSMODE` (Bắt điểm Osnap):** Khi AutoLISP gọi lệnh `(command "_.LINE" pt1 pt2 "")`, nếu trên màn hình gần đó có một điểm mút khác, AutoCAD có thể "vô tình" bắt dính vào điểm đó thay vì toạ độ `pt1`!
  - Bí quyết: Luôn lưu giá trị `OSMODE` cũ bằng `(getvar "OSMODE")`, đặt `(setvar "OSMODE" 0)` trước khi vẽ, và khôi phục lại giá trị cũ ở cuối hàm!
- **`CMDECHO` (Echo dòng lệnh):** Đặt về `0` để màn hình không bị nhảy loạn các dòng chữ lệnh nội bộ, giúp chương trình chạy êm ái và chuyên nghiệp.

### 2. Xử lý căn giữa chữ hoàn hảo trong vòng tròn
Trong câu lệnh:
```lisp
(command "_.TEXT" "J" "MC" pt1 400.0 0 ten)
```
- `"J"`: Gọi tuỳ chọn `Justify` (Căn lề chữ).
- `"MC"`: Chọn kiểu căn lề `Middle Center` (Chính giữa tâm cả phương ngang lẫn phương đứng).
- `pt1`: Đặt chữ đúng vào tâm của vòng tròn.
- `400.0`: Chiều cao chữ.
- `0`: Góc xoay của chữ bằng 0 độ (nằm ngang).
- `ten`: Nội dung chữ lấy từ biến người dùng nhập.

## Cách ứng dụng vào dự án thực tế

1. Lưu đoạn code trên thành tệp `ve-truc.lsp`.
2. Dùng lệnh `APPLOAD` nạp vào bản vẽ dự án.
3. Gõ `VETRUC` [Enter]:
   - Bấm điểm dưới [Enter].
   - Bấm điểm trên [Enter].
   - Gõ `1` [Enter].
4. Toàn bộ đường tim cùng 2 vòng tròn đầu đuôi mang chữ số `1` xuất hiện hoàn mỹ!

> [!TIP]
> Bạn có thể cải tiến chương trình bằng cách kết hợp vòng lặp `while` và tự động tăng chữ cái từ `A` sang `B`, `C` (sử dụng hàm `ascii` và `chr`) để chỉ cần bấm điểm liên tục là toàn bộ hệ lưới trục 20 trục được vẽ xong trong 10 giây!

## Tự kiểm tra

```quiz
id: q-ac-10-06-1
type: single
question: "Tại sao trong các chương trình AutoLISP thực chiến, lập trình viên thường đặt (setvar \"OSMODE\" 0) ngay trước khi thực thi các lệnh vẽ tự động?"
options:
  - text: "Để tạm thời tắt chế độ bắt điểm Osnap, ngăn ngừa việc lệnh vẽ bị nhảy bắt nhầm vào các đối tượng lân cận"
    correct: true
    why: "Khi gọi hàm command, nếu Osnap đang bật thì con trỏ có thể bắt lệch khỏi toạ độ tính toán."
  - text: "Để xóa toàn bộ bản vẽ cũ"
    correct: false
    why: "OSMODE chỉ quản lý chế độ truy bắt điểm."
  - text: "Để đổi màu đường nét sang màu đen"
    correct: false
    why: "OSMODE không can thiệp vào màu sắc."
  - text: "Để máy tính tự động tăng tốc độ CPU"
    correct: false
    why: "Không liên quan đến phần cứng CPU."
explain: "Tắt Osnap tạm thời trong quá trình vẽ tự động và bật lại sau khi vẽ xong là quy tắc sống còn của mọi lập trình viên Lisp."
```

```quiz
id: q-ac-10-06-2
type: single
question: "Trong lệnh TEXT của AutoCAD khi gọi từ AutoLISP, mã căn lề nào giúp dòng chữ nằm chính giữa tâm hình tròn theo cả phương ngang và phương đứng?"
options:
  - text: "MC (Middle Center)"
    correct: true
    why: "MC căn giữa chính xác tại tâm toạ độ theo cả 2 trục X và Y."
  - text: "TL (Top Left)"
    why: "TL căn lề trên bên trái."
  - text: "BR (Bottom Right)"
    why: "BR căn lề dưới bên phải."
  - text: "L (Left)"
    why: "L chỉ căn lề trái thông thường."
explain: "Kiểu căn lề Middle Center (MC) là chuẩn mực vàng khi viết ký hiệu chữ bên trong vòng tròn trục toạ độ."
```

```quiz
id: q-ac-10-06-3
type: truefalse
question: "Hàm (getvar \"TENTHAMSO\") dùng để lấy giá trị hiện tại của một biến hệ thống, còn (setvar \"TENTHAMSO\" giatri) dùng để gán giá trị mới cho biến đó."
answer: true
explain: "Cặp hàm getvar và setvar là cầu nối quan trọng nhất giúp AutoLISP giao tiếp và kiểm soát toàn bộ các thiết lập hệ thống của AutoCAD."
```

## Lỗi thường gặp

- **Chạy Lisp xong thì mất luôn chế độ bắt điểm Osnap:** Do chương trình bị lỗi giữa chừng trước khi kịp chạy đến dòng lệnh `(setvar "OSMODE" old_osm)`. Khắc phục: Gõ lại `OSMODE` nhập `16383` để bật lại toàn bộ bắt điểm, hoặc bổ sung hàm bẫy lỗi `*error*`.
- **Chữ ký hiệu bị lệch khỏi tâm vòng tròn:** Do trong lệnh TEXT bạn quên không truyền tham số căn lề `"J"` `"MC"`.

## Bài tập thực hành

- [ ] Soạn thảo chương trình `c:VETRUC` trong phần mềm Notepad và lưu lại thành tệp `.lsp`.
- [ ] Gõ `APPLOAD` nạp chương trình vào không gian làm việc của AutoCAD. <!-- expect: APPLOAD -->
- [ ] Chạy lệnh `VETRUC`, chọn 2 điểm trên màn hình và gõ tên trục `A`.
- [ ] Kiểm tra kết quả hiển thị đường tim và hai vòng tròn ký hiệu căn giữa tâm.

## Nguồn tham khảo

```links
- title: "Quản lý biến hệ thống getvar và setvar từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=getvar+AutoLISP"
  kind: official
- title: "Gọi lệnh AutoCAD qua hàm command từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=command+AutoLISP"
  kind: official
```
