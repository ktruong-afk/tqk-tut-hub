---
id: ac-10-05
title: Xử lý danh sách toạ độ và vòng lặp trong AutoLISP
category: Nâng cao và Tự động hoá
tags: [autolisp, list, car, cadr, repeat, while, vong-lap]
level: advanced
minutes: 25
needs: [ac-10-04]
appVersions: ['2024', '2025']
edition: all
---
# Xử lý danh sách toạ độ và vòng lặp trong AutoLISP

> **Mục tiêu:**
> - Hiểu bản chất toạ độ điểm trong AutoCAD thực chất là một danh sách số học (`List`).
> - Sử dụng các hàm xử lý danh sách kinh điển (`car`, `cadr`, `caddr`, `list`, `cons`, `nth`) để trích xuất toạ độ X, Y, Z.
> - Làm chủ cấu trúc vòng lặp lặp lại `repeat` và vòng lặp có điều kiện `while` để vẽ hàng loạt đối tượng tự động.

## Bản chất của LISP: Mọi thứ đều là danh sách (List)

Cái tên **LISP** vốn là chữ viết tắt của **LIS**t **P**rocessing (Xử lý danh sách). Trong [[AutoLISP]]:
- Toạ độ một điểm $P(100, 250, 0)$ trên bản vẽ: Được biểu diễn dưới dạng danh sách 3 phần tử: `(100.0 250.0 0.0)`.
- Một tam giác: Là danh sách gồm 3 điểm toạ độ `(pt1 pt2 pt3)`.
- Một tập hợp đối tượng chọn trên màn hình (`Selection Set`): Cũng được quản lý dưới dạng danh sách!

Vì vậy, nếu muốn trở thành một lập trình viên AutoLISP thực thụ, bạn bắt buộc phải làm chủ các công cụ mổ xẻ và lắp ráp danh sách.

## 1. Mổ xẻ toạ độ điểm với car, cadr và caddr

Khi hàm `(getpoint)` trả về điểm `pt` là danh sách `(100.0 250.0 50.0)`:
- **`car`:** Lấy phần tử **đầu tiên** của danh sách $\to$ Chính là toạ độ **X**!
  `(car pt)` $\to$ Trả về `100.0`.
- **`cadr`:** Lấy phần tử **thứ hai** của danh sách $\to$ Chính là toạ độ **Y**!
  `(cadr pt)` $\to$ Trả về `250.0`.
- **`caddr`:** Lấy phần tử **thứ ba** của danh sách $\to$ Chính là toạ độ **Z**!
  `(caddr pt)` $\to$ Trả về `50.0`.

### Cách tạo toạ độ điểm mới với hàm list:
Bạn muốn tính toạ độ một điểm mới `pt2` nằm dịch sang bên phải 500mm so với điểm gốc `pt1`?
```lisp
;; X_moi = X_cu + 500, Y_moi giu nguyen, Z = 0
(setq pt2 (list (+ (car pt1) 500.0) (cadr pt1) 0.0))
```
Rất trực quan và chuẩn mực toán học!

## 2. Vòng lặp cố định số lần với repeat

Hàm **`repeat`** được sử dụng khi bạn biết trước số lần cần thực hiện (ví dụ: vẽ 10 hình tròn, hoặc vẽ 5 hàng cột).

### Cú pháp:
```lisp
(repeat <so_lan_lap>
  ;; Cac cau lenh can lap lai o day
)
```

### Chương trình mẫu: Vẽ 5 hình tròn đồng tâm cách đều nhau 20mm
```code-live
lang: lisp
run: false
starter: |
  (defun c:DONGTAM ( / tam bk i )
    (setq tam (getpoint "\nChon tam: "))
    (setq bk 20.0)
    (setq i 1)
    
    ;; Lap lai dung 5 lan
    (repeat 5
      (command "_.CIRCLE" tam bk)
      (setq bk (+ bk 20.0)) ;; Tang ban kinh len 20mm moi vong lap
      (setq i (+ i 1))
    )
    
    (princ "\nDa ve xong 5 vong tron dong tam!")
    (princ)
  )
```

## 3. Vòng lặp điều kiện với while

Hàm **`while`** lặp đi lặp lại một khối lệnh **chừng nào điều kiện kiểm tra còn đúng (True)**. Nó rất thích hợp cho các bài toán người dùng muốn bấm chuột vẽ liên tục cho đến khi nào nhấn Enter (hoặc Esc) thì dừng:

### Chương trình mẫu: Đánh số thứ tự tăng dần liên tục
Chương trình hỏi người dùng bấm chuột vào đâu thì ghi số `1`, bấm tiếp ghi số `2`, bấm tiếp ghi số `3`... cho đến khi nhấn phím Enter để kết thúc:

