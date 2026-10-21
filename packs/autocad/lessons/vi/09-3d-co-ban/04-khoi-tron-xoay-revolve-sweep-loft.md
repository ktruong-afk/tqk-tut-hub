---
id: ac-09-04
title: Tạo hình nâng cao với REVOLVE, SWEEP và LOFT
category: Mô hình hoá 3D
tags: [revolve, sweep, loft, tron-xoay, duong-dan, 3d-nang-cao]
level: intermediate
minutes: 25
needs: [ac-09-03]
appVersions: ['2024', '2025']
edition: full-only
---
# Tạo hình nâng cao với REVOLVE, SWEEP và LOFT

> **Mục tiêu:**
> - Sử dụng lệnh `REVOLVE` để quay biên dạng 2D quanh một trục tâm tạo các chi tiết tròn xoay (trục, puly, bình lọ).
> - Sử dụng lệnh `SWEEP` để quét biên dạng trượt dọc theo đường cong 3D dẫn hướng (ống nước, tay vịn cầu thang, lò xo).
> - Sử dụng lệnh `LOFT` để nối chuyển tiếp mượt mà qua các mặt cắt tiết diện khác nhau (côn chuyển ống gió, vỏ tàu thuyền).

## Bộ ba công cụ tạo hình 3D phức tạp

Trong thực tế chế tạo máy và kiến trúc, có rất nhiều vật thể có hình dáng uốn lượn mà lệnh `EXTRUDE` kéo thẳng không thể nào làm được:
- Một cái trục bậc cơ khí, một cái bát đựng nước hoặc một cái puly truyền đai: Có dạng tròn xoay đồng tâm quanh một trục.
- Một đường ống dẫn dầu uốn lượn quanh co trong nhà máy: Có tiết diện tròn chạy dọc theo một đường ống 3 chiều.
- Một phễu nạp liệu chuyển tiếp từ miệng trên hình chữ nhật xuống miệng dưới hình tròn: Có các mặt cắt khác nhau hoàn toàn.

Bộ ba công cụ **`REVOLVE`**, **`SWEEP`** và **`LOFT`** là chìa khóa để giải quyết trọn vẹn mọi hình thái hình học phức tạp này.

## 1. Khối tròn xoay với lệnh REVOLVE (Lệnh tắt REV)

Nguyên lý: Bạn chỉ cần vẽ đúng **một nửa mặt cắt của vật thể**, sau đó quay mặt cắt này quanh một trục tâm 360 độ!

### Cách dùng từng bước:
1. Vẽ một nửa mặt cắt của chi tiết trục bậc bằng lệnh `PLINE` khép kín (ví dụ nửa biên dạng của một cái puly).
2. Dùng `LINE` vẽ một đường thẳng đứng làm trục xoay tâm.
3. Gõ `REV` hoặc `REVOLVE` rồi nhấn [Enter].
4. Bấm chọn biên dạng mặt cắt vừa vẽ, nhấn [Enter].
5. Bấm chọn 2 điểm trên đường thẳng trục xoay (Specify axis start point and end point).
6. Nhập góc xoay: Mặc định là `360` độ (quay tròn hoàn chỉnh) rồi nhấn [Enter].
7. Ngay lập tức, một chi tiết puly tròn xoay 3D hoàn mỹ xuất hiện trước mắt bạn!

## 2. Quét khối trượt theo đường dẫn với lệnh SWEEP

Nguyên lý: Bạn có một hình tiết diện (Profile - ví dụ hình tròn đường kính 50mm) và một đường dẫn (Path - ví dụ một đường cong `SPLINE` hoặc `POLYLINE` uốn lượn). Lệnh `SWEEP` sẽ kéo hình tiết diện trượt dọc suốt chiều dài của đường cong đó.

### Cách dùng từng bước:
1. Vẽ một đường cong uốn lượn tự do trong không gian bằng lệnh `SPLINE`.
2. Vẽ một hình tròn đường kính 30mm bằng `CIRCLE` đặt ở điểm đầu của đường cong.
3. Gõ `SWEEP` rồi nhấn [Enter].
4. Bấm chọn hình tròn (đối tượng cần quét), nhấn [Enter].
5. Bấm chọn đường cong Spline (đường dẫn hướng).
6. Hình tròn sẽ tự động chạy trượt dọc theo đường cong và biến thành một đường ống mềm uốn lượn 3D tuyệt đẹp!

## 3. Nối chuyển tiếp các tiết diện với lệnh LOFT

Nguyên lý: Bạn có nhiều mặt cắt khác nhau được xếp tầng song song theo chiều cao. Lệnh `LOFT` sẽ phủ một lớp da khối đặc nối mượt mà từ mặt cắt này sang mặt cắt kia.

