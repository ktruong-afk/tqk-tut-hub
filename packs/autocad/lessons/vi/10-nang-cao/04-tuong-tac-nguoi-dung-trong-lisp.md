---
id: ac-10-04
title: Tương tác người dùng với các hàm nhập liệu getxxx trong AutoLISP
category: Nâng cao và Tự động hoá
tags: [autolisp, getpoint, getdist, getstring, getint, initget]
level: advanced
minutes: 25
needs: [ac-10-03]
appVersions: ['2024', '2025']
edition: all
---
# Tương tác người dùng với các hàm nhập liệu getxxx trong AutoLISP

> **Mục tiêu:**
> - Sử dụng họ hàm nhập liệu `getxxx` (`getpoint`, `getdist`, `getint`, `getreal`, `getstring`) để nhận thông tin từ người dùng.
> - Xử lý thông điệp nhắc lệnh thân thiện bằng tiếng Việt và kiểm soát toạ độ điểm tham chiếu.
> - Kết hợp hàm `initget` và `getkword` để tạo các từ khóa tuỳ chọn linh hoạt trên thanh dòng lệnh.

## Giao tiếp giữa chương trình Lisp và người sử dụng

Một chương trình tự động hóa thực thụ không thể chỉ vẽ các con số cố định chết cứng. Nó phải biết "giao tiếp" và hỏi người vẽ:
- "Bạn muốn đặt cột ở toạ độ nào?"
- "Chiều rộng dầm bằng bao nhiêu mm?"
- "Số lượng lỗ khoan là bao nhiêu lỗ?"
- "Bạn chọn kiểu móng nông [Nong] hay móng cọc [Coc]?"

Trong [[AutoLISP]], toàn bộ việc giao tiếp này được thực hiện thông qua **Họ hàm `getxxx`**. Khi gặp hàm `getxxx`, chương trình sẽ tạm dừng lại, hiển thị câu hỏi nhắc nhở dưới thanh dòng lệnh và chờ người dùng bấm chuột hoặc gõ bàn phím rồi mới chạy tiếp.

## Bảng tổng hợp các hàm nhập liệu cốt lõi

| Tên hàm | Dữ liệu nhận vào | Ví dụ sử dụng thực tế |
|---|---|---|
| **`getpoint`** | **Toạ độ điểm 3D** (bấm chuột trên màn hình) | `(setq pt (getpoint "\nChon diem dat:"))` |
| **`getdist`** | **Khoảng cách chiều dài** (số thực đo được) | `(setq d (getdist "\nNhap chieu dai:"))` |
| **`getint`** | **Số nguyên** (Integer: 1, 2, 5, 10...) | `(setq n (getint "\nNhap so luong:"))` |
| **`getreal`** | **Số thực thập phân** (Real: 3.14, 0.05...) | `(setq r (getreal "\nNhap ban kinh:"))` |
| **`getstring`** | **Chuỗi ký tự văn bản** (Text / String) | `(setq ten (getstring T "\nNhap ten truc:"))` |
| **`getkword`** | **Từ khóa lựa chọn** (Keywords) | `(setq opt (getkword "\nChon [Tron/Vuong]:"))` |

*(Chú ý quan trọng: Ký tự `\n` đặt ở đầu câu nhắc lệnh đại diện cho việc xuống dòng mới, giúp câu hỏi hiển thị sạch sẽ trên dòng lệnh mà không bị dính vào lệnh trước).*

## Kỹ thuật điểm tham chiếu trong getpoint và getdist

Hàm `getpoint` và `getdist` có một tính năng cực kỳ thông minh: Cho phép bạn truyền vào một **điểm mốc tham chiếu gốc**:
- Cú pháp: `(getpoint pt "\nChon diem tiep theo:")`
- Khi người dùng rê chuột, một sợi dây cao su ảo (Rubber-band line) sẽ nối căng từ điểm gốc `pt` đến đầu con trỏ chuột! Người vẽ nhìn thấy khoảng cách và hướng di chuyển vô cùng trực quan giống hệt các lệnh gốc của AutoCAD.

## Tạo menu từ khóa lựa chọn với initget và getkword

Bạn muốn người dùng chọn giữa hai phương án: vẽ hình tròn `Tron` hoặc hình vuông `Vuong`?
- Hàm **`initget`** (Initialize Get) dùng để khởi tạo danh sách các từ khóa hợp lệ.
- Hàm **`getkword`** (Get Keyword) bắt buộc người dùng chỉ được gõ một trong các từ khóa đó!

### Chương trình mẫu hoàn chỉnh:

```code-live
lang: lisp
run: false
starter: |
  (defun c:VEHINH ( / pt opt canh bk )
    ;; 1. Khoi tao tu khoa lua chon
    (initget "Tron Vuong")
    (setq opt (getkword "\nBan muon ve hinh gi? [Tron/Vuong] <Tron>: "))
    
    ;; 2. Neu nguoi dung nhan Enter, mac dinh lay "Tron"
    (if (null opt) (setq opt "Tron"))
    
    ;; 3. Hoi diem dat
    (setq pt (getpoint "\nChon tam dat hinh tren ban ve: "))
    
    ;; 4. Re nhanh dieu kien
    (if (= opt "Tron")
      (progn
        (setq bk (getdist pt "\nNhap ban kinh hinh tron: "))
        (command "_.CIRCLE" pt bk)
      )
      (progn
        (setq canh (getdist pt "\nNhap chieu dai canh hinh vuong: "))
        (command "_.RECTANG" pt (list (+ (car pt) canh) (+ (cadr pt) canh)))
      )
    )
    
    (princ "\nDa hoan tat ve hinh!")
    (princ)
  )
```

