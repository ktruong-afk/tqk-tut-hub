---
id: ac-10-03
title: Nhập môn lập trình AutoLISP và giải phẫu hàm cơ bản
category: Nâng cao và Tự động hoá
tags: [autolisp, lisp, appload, defun, setq, tu-dong-hoa]
level: advanced
minutes: 25
needs: [ac-08-06]
appVersions: ['2024', '2025']
edition: all
---
# Nhập môn lập trình AutoLISP và giải phẫu hàm cơ bản

> **Mục tiêu:**
> - Hiểu nguyên lý cú pháp tiền tố và cấu trúc giải phẫu của một hàm [[AutoLISP]] tiêu chuẩn (`defun c:TENTEN`).
> - Khai báo và gán biến số với hàm `setq`, bảo vệ bộ nhớ với danh sách biến cục bộ `( / bien1 bien2 )`.
> - Nạp tệp Lisp vào bản vẽ với lệnh `APPLOAD` và gọi lệnh thực thi trực tiếp trên thanh dòng lệnh.

## AutoLISP: Siêu năng lực tự động hoá của người dùng AutoCAD

Trong cộng đồng kỹ sư thiết kế tại Việt Nam, từ lâu đã lưu truyền câu nói: *"Biết vẽ AutoCAD chỉ là thợ vẽ, biết dùng AutoLISP mới là cao thủ"*.

Hầu hết các công ty thiết kế lớn đều trang bị cho nhân viên những bộ "Lisp tủ":
- Lisp vẽ tim trục và vẽ cột tự động chỉ sau 1 cú click.
- Lisp cộng tổng chiều dài các đoạn thép (tổng chiều dài pline) trong 1 giây.
- Lisp đánh số thứ tự phòng, số thứ tự cọc móng tự động tăng dần từ 1 đến 1000.

**[[AutoLISP]]** là một phương ngữ của ngôn ngữ lập trình LISP (List Processing) được Autodesk tích hợp sâu vào trái tim của AutoCAD. Nó cho phép bạn tự sáng chế ra những lệnh mới toanh theo ý thích cá nhân mà phiên bản AutoCAD gốc không hề có!

![Giải phẫu cấu trúc một chương trình AutoLISP chuẩn](media/ac-10-03-autolisp-structure.svg)

```hotspots
image: media/ac-10-03-autolisp-structure.svg
alt: Cấu trúc giải phẫu hàm AutoLISP chuẩn trong AutoCAD
layout: central
points:
  - id: spot-1
    x: 23
    y: 25
    title: 1. Khai báo hàm (defun c:TENTEN)
    text: "Tiền tố c: biến hàm lisp thành lệnh gõ phím trực tiếp trên dòng lệnh Command Line."
  - id: spot-2
    x: 75
    y: 25
    title: 2. Biến cục bộ ( / pt r )
    text: "Khai báo sau dấu gạch chéo để giải phóng bộ nhớ RAM sau khi chạy xong."
  - id: spot-3
    x: 23
    y: 55
    title: 3. Gán biến (setq)
    text: "Lưu trữ giá trị toạ độ, số đo hoặc chuỗi ký tự vào tên biến đại diện."
  - id: spot-4
    x: 75
    y: 75
    title: 4. Gọi lệnh CAD (command)
    text: "Thực thi các lệnh vẽ quen thuộc của CAD (như CIRCLE, LINE) bằng mã code."
```

## Cú pháp cơ bản của LISP: Cặp dấu ngoặc đơn và toán tử tiền tố

Khác với các ngôn ngữ lập trình thông thường viết $1 + 2$, trong LISP mọi câu lệnh đều được bao bọc trong **cặp dấu ngoặc đơn `( ... )`** và toán tử luôn nằm ở vị trí đầu tiên (**Toán tử tiền tố - Prefix notation**):
- Phép cộng $1 + 2$: Viết là `(+ 1 2)` $\to$ Kết quả trả về `3`.
- Phép nhân $5 \times 10$: Viết là `(* 5 10)` $\to$ Kết quả trả về `50`.
- Biểu thức phức tạp $(10 + 20) \times 2$: Viết là `(* (+ 10 20) 2)` $\to$ Kết quả trả về `60`.

*(Quy tắc vàng: Mở bao nhiêu dấu ngoặc đơn thì bắt buộc phải đóng bấy nhiêu dấu ngoặc đơn!)*

