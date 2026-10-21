---
id: ac-08-04
title: Cứu hộ và tối ưu hoá tệp bản vẽ với RECOVER, AUDIT và PURGE
category: Nâng cao năng suất
tags: [recover, audit, purge, sua-loi, toi-uu, cuu-file]
level: intermediate
minutes: 25
needs: [ac-08-01]
appVersions: ['2024', '2025']
edition: all
---
# Cứu hộ và tối ưu hoá tệp bản vẽ với RECOVER, AUDIT và PURGE

> **Mục tiêu:**
> - Sử dụng lệnh `RECOVER` để cứu các tệp bản vẽ DWG bị lỗi hỏng nặng không thể mở bằng cách thông thường.
> - Quét và sửa chữa lỗi cấu trúc cơ sở dữ liệu ngầm với lệnh `AUDIT`.
> - Dọn dẹp rác nâng cao (Regapps, DGN linetypes) và tối ưu dung lượng tệp với lệnh `PURGE`.

## Nỗi kinh hoàng "Fatal Error" và tệp bản vẽ bị hỏng

Bất kỳ ai làm việc với AutoCAD lâu năm đều từng trải qua cảm giác thót tim:
- Đang vẽ thì phần mềm đột ngột tắt phụt với hộp thoại thông báo màu đỏ: *"FATAL ERROR: Unhandled Access Violation..."*.
- Mở lại file DWG thì phần mềm từ chối mở và báo lỗi: *"Drawing file is not valid"*.
- Hoặc một file chỉ có vài đường nét đơn giản nhưng dung lượng phình to bất thường lên 50MB, mỗi lần bấm `Ctrl + C` hoặc `Ctrl + V` máy bị đơ cứng mất 30 giây!

Những sự cố này thường do tệp bản vẽ bị mất điện đột ngột khi đang lưu, hoặc do copy các khối block từ phần mềm MicroStation (DGN) mang theo hàng chục ngàn kiểu nét vẽ rác ngầm.

Bộ ba cứu hộ **`RECOVER`**, **`AUDIT`** và **`PURGE` nâng cao** là "bác sĩ cấp cứu" chuyên nghiệp giúp bạn phục hồi nguyên vẹn dữ liệu bản vẽ mà không phải vẽ lại từ đầu!

## Bộ ba công cụ cứu hộ và tối ưu từng bước

### 1. Cứu tệp không mở được với lệnh RECOVER
Khi bạn nhấp đúp vào tệp DWG ngoài màn hình desktop nhưng AutoCAD báo lỗi không thể mở:
1. Mở phần mềm AutoCAD lên với một bản vẽ trống.
2. Bấm vào chữ **A** lớn góc trên bên trái > chọn **Drawing Utilities** > chọn **Recover** (hoặc gõ lệnh `RECOVER` rồi nhấn [Enter]).
3. Duyệt tìm đến tệp DWG đang bị hỏng, bấm **Open**.
4. AutoCAD sẽ chạy thuật toán quét sâu vào từng sector cơ sở dữ liệu nhị phân của tệp, phục hồi lại các đối tượng đồ họa còn nguyên vẹn và tự động vá các con trỏ bị gãy.
5. Khi hoàn tất, một bảng thống kê sẽ hiện ra thông báo số lượng lỗi đã được khắc phục. Bản vẽ sẽ được mở ra an toàn!

### 2. Sửa lỗi định kỳ cho tệp đang vẽ với AUDIT
Khi tệp bản vẽ vẫn mở được nhưng có dấu hiệu giật lag hoặc hay bị văng đột ngột:
1. Gõ `AUDIT` rồi nhấn [Enter].
2. Dòng lệnh hỏi: `Fix any errors detected? [Yes/No] <N>:`.
3. Gõ `Y` (Yes) rồi nhấn [Enter].
4. AutoCAD quét nhanh cây dữ liệu và sửa chữa toàn bộ các lỗi tiềm ẩn.
5. Khuyên dùng: Hãy chạy lệnh `AUDIT` mỗi tuần một lần cho các tệp dự án quan trọng!

### 3. Dọn dẹp rác nâng cao và diệt "rác tàng hình" (Regapps)
Nhiều bản vẽ sau khi dùng lệnh `PURGE` thông thường mà file vẫn nặng hàng chục MB. Đó là do các dữ liệu ứng dụng đã đăng ký (**Regapps** - Registered Applications) bám chặt bên trong:
1. Gõ `-PURGE` (Lưu ý: Có dấu gạch ngang phía trước để vào chế độ dòng lệnh).
2. Dòng lệnh hỏi đối tượng cần dọn: Gõ `R` (Regapps) rồi nhấn [Enter].
3. Dòng lệnh hỏi tên cần quét: Nhấn [Enter] (chọn tất cả `*`).
4. Dòng lệnh hỏi có muốn xác nhận từng mục: Gõ `N` (No) rồi nhấn [Enter].
5. Bạn sẽ kinh ngạc khi thấy màn hình cuộn xóa hàng chục ngàn dòng regapps rác!
6. Dung lượng tệp DWG có thể lập tức giảm từ 40MB xuống chỉ còn 2MB!

## Cứu bản vẽ chưa kịp lưu khi bị sập nguồn (Drawing Recovery Manager)