## Bắt lỗi nhập liệu: Người dùng vô tình nhấn Esc

Trong thực tế, khi chương trình đang hỏi `getpoint`, người dùng có thể đổi ý và nhấn phím [Esc] để hủy bỏ. Nếu không xử lý, chương trình có thể để lại các biến hệ thống rác (như tắt mất bắt điểm Osnap).

Hàm **`vl-catch-all-apply`** hoặc gán hàm bẫy lỗi **`*error*`** là kỹ thuật chuyên nghiệp của lập trình viên Lisp:
- Định nghĩa hàm `(defun *error* (msg) ...)` ở đầu chương trình.
- Khi người dùng nhấn [Esc], hàm bẫy lỗi sẽ tự động được kích hoạt để khôi phục lại toàn bộ cài đặt gốc của AutoCAD sạch sẽ như chưa từng có chuyện gì xảy ra!

> [!TIP]
> Trong hàm `(getstring T "\nNhap ghi chu: ")`, tham số cờ `T` (True) cho phép chuỗi nhập vào chứa khoảng trắng (dấu cách). Nếu không có `T`, khi người dùng bấm dấu cách thì chuỗi nhập sẽ bị ngắt lệnh ngay lập tức!

## Tự kiểm tra

```quiz
id: q-ac-10-04-1
type: single
question: "Hàm nào trong AutoLISP dùng để nhận dữ liệu là một con số nguyên (ví dụ số lượng cọc = 12) từ bàn phím?"
options:
  - text: "getint"
    correct: true
    why: "getint (Get Integer) chuyên dùng để nhận các số nguyên không có phần thập phân."
  - text: "getreal"
    why: "getreal dùng để nhận số thực có phần thập phân."
  - text: "getpoint"
    why: "getpoint dùng để nhận toạ độ điểm."
  - text: "getstring"
    why: "getstring dùng để nhận chuỗi chữ văn bản."
explain: "Sử dụng getint khi bạn cần người dùng nhập số lượng đối tượng cần nhân bản hoặc số thứ tự nguyên."
```

```quiz
id: q-ac-10-04-2
type: single
question: "Ký tự điều khiển '\\n' đặt ở đầu câu thông điệp nhắc lệnh trong các hàm getxxx có tác dụng gì?"
options:
  - text: "Xuống một dòng mới trên thanh Command Line để câu nhắc hiển thị rõ ràng"
    correct: true
    why: "\\n đại diện cho ký tự New Line trong lập trình."
  - text: "Tự động dịch câu hỏi sang tiếng Nhật"
    correct: false
    why: "\\n không liên quan đến dịch thuật."
  - text: "Tắt toàn bộ âm thanh của máy tính"
    correct: false
    why: "Không liên quan đến phần cứng âm thanh."
  - text: "Làm biến mất chữ số kích thước"
    correct: false
    why: "Không can thiệp vào kích thước bản vẽ."
explain: "Luôn đặt \\n ở đầu chuỗi thông điệp nhắc lệnh để dòng chữ xuất hiện ở dòng lệnh mới tinh tươm."
```

```quiz
id: q-ac-10-04-3
type: truefalse
question: "Hàm initget kết hợp với getkword cho phép tạo ra các từ khóa tuỳ chọn [A/B/C] bấm chọn được trên thanh dòng lệnh của AutoCAD."
answer: true
explain: "Cặp hàm initget và getkword là chuẩn mực để tạo các tùy chọn nhánh lệnh thân thiện và chuyên nghiệp."
```

## Lỗi thường gặp

- **Nhập chữ có dấu cách bị ngắt lệnh giữa chừng:** Khi dùng `getstring` nhập tên phòng "Phòng Khách" thì chỉ nhận được chữ "Phòng". Khắc phục: Thêm cờ `T` vào trước chuỗi nhắc: `(getstring T "\nNhap ten phong: ")`.
- **Nhập khoảng cách bằng getdist nhưng quên điểm mốc:** Khiến người vẽ không nhìn thấy sợi dây cao su ảo kéo dài để ngắm phương hướng.

## Bài tập thực hành

- [ ] Mở phần mềm soạn thảo văn bản Notepad, viết một hàm lisp đơn giản dùng `getpoint` và `getdist`.
- [ ] Lưu file với tên `test-input.lsp`.
- [ ] Gõ lệnh `APPLOAD` nạp file vừa lưu vào AutoCAD. <!-- expect: APPLOAD -->
- [ ] Chạy thử lệnh và quan sát dòng nhắc lệnh hiển thị trên màn hình.
- [ ] Nhấn phím `Esc` để hủy lệnh và kiểm tra việc ngắt lệnh an toàn.

## Nguồn tham khảo

```links
- title: "Các hàm nhập liệu người dùng getxxx từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=User+Input+Functions+AutoLISP"
  kind: official
- title: "Hàm initget khởi tạo từ khóa từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=initget"
  kind: official
```