## 4 thành phần giải phẫu của một hàm Lisp hoàn chỉnh

Hãy cùng quan sát đoạn mã Lisp tự động vẽ một hình tròn bán kính 50mm tại điểm người dùng bấm chuột:

```code-live
lang: lisp
run: false
starter: |
  (defun c:VETRON ( / pt )
    ;; 1. Hỏi người dùng bấm chọn tâm hình tròn
    (setq pt (getpoint "\nChon tam hinh tron tren man hinh: "))
    
    ;; 2. Gọi lệnh CIRCLE của AutoCAD để vẽ hình tròn bán kính 50
    (command "_.CIRCLE" pt 50)
    
    ;; 3. Thông báo hoàn tất ra dòng lệnh
    (princ "\nDa ve xong hinh tron ban kinh 50mm!")
    
    ;; 4. Kết thúc sạch sẽ, không trả về giá trị thừa
    (princ)
  )
```

### Giải mã từng dòng code:
1. **`(defun c:VETRON ( / pt ) ... )`:**
   - `defun`: Lệnh định nghĩa hàm (Define Function).
   - `c:VETRON`: Tiền tố `c:` rất quan trọng! Nó báo cho AutoCAD biết đây là một **lệnh dòng lệnh**. Bạn chỉ cần gõ chữ `VETRON` rồi nhấn Enter là lệnh sẽ chạy. Nếu không có `c:`, bạn sẽ phải gõ `(VETRON)` trong dấu ngoặc kép rất bất tiện.
   - `( / pt )`: Khai báo biến cục bộ (Local Variable). Các biến đặt sau dấu gạch chéo `/` sẽ tự động bị xóa khỏi bộ nhớ RAM khi lệnh chạy xong, tránh xung đột với các chương trình khác.
2. **`(setq pt (getpoint ...))`:**
   - `setq` (Set Quote): Gán giá trị vào biến.
   - `getpoint`: Tạm dừng chương trình để người dùng bấm chuột chọn toạ độ trên màn hình. Giá trị toạ độ đó được gán vào biến `pt`.
3. **`(command "_.CIRCLE" pt 50)`:**
   - Hàm `command` gửi lệnh trực tiếp vào thanh dòng lệnh của AutoCAD.
   - Tiền tố `_.`: Dấu gạch dưới `_` để chạy được trên mọi ngôn ngữ AutoCAD (Anh, Pháp, Đức), dấu chấm `.` để chạy đúng lệnh gốc kể cả khi lệnh đã bị người dùng đổi alias.
4. **`(princ)`:**
   - In chuỗi thông báo ra dòng lệnh và giúp hàm kết thúc sạch sẽ, không hiển thị chữ `nil` vô nghĩa ở cuối lệnh.

## Cách dùng từng bước: Nạp và chạy Lisp với APPLOAD

1. Mở phần mềm Notepad của Windows, dán đoạn code trên vào.
2. Bấm **Save As**, chọn *Save as type: All Files*, đặt tên file là **`ve-hinh-tron.lsp`** (phần mở rộng bắt buộc là `.lsp`).
3. Mở AutoCAD lên: Gõ lệnh **`APPLOAD`** rồi nhấn [Enter] (hoặc vào menu *Manage* > chọn **Load Application**).
4. Hộp thoại **Load/Unload Applications** mở ra:
   - Duyệt tìm và chọn file `ve-hinh-tron.lsp` vừa lưu.
   - Bấm nút **Load**.
   - Nhìn xuống góc dưới hộp thoại thấy dòng chữ: *"ve-hinh-tron.lsp successfully loaded."*
5. Bấm **Close** đóng hộp thoại lại.
6. Giờ đây trên thanh dòng lệnh của AutoCAD, bạn gõ chữ **`VETRON`** rồi nhấn [Enter].
7. Bấm chuột vào bất kỳ điểm nào trên màn hình: Một hình tròn bán kính 50mm xuất hiện ngay lập tức tại vị trí bạn vừa bấm!

> [!TIP]
> Muốn tệp Lisp tự động nạp mỗi khi mở AutoCAD mà không phải bấm APPLOAD thủ công: Trong hộp thoại `APPLOAD`, bấm vào biểu tượng chiếc cặp da **Startup Suite (Contents...)**, bấm **Add** và chọn tệp Lisp của bạn. Tệp sẽ được nạp vĩnh viễn mỗi khi khởi động!