```code-live
lang: lisp
run: false
starter: |
  (defun c:DANHSO ( / stt pt )
    (setq stt 1) ;; Bat dau tu so 1
    
    ;; Vong lap while: Chay chung nao nguoi dung con bam chon diem pt
    (while (setq pt (getpoint (strcat "\nChon vi tri danh so [" (itoa stt) "] (Enter de dung): ")))
      ;; Ghi chu bang lenh TEXT cua CAD
      (command "_.TEXT" "J" "MC" pt 2.5 0 (itoa stt))
      ;; Tang so thu tu len 1 don vi
      (setq stt (+ stt 1))
    )
    
    (princ "\nDa hoan tat danh so thu tu!")
    (princ)
  )
```

*(Giải thích hàm phụ trợ:* `itoa` là hàm đổi từ số nguyên sang chuỗi ký tự text - Integer to ASCII; `strcat` là hàm nối các chuỗi chữ lại với nhau).*

> [!TIP]
> Sử dụng hàm `(polar pt goc khoang_cach)` là cách hiện đại nhất trong Lisp để tính toán toạ độ điểm tiếp theo dựa trên một điểm gốc, góc xoay (đo bằng Radian) và khoảng cách, không cần phải nhẩm tính lượng giác cộng trừ dX, dY!

## Tự kiểm tra

```quiz
id: q-ac-10-05-1
type: single
question: "Khi điểm toạ độ pt được lưu trữ dưới dạng danh sách (X Y Z), hàm nào trong AutoLISP dùng để lấy giá trị toạ độ Y của điểm đó?"
options:
  - text: "cadr"
    correct: true
    why: "cadr trích xuất phần tử thứ hai của danh sách, tương ứng với toạ độ Y."
  - text: "car"
    why: "car trích xuất phần tử đầu tiên, tương ứng với toạ độ X."
  - text: "caddr"
    why: "caddr trích xuất phần tử thứ ba, tương ứng với toạ độ Z."
  - text: "last"
    why: "last lấy phần tử cuối cùng."
explain: "Bộ ba hàm kinh điển: (car pt) lấy X, (cadr pt) lấy Y, (caddr pt) lấy Z."
```

```quiz
id: q-ac-10-05-2
type: single
question: "Hàm nào trong AutoLISP dùng để ghép các con số riêng lẻ X, Y, Z thành một danh sách toạ độ điểm hoàn chỉnh?"
options:
  - text: "list"
    correct: true
    why: "Hàm (list x y z) gom các phần tử thành một danh sách toạ độ điểm hợp lệ."
  - text: "group"
    why: "group không phải hàm AutoLISP tiêu chuẩn."
  - text: "combine"
    why: "combine không phải hàm tạo danh sách."
  - text: "setq"
    why: "setq dùng để gán biến, không phải hàm tạo danh sách."
explain: "Sử dụng hàm list để khởi tạo danh sách toạ độ: ví dụ (list 100.0 200.0 0.0)."
```

```quiz
id: q-ac-10-05-3
type: truefalse
question: "Cấu trúc vòng lặp while (setq pt (getpoint ...)) sẽ tự động dừng lại khi người dùng nhấn phím Enter mà không bấm chọn điểm nào."
answer: true
explain: "Khi người dùng nhấn Enter, hàm getpoint trả về giá trị nil (rỗng). Điều kiện while nhận giá trị nil và tự động kết thúc vòng lặp an toàn."
```

## Lỗi thường gặp

- **Góc trong hàm polar tính bằng độ (Degrees) thay vì Radian:** LISP yêu cầu góc phải đo bằng Radian ($180^{\circ} = \pi \text{ rad}$). Nếu gõ 90 độ thẳng vào hàm polar thì hình vẽ sẽ bị quay sai hướng. Hãy nhớ công thức: $\text{rad} = \text{goc} \times \frac{\pi}{180}$.
- **Vòng lặp vô tận (Infinite Loop) làm treo AutoCAD:** Do trong vòng lặp `while` bạn quên không cập nhật biến đếm hoặc không có điều kiện thoát. Khắc phục: Nhấn tổ hợp phím [Esc] hoặc [Ctrl + Break] để ngắt chương trình khẩn cấp.

## Bài tập thực hành

- [ ] Tạo một file lisp mới chứa đoạn mã hàm đánh số thứ tự tự động `c:DANHSO`.
- [ ] Dùng lệnh `APPLOAD` nạp file vào bản vẽ AutoCAD. <!-- expect: APPLOAD -->
- [ ] Gõ lệnh `DANHSO`, bấm chuột liên tiếp 5 điểm trên màn hình để kiểm tra số thứ tự 1, 2, 3, 4, 5 tự động xuất hiện.
- [ ] Nhấn phím Enter để kết thúc vòng lặp an toàn.

## Nguồn tham khảo

```links
- title: "Các hàm xử lý danh sách List trong AutoLISP từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=List+Handling+AutoLISP"
  kind: official
- title: "Cấu trúc vòng lặp repeat và while từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=repeat+AutoLISP"
  kind: official
```