Nếu máy tính bị sập nguồn điện đột ngột trong khi bạn đang vẽ hăng say:
1. Khởi động lại AutoCAD.
2. Một bảng điều khiển **Drawing Recovery Manager** sẽ tự động mở ra bên trái màn hình.
3. Bảng này liệt kê tệp bạn vừa vẽ cùng các bản sao lưu tự động:
   - File gốc `.dwg`.
   - File sao lưu dự phòng `.bak` (Backup file).
   - File tự động lưu `.sv$` (AutoSave file do biến `SAVETIME` lưu định kỳ mỗi 10 phút).
4. Bạn chỉ việc nhấp đúp vào file có mốc thời gian gần nhất để mở lại toàn bộ sản phẩm của mình!

> [!TIP]
> Vào lệnh `OPTIONS` > thẻ *Open and Save* > kiểm tra ô **Minutes between saves** đang đặt là `10` hoặc `5` phút để đảm bảo nếu có sự cố xảy ra, bạn chỉ mất tối đa 5 phút công sức vẽ!

> [!TIP]
> Lệnh `OVERKILL` (đã học ở chặng 3) kết hợp với `AUDIT` và `PURGE` là bộ công cụ tối thượng để tối ưu hóa triệt để độ mượt mà của bản vẽ.

## Tự kiểm tra

```quiz
id: q-ac-08-04-1
type: single
question: "Khi một tệp bản vẽ DWG bị lỗi hỏng nặng không thể mở bằng cách thông thường, lệnh nào giúp AutoCAD quét sâu và phục hồi lại tệp tin?"
options:
  - text: "RECOVER"
    correct: true
    why: "RECOVER quét phân tích và sửa chữa tệp tin DWG bị hỏng trước khi nạp vào bộ nhớ."
  - text: "OPEN"
    why: "OPEN thông thường sẽ báo lỗi và từ chối mở file bị hỏng."
  - text: "NEW"
    why: "NEW dùng để tạo bản vẽ mới trống."
  - text: "SAVEAS"
    why: "SAVEAS dùng để lưu bản vẽ đang mở thành tên khác."
explain: "Lệnh RECOVER là cứu tinh chuyên dụng để mở các tệp bản vẽ bị crash hoặc lỗi cấu trúc dữ liệu."
```

```quiz
id: q-ac-08-04-2
type: single
question: "Để dọn dẹp hàng ngàn 'rác tàng hình' Regapps khiến tệp bản vẽ bị phình to bất thường và giật lag khi Copy-Paste, bạn dùng cú pháp lệnh nào?"
options:
  - text: "Lệnh -PURGE rồi chọn tùy chọn Regapps (gõ R)"
    correct: true
    why: "Lệnh -PURGE với tùy chọn Regapps thanh lọc toàn bộ các định danh ứng dụng bên ngoài bám vào file."
  - text: "Lệnh ERASE All"
    why: "ERASE All sẽ xóa sạch toàn bộ hình vẽ của công trình."
  - text: "Lệnh EXPLODE"
    why: "EXPLODE phá vỡ khối, càng làm tăng rác hình học."
  - text: "Lệnh ZOOM All"
    why: "ZOOM All chỉ là thao tác quan sát màn hình."
explain: "Tùy chọn Regapps trong lệnh -PURGE giúp giải phóng bộ nhớ và giảm dung lượng file bị phình to bất thường."
```

```quiz
id: q-ac-08-04-3
type: truefalse
question: "Khi AutoCAD bị sập phần mềm đột ngột, bảng Drawing Recovery Manager sẽ hỗ trợ phục hồi bản vẽ từ các tệp sao lưu tự động .bak và .sv$."
answer: true
explain: "Drawing Recovery Manager tự động liệt kê các phiên bản backup và autosave gần nhất để người dùng lấy lại dữ liệu an toàn."
```

## Lỗi thường gặp

- **Chạy PURGE thông thường nhưng file vẫn nặng nề:** Do chưa dọn `Regapps` và chưa dọn các kiểu nét vẽ `DGN linetypes` bám ngầm. Khắc phục: Dùng `-PURGE` chọn `R`, hoặc dùng công cụ `DGN Clean` của Autodesk.
- **Không tìm thấy file tự lưu .sv$:** Do thư mục lưu tạm nằm sâu trong thư mục `AppData\Local\Temp`. Dùng bảng `Drawing Recovery Manager` là cách nhanh nhất để tìm ra các file này.

## Bài tập thực hành

- [ ] Gõ lệnh `AUDIT`, chọn `Y` (Yes) để kiểm tra và sửa toàn bộ các lỗi cơ sở dữ liệu của bản vẽ hiện hành. <!-- expect: AUDIT -->
- [ ] Gõ lệnh `PURGE` để mở hộp thoại dọn dẹp các đối tượng không dùng tới. <!-- expect: PURGE -->
- [ ] Bấm nút **Purge All** nhiều lần để thanh lọc sạch sẽ các đối tượng thừa. <!-- expect: PURGE -->
- [ ] Thử gõ lệnh `RECOVER` để mở hộp thoại duyệt tệp cứu hộ bản vẽ. <!-- expect: RECOVER -->

## Nguồn tham khảo

```links
- title: "Phục hồi tệp bản vẽ bị lỗi với lệnh RECOVER từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=RECOVER"
  kind: official
- title: "Khắc phục sự cố tệp DWG với AUDIT từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=AUDIT"
  kind: official
```