## Tự kiểm tra

```quiz
id: q-ac-10-03-1
type: single
question: "Tiền tố 'c:' đặt trước tên hàm trong khai báo (defun c:TENTEN ...) của AutoLISP mang ý nghĩa gì?"
options:
  - text: "Biến hàm Lisp thành một lệnh người dùng có thể gõ trực tiếp trên thanh Command Line mà không cần dấu ngoặc đơn"
    correct: true
    why: "Tiền tố c: (Command) tích hợp hàm vào hệ thống lệnh chính thức của AutoCAD."
  - text: "Báo cho phần mềm biết đây là hàm viết bằng ngôn ngữ C++"
    correct: false
    why: "AutoLISP là phương ngữ của ngôn ngữ LISP, không liên quan đến C++."
  - text: "Bắt buộc người vẽ phải dùng máy in màu"
    correct: false
    why: "Không liên quan đến thiết bị in ấn."
  - text: "Làm cho chương trình chạy chậm đi 10 lần"
    correct: false
    why: "Tiền tố c: không ảnh hưởng đến tốc độ thực thi của hàm."
explain: "Khai báo c:TEN_LENH giúp bạn có thể gọi lệnh Lisp giống hệt các lệnh gốc LINE, CIRCLE của AutoCAD."
```

```quiz
id: q-ac-10-03-2
type: single
question: "Lệnh nào trong AutoCAD dùng để mở hộp thoại nạp các tệp mã nguồn AutoLISP (.lsp) và ứng dụng mở rộng vào bản vẽ?"
options:
  - text: "APPLOAD"
    correct: true
    why: "APPLOAD là chữ viết tắt của Application Load."
  - text: "MENULOAD"
    why: "MENULOAD dùng để nạp tệp menu giao diện."
  - text: "SCRIPT"
    why: "SCRIPT dùng để chạy tệp kịch bản .scr."
  - text: "INSERT"
    why: "INSERT dùng để chèn khối Block."
explain: "Sử dụng lệnh APPLOAD để nạp tệp Lisp chạy thử nghiệm hoặc thêm vào Startup Suite để dùng vĩnh viễn."
```

```quiz
id: q-ac-10-03-3
type: truefalse
question: "Các biến số được liệt kê sau dấu gạch chéo '(/ bien1 bien2)' trong khai báo hàm AutoLISP là các biến cục bộ sẽ tự động giải phóng khỏi bộ nhớ RAM khi lệnh chạy xong."
answer: true
explain: "Khai báo biến cục bộ là nguyên tắc vàng trong lập trình AutoLISP để tránh rò rỉ bộ nhớ và xung đột biến số giữa các chương trình khác nhau."
```

## Lỗi thường gặp

- **Báo lỗi 'malformed list on input':** Lỗi kinh điển số 1 của người mới học Lisp: Bạn bị thiếu một dấu đóng ngoặc đơn `)` ở đâu đó trong file code. Khắc phục: Đếm lại xem số lượng mở ngoặc `(` và đóng ngoặc `)` đã bằng nhau chưa.
- **Báo lỗi 'no function definition':** Do gõ sai tên hàm cơ bản của AutoCAD (ví dụ gõ nhầm `getpoints` thay vì `getpoint`).

## Bài tập thực hành

- [ ] Gõ lệnh `APPLOAD` để mở hộp thoại quản lý nạp ứng dụng trong AutoCAD. <!-- expect: APPLOAD -->
- [ ] Quan sát biểu tượng chiếc cặp da `Startup Suite` phục vụ nạp Lisp vĩnh viễn.
- [ ] Bấm nút đóng hoặc Cancel để thoát khỏi hộp thoại APPLOAD.
- [ ] Gõ thử biểu thức toán học trực tiếp trên dòng lệnh AutoCAD: `(+ 150 250)` và nhấn Enter để xem kết quả tính toán tự động 400.

## Nguồn tham khảo

```links
- title: "Hướng dẫn lập trình AutoLISP chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=AutoLISP"
  kind: official
- title: "Quản lý nạp ứng dụng với APPLOAD từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=APPLOAD"
  kind: official
```
