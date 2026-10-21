---
id: ac-09-07
title: Gia công mép cạnh khối 3D với FILLETEDGE và CHAMFEREDGE
category: Mô hình hoá 3D
tags: [filletedge, chamferedge, bo-canh, vat-mep, solid-editing]
level: intermediate
minutes: 20
needs: [ac-09-05]
appVersions: ['2024', '2025']
edition: full-only
---
# Gia công mép cạnh khối 3D với FILLETEDGE và CHAMFEREDGE

> **Mục tiêu:**
> - Sử dụng lệnh `FILLETEDGE` để bo tròn các cạnh sắc nhọn của khối đặc 3D Solid với bán kính uốn cong mượt mà.
> - Sử dụng lệnh `CHAMFEREDGE` để vát mép cạnh kỹ thuật theo khoảng cách vát hoặc góc vát.
> - Làm chủ tuỳ chọn chọn chuỗi liên tục (`Chain`) và chọn vòng mép (`Loop`) để gia công hàng loạt cạnh trong một lần bấm.

## Hoàn thiện gia công: Loại bỏ các góc cạnh sắc nhọn nguy hiểm

Khi mới tạo các khối 3D bằng `BOX` hay `EXTRUDE`, các mép cạnh giao nhau luôn là góc vuông 90° sắc lẹm. Trong thực tế sản xuất cơ khí và chế tạo sản phẩm tiêu dùng:
- Các góc nhọn sắc dễ gây đứt tay cho công nhân và người sử dụng.
- Góc nhọn là nơi tập trung ứng suất cơ học cao nhất (Stress concentration), rất dễ làm nứt vỡ chi tiết khi chịu lực va đập.
- Khuôn đúc hoặc máy phay CNC luôn đòi hỏi các góc lượn bán kính để dòng kim loại nóng chảy điền đầy và dao phay có thể lướt qua.

Để gia công bo tròn và vát mép trực tiếp trên khối đặc 3D Solid, AutoCAD cung cấp hai công cụ chuyên dụng: **`FILLETEDGE`** (Bo tròn) và **`CHAMFEREDGE`** (Vát mép).

## 1. Bo tròn cạnh 3D với lệnh FILLETEDGE

### Cách dùng từng bước:
1. Gõ `FILLETEDGE` rồi nhấn [Enter] (hoặc bấm nút *Fillet Edge* trên thẻ Solid Editing).
2. Dòng lệnh nhắc: `Select an edge or [Chain/Loop/Radius]:`.
3. Gõ `R` (Radius) rồi nhấn [Enter] để cài đặt bán kính bo tròn.
4. Nhập giá trị bán kính: ví dụ nhập `10` mm rồi nhấn [Enter].
5. Bấm chuột chọn vào cạnh sắc của khối 3D cần bo tròn:
   - Một đường viền uốn cong xem trước (Preview) màu vàng sẽ xuất hiện ngay tại cạnh đó.
6. Bạn có thể bấm chọn tiếp các cạnh khác nếu muốn bo cùng bán kính 10mm.
7. Nhấn [Enter] hai lần để xác nhận thực hiện.
8. Mép cạnh sắc nhọn lập tức được mài tròn mượt mà và bóng bẩy!

### Các tùy chọn chọn cạnh thông minh:
- **`Chain` (Chuỗi tiếp xúc):** Nếu cạnh bạn chọn nối liền tiếp tuyến với các cạnh cong khác, AutoCAD sẽ tự động bắt trọn toàn bộ chuỗi đường viền quanh chi tiết chỉ với 1 cú click.
- **`Loop` (Vòng chu vi mặt):** Chọn toàn bộ các cạnh bao quanh một mặt phẳng của khối mà không cần bấm từng cạnh một.

## 2. Vát mép cạnh kỹ thuật với lệnh CHAMFEREDGE

Thay vì bo tròn cung cong, `CHAMFEREDGE` gọt phẳng mép cạnh một góc xiên (ví dụ vát góc C2x45° ở đầu trục hoặc miệng lỗ khoan bu lông để dễ bắt ốc vít).

### Cách dùng từng bước:
1. Gõ `CHAMFEREDGE` rồi nhấn [Enter].
2. Dòng lệnh nhắc: `Select an edge or [Loop/Distance]:`.
3. Gõ `D` (Distance) rồi nhấn [Enter] để cài đặt kích thước vát:
   - *Enter first chamfer distance:* Nhập khoảng cách vát mép thứ nhất: ví dụ `5` mm.
   - *Enter second chamfer distance:* Nhập khoảng cách vát mép thứ hai: ví dụ `5` mm.
4. Bấm chuột chọn vào cạnh cần vát mép.
5. Nhấn [Enter] hai lần để hoàn tất.
6. Mép cạnh được vát chéo một mặt phẳng 45 độ phẳng phiu và chuẩn kỹ thuật!

