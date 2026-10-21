---
id: ac-05-06
title: Ghi chú dẫn hướng chuyên nghiệp với Multileader (MLEADER)
category: Ghi kích thước
tags: [mleader, mleaderstyle, chu-thich, leader]
level: intermediate
minutes: 20
needs: [ac-05-04]
appVersions: ['2024', '2025']
edition: all
---
# Ghi chú dẫn hướng chuyên nghiệp với Multileader (MLEADER)

> **Mục tiêu:**
> - Sử dụng lệnh `MLEADER` để tạo đường dẫn ghi chú chi tiết kỹ thuật có mũi tên và đoạn ngang gác chữ.
> - Thiết lập kiểu ghi chú dẫn hướng bằng `MLEADERSTYLE` với nội dung văn bản (MText) hoặc khối ký hiệu (Block).
> - Thao tác thêm nhánh dẫn (`Add Leader`) hoặc gom cụm ghi chú (`Align / Collect Leaders`).

## Khái niệm đường chú thích dẫn hướng Multileader

Trên bản vẽ cơ khí hoặc xây dựng, có rất nhiều vị trí cần chỉ rõ tên vật liệu, mối hàn, cấu tạo lớp sàn hoặc ký hiệu cấu kiện. Nếu bạn vẽ mũi tên bằng `LINE` rồi viết chữ rời rạc bằng `MTEXT`, khi di dời chi tiết, chữ và mũi tên sẽ bị tách rời nhau rất mất công chỉnh sửa.

AutoCAD cung cấp đối tượng chuyên nghiệp **Multileader ([[MLeader]])** (lệnh tắt `MLD`). Đây là một khối thông minh tích hợp trọn gói 3 phần:
1. **Đầu mũi tên và đường dẫn (Leader line & Arrowhead):** Chỉ chính xác vào điểm cần ghi chú.
2. **Đoạn ngang gác chữ (Landing line):** Giữ cho chữ số luôn nằm cân đối, thẳng thớm.
3. **Nội dung ghi chú (Content):** Có thể là một đoạn văn bản nhiều dòng (`MText`) hoặc một khối ký hiệu đánh số thứ tự (`Block`).

![Cấu tạo của một Multileader chuẩn](media/ac-05-06-mleader-parts.svg)

```hotspots
image: media/ac-05-06-mleader-parts.svg
alt: Các thành phần cấu tạo của đường ghi chú dẫn hướng Multileader
layout: central
points:
  - id: spot-1
    x: 20
    y: 70
    title: Mũi tên chỉ điểm (Arrowhead)
    text: Chỉ vào bề mặt chi tiết hoặc cấu kiện cần chú thích.
  - id: spot-2
    x: 45
    y: 52
    title: Đường dẫn chéo (Leader line)
    text: Nối từ mũi tên đến đoạn gác chữ, có thể gãy góc linh hoạt.
  - id: spot-3
    x: 62
    y: 45
    title: Đoạn ngang đỡ chữ (Landing line)
    text: Đoạn thẳng nằm ngang cố định giúp dòng chữ nằm ngay ngắn.
  - id: spot-4
    x: 80
    y: 35
    title: Nội dung chú thích (Content)
    text: Văn bản MText hoặc Block ký hiệu được liên kết vĩnh viễn với đường dẫn.
```

## Cách dùng từng bước

### 1. Tạo đường chú thích với lệnh MLEADER
1. Gõ `MLD` hoặc `MLEADER` rồi nhấn [Enter].
2. Bấm chuột chọn điểm cần chú thích trên chi tiết (vị trí đầu mũi tên).
3. Di chuột ra ngoài khoảng trống bản vẽ và bấm điểm thứ hai để định hình hướng đường dẫn chéo.
4. Ngay lập tức, đoạn ngang `Landing` xuất hiện và khung nhập văn bản mở ra.
5. Gõ nội dung ghi chú (ví dụ: `Thép hình I200 mạ kẽm nhúng nóng` hoặc `Vát mép C2x45°`).
6. Bấm chuột ra ngoài hoặc bấm nút **Close Text Editor** để hoàn tất.

### 2. Thiết lập kiểu dáng bằng MLEADERSTYLE
1. Gõ `MLS` hoặc `MLEADERSTYLE` rồi nhấn [Enter].
2. Bấm nút **New**, đặt tên kiểu (ví dụ: `CHU-THICH-CO-KHI`).
3. Trong hộp thoại có 3 thẻ chính:
   - **Leader Format:** Chọn kiểu nét (Straight hoặc Spline cong), màu sắc nét vẽ, kiểu mũi tên và kích thước mũi tên.
   - **Leader Structure:** Quy định số lượng điểm gãy góc (mặc định 2 điểm), chiều dài đoạn ngang `Landing distance` (thường đặt `5` đến `8` mm).
   - **Content:** Chọn kiểu nội dung là `Mtext` (văn bản) hoặc `Block` (ví dụ hình tròn đánh số chi tiết 1, 2, 3).
4. Bấm **OK**, chọn **Set Current** và **Close**.

## Tuỳ chọn nâng cao và mẹo hay