### Cách dùng từng bước:
1. Ở tầng dưới cùng (Z = 0): Vẽ một hình chữ nhật lớn 100 x 100 mm bằng `RECTANG`.
2. Ở tầng lơ lửng phía trên (Z = 150): Vẽ một hình tròn bán kính 30mm bằng `CIRCLE` (nằm cao hơn 150mm).
3. Gõ `LOFT` rồi nhấn [Enter].
4. Bấm chọn hình chữ nhật ở đáy, rồi bấm tiếp chọn hình tròn ở trên, nhấn [Enter] 2 lần.
5. Một khối phễu chuyển đổi tiết diện từ vuông sang tròn xuất hiện vô cùng mượt mà và chính xác!

> [!TIP]
> Trong lệnh `REVOLVE`, nếu bạn không nhập 360 độ mà nhập `270` độ hoặc `180` độ, bạn sẽ tạo ra một mặt cắt bổ đôi chi tiết máy rất trực quan để quan sát cấu tạo bên trong!

## Tự kiểm tra

```quiz
id: q-ac-09-04-1
type: single
question: "Để dựng một chi tiết cơ khí tròn xoay đối xứng tâm như trục xe, bình chứa hoặc puly đai truyền, lệnh nào là tối ưu nhất?"
options:
  - text: "REVOLVE (lệnh tắt REV)"
    correct: true
    why: "REVOLVE quay một nửa biên dạng 2D quanh trục để tạo thành khối tròn xoay 3D."
  - text: "EXTRUDE"
    why: "EXTRUDE chỉ kéo đùn thẳng theo phương vuông góc."
  - text: "MIRROR"
    why: "MIRROR chỉ lấy đối xứng 2D phẳng."
  - text: "ROTATE"
    why: "ROTATE chỉ xoay góc của đối tượng 2D."
explain: "Sử dụng REVOLVE để tạo toàn bộ các chi tiết máy dạng tròn xoay trong cơ khí chính xác."
```

```quiz
id: q-ac-09-04-2
type: single
question: "Lệnh SWEEP trong AutoCAD yêu cầu người vẽ cung cấp hai thành phần đầu vào nào?"
options:
  - text: "Một hình tiết diện (Profile) và một đường dẫn (Path)"
    correct: true
    why: "SWEEP kéo trượt hình tiết diện dọc theo đường dẫn để sinh ra khối 3D."
  - text: "Hai điểm mốc và một con số chiều cao"
    correct: false
    why: "Đây là thông số của lệnh EXTRUDE hoặc BOX."
  - text: "Bảng nét in CTB và khổ giấy in"
    correct: false
    why: "Đây là các thông số của lệnh in ấn Layout."
  - text: "Mười bức ảnh chụp vệ tinh"
    correct: false
    why: "Không liên quan đến ảnh vệ tinh."
explain: "Biên dạng mặt cắt (Profile) và đường tim dẫn hướng (Path) là cặp thông số bắt buộc của lệnh SWEEP."
```

```quiz
id: q-ac-09-04-3
type: truefalse
question: "Lệnh LOFT cho phép nối chuyển tiếp mượt mà giữa các mặt cắt có hình dạng khác nhau (ví dụ từ hình chữ nhật ở đáy lên hình tròn ở đỉnh)."
answer: true
explain: "LOFT là công cụ đắc lực để thiết kế các đường ống chuyển tiết diện gió, thân cánh máy bay và thân xe hơi khí động học."
```

## Lỗi thường gặp

- **REVOLVE báo lỗi Self-intersecting (Tự giao cắt):** Do biên dạng của bạn vẽ bị lấn qua trục xoay tâm, hoặc trục xoay cắt ngang qua thân hình. Khắc phục: Đường trục xoay phải nằm ngoài mép hoặc trùng khít với đường bao cạnh của nửa biên dạng.
- **SWEEP bị xoắn hoặc méo góc:** Do bán kính góc uốn của đường dẫn quá hẹp so với đường kính của hình tiết diện khiến vật thể bị tự cắn vào nhau. Khắc phục: Bo rộng bán kính cong của đường dẫn.

## Bài tập thực hành

- [ ] Chuyển sang góc nhìn `SW Isometric`.
- [ ] Dùng `PLINE` vẽ một hình thang khép kín có đáy lớn 40mm, đáy nhỏ 20mm, chiều cao 50mm. <!-- expect: PLINE -->
- [ ] Gõ lệnh `REVOLVE` (hoặc `REV`), chọn hình thang và chọn cạnh đứng làm trục xoay 360 độ để tạo một chiếc puly tròn xoay. <!-- expect: REVOLVE -->
- [ ] Dùng `SPLINE` vẽ một đường cong lượn sóng tự do. <!-- expect: SPLINE -->
- [ ] Dùng `CIRCLE` vẽ một đường tròn bán kính 10mm tại đầu đường cong, sau đó dùng `SWEEP` tạo ống cong 3D. <!-- expect: SWEEP -->
- [ ] Dùng `LOFT` tạo một hình côn chuyển đổi tiết diện từ hình chữ nhật sang hình tròn. <!-- expect: LOFT -->

## Nguồn tham khảo

```links
- title: "Quay khối tròn xoay với lệnh REVOLVE từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=REVOLVE"
  kind: official
- title: "Quét khối trượt đường dẫn với lệnh SWEEP từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=SWEEP"
  kind: official
```