## Kéo tay kẹp điều chỉnh bán kính trực tiếp (Direct Manipulation)

Trong AutoCAD phiên bản mới:
- Khi đang ở trong bước xem trước của `FILLETEDGE`, bạn sẽ thấy một mũi tên tay kẹp màu xanh nhỏ xuất hiện ngay tại cung tròn.
- Bạn có thể **dùng chuột kéo mũi tên** đó vào hoặc ra để xem trực quan sự thay đổi kích thước bo tròn theo thời gian thực trước khi nhấn Enter chốt kích thước!

> [!WARNING]
> Bán kính bo tròn `Radius` không được phép lớn hơn kích thước hình học của mặt phẳng tiếp giáp. Ví dụ: Khối hộp chỉ dày 15mm thì bạn không thể bo tròn với bán kính R20 được vì sẽ làm triệt tiêu mất bề mặt của khối!

## Tự kiểm tra

```quiz
id: q-ac-09-07-1
type: single
question: "Lệnh nào trong AutoCAD chuyên dùng để bo tròn các mép cạnh sắc nhọn của khối đặc 3D Solid với bán kính cong uốn lượn?"
options:
  - text: "FILLETEDGE"
    correct: true
    why: "FILLETEDGE là lệnh chuyên biệt để bo tròn cạnh của khối đặc 3D Solid."
  - text: "FILLET"
    why: "FILLET thông thường tối ưu cho đường nét 2D phẳng."
  - text: "ROUND"
    why: "ROUND không phải lệnh AutoCAD chuẩn."
  - text: "SMOOTH"
    why: "SMOOTH dùng để làm mịn lưới Mesh."
explain: "Sử dụng FILLETEDGE để gia công các góc lượn đúc và bo viền an toàn cho chi tiết máy 3D."
```

```quiz
id: q-ac-09-07-2
type: single
question: "Trong lệnh FILLETEDGE, tùy chọn nào cho phép người vẽ chọn nhanh toàn bộ một chuỗi các cạnh nối tiếp tuyến liên tục chỉ bằng một cú click chuột?"
options:
  - text: "Tùy chọn Chain"
    correct: true
    why: "Chain tự động lần theo các cạnh tiếp xúc mượt mà để chọn toàn bộ chuỗi cạnh."
  - text: "Tùy chọn Single"
    why: "Single chỉ chọn từng cạnh đơn lẻ."
  - text: "Tùy chọn Erase"
    why: "Erase dùng để xóa đối tượng."
  - text: "Tùy chọn Offset"
    why: "Offset là lệnh song song 2D."
explain: "Tùy chọn Chain giúp tiết kiệm thời gian đáng kể khi phải bo tròn đường viền quanh một chi tiết uốn lượn phức tạp."
```

```quiz
id: q-ac-09-07-3
type: truefalse
question: "Bạn không thể đặt bán kính bo tròn FILLETEDGE lớn hơn chiều dày hình học của cạnh vật thể tiếp giáp."
answer: true
explain: "Bán kính quá lớn sẽ làm hình học tự triệt tiêu bề mặt, khiến AutoCAD báo lỗi tính toán hình khối (Modeling failure)."
```

## Lỗi thường gặp

- **AutoCAD báo lỗi Fillet failure / Chamfer failure:** Do bán kính đặt quá to làm các góc bo ở hai đầu cạnh đè chéo lên nhau. Khắc phục: Giảm giá trị bán kính `Radius` nhỏ xuống (ví dụ từ 20mm giảm về 5mm).
- **Chọn nhầm mặt thay vì chọn cạnh:** Khi rê chuột cần ngắm chuẩn vào đường cạnh viền của khối 3D để cạnh sáng lên trước khi bấm chuột.

## Bài tập thực hành

- [ ] Gõ `BOX`, vẽ một khối hộp chữ nhật kích thước 120 x 80 x 60 mm. <!-- expect: BOX -->
- [ ] Gõ lệnh `FILLETEDGE`, nhập `R` đặt bán kính bo tròn là 15 mm. <!-- expect: FILLETEDGE -->
- [ ] Bấm chọn 4 cạnh thẳng đứng của khối hộp, nhấn Enter hai lần để bo tròn 4 góc. <!-- expect: FILLETEDGE -->
- [ ] Gõ lệnh `CHAMFEREDGE`, nhập `D` đặt khoảng cách vát mép là 5 mm cho cả hai cạnh. <!-- expect: CHAMFEREDGE -->
- [ ] Bấm chọn chu vi mép trên đỉnh khối hộp và nhấn Enter hai lần để vát phẳng mép cạnh. <!-- expect: CHAMFEREDGE -->

## Nguồn tham khảo

```links
- title: "Bo tròn cạnh 3D với FILLETEDGE từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=FILLETEDGE"
  kind: official
- title: "Vát mép cạnh 3D với CHAMFEREDGE từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=CHAMFEREDGE"
  kind: official
```