- **Thêm nhiều mũi tên chỉ cùng một nội dung (`Add Leader`):**
  Khi nhiều vị trí có cùng quy cách gia công, bạn không cần tạo nhiều ghi chú trùng lặp. Gõ lệnh `AIMLEADEREDITADD` (hoặc bấm nút **Add Leader** trên Ribbon), chọn ghi chú đã có, rồi bấm vào các vị trí khác để mọc thêm mũi tên dẫn về cùng 1 dòng chữ.
- **Căn thẳng hàng các ghi chú (`MLEADERALIGN`):**
  Quét chọn một loạt các ghi chú nằm lộn xộn, gõ lệnh `MLEADERALIGN` để căn toàn bộ các dòng chữ thẳng hàng tắp theo phương đứng hoặc ngang.

> [!TIP]
> Nhấp đúp chuột vào mũi tên của Multileader để mở trực tiếp bảng sửa chữ hoặc kéo các điểm kẹp (Grips) để di chuyển dòng chữ; mũi tên sẽ tự động co giãn theo mà không bị đứt gãy.

## Tự kiểm tra

```quiz
id: q-ac-05-06-1
type: single
question: "Lệnh tắt ngắn nhất trong AutoCAD để tạo đường ghi chú dẫn hướng Multileader là gì?"
options:
  - text: "MLD"
    correct: true
    why: "MLD là alias tiêu chuẩn của lệnh MLEADER."
  - text: "ML"
    correct: false
    why: "ML là lệnh MLINE (vẽ nhiều đường thẳng song song)."
  - text: "LE"
    correct: false
    why: "LE là QLEADER (công cụ ghi chú đời cũ, ít linh hoạt hơn MLEADER)."
  - text: "MLS"
    correct: false
    why: "MLS là MLEADERSTYLE (quản lý kiểu ghi chú)."
explain: "Sử dụng MLD để gọi lệnh MLEADER tạo ghi chú dẫn hướng hiện đại và tiện lợi nhất."
```

```quiz
id: q-ac-05-06-2
type: single
question: "Ưu điểm lớn nhất của Multileader so với việc vẽ đường thẳng (LINE) rồi viết chữ rời (MTEXT) là gì?"
options:
  - text: "Mũi tên, đường dẫn và nội dung chữ liên kết thành một đối tượng duy nhất, tự co giãn khi di chuyển"
    correct: true
    why: "Di chuyển chữ thì mũi tên tự động bám theo mà không bị rời rạc bản vẽ."
  - text: "Tự động dịch nội dung ghi chú sang tiếng Nhật"
    correct: false
    why: "AutoCAD không có tính năng tự động dịch ngôn ngữ cho Mleader."
  - text: "Không bao giờ tốn bộ nhớ RAM của máy tính"
    correct: false
    why: "Mọi đối tượng đồ hoạ đều tiêu tốn bộ nhớ của tệp DWG."
  - text: "Chỉ in được ra máy in màu"
    correct: false
    why: "In ấn phụ thuộc vào thiết bị in và nét in CTB."
explain: "Tính liên kết nguyên khối (Leader line + Landing + Text/Block) là lý do MLEADER thay thế hoàn toàn các phương pháp thủ công trước đây."
```

```quiz
id: q-ac-05-06-3
type: truefalse
question: "Trong MLEADERSTYLE, bạn có thể chọn Content Type là Block để tạo các ký hiệu bóng tròn đánh số chi tiết cơ khí (Detail Balloon)."
answer: false
explain: "MLEADER hỗ trợ trực tiếp khối Block có thuộc tính để đánh số thứ tự chi tiết từ 1 đến N rất chuyên nghiệp."
```

## Lỗi thường gặp

- **Chữ ghi chú quá bé hoặc mũi tên biến mất:** Do tỉ lệ bản vẽ chưa khớp với thông số trong `MLEADERSTYLE`. Khắc phục: Vào thẻ Leader Format tăng kích thước `Arrowhead size` và thẻ Content tăng `Text height`, hoặc tích chọn chế độ `Annotative`.
- **Dòng chữ bị đè lên đường gác chữ (Landing):** Trong thẻ Content, mục `Text attachment` chưa chọn đúng kiểu (nên chọn `Middle of text` hoặc `Bottom of bottom line`).

## Bài tập thực hành

- [ ] Gõ `MLEADERSTYLE` (hoặc `MLS`), tạo một kiểu ghi chú mới có tên `GHI-CHU-MAU`. <!-- expect: MLEADERSTYLE -->
- [ ] Trong thẻ `Leader Structure`, đặt `Landing distance` là 8. Bấm OK và Set Current. <!-- expect: MLEADERSTYLE -->
- [ ] Vẽ một hình chữ nhật kích thước 100 x 50 mm bằng `RECTANG`. <!-- expect: RECTANG -->
- [ ] Dùng lệnh `MLEADER` (hoặc `MLD`), bấm vào góc hình chữ nhật và kéo ra ngoài ghi chú dòng chữ: "Tấm thép CT3 dày 10mm". <!-- expect: MLEADER -->

## Nguồn tham khảo

```links
- title: "Tài liệu Multileaders chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=MLEADER"
  kind: official
- title: "Quản lý Multileader Styles từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=MLEADERSTYLE"
  kind: official
```
