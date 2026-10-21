---
id: ac-09-09
title: Phân biệt bản chất mô hình Solid, Surface và Mesh trong AutoCAD
category: Mô hình hoá 3D
tags: [solid, surface, mesh, massprop, mo-hinh-hoa-3d]
level: intermediate
minutes: 20
needs: [ac-09-03]
appVersions: ['2024', '2025']
edition: full-only
---
# Phân biệt bản chất mô hình Solid, Surface và Mesh trong AutoCAD

> **Mục tiêu:**
> - Phân biệt bản chất hình học, cấu trúc dữ liệu và phạm vi ứng dụng giữa 3 loại mô hình: [[Solid]], [[Surface]] và [[Mesh]].
> - Tra cứu các đặc tính vật lý thực tế (thể tích, khối lượng, trọng tâm, mô men quán tính) với lệnh `MASSPROP`.
> - Chuyển đổi linh hoạt giữa các định dạng mô hình phục vụ mô phỏng và gia công chế tạo.

## Ba trường phái mô hình hoá 3D

Khi làm việc trong môi trường 3D của AutoCAD, bạn sẽ thấy trên thanh Ribbon xuất hiện 3 thẻ công cụ chuyên biệt: **Solid**, **Surface** và **Mesh**. Rất nhiều người dùng bối rối không biết khi nào nên dùng loại nào và tại sao cùng là hình quả cầu mà máy tính lại đối xử khác nhau.

Mỗi loại mô hình đại diện cho một triết lý toán học và mục đích sử dụng hoàn toàn khác nhau trong nền công nghiệp hiện đại.

## Bảng so sánh toàn diện: Solid vs Surface vs Mesh

| Đặc tính | Khối đặc (3D Solid) | Bề mặt (3D Surface) | Lưới đa giác (3D Mesh) |
|---|---|---|---|
| **Cấu trúc ruột** | **Đặc ruột 100%**, có thể tích và khối lượng | **Rỗng ruột**, chỉ là một lớp vỏ bọc không có chiều dày | **Rỗng ruột**, ghép từ các mặt tam giác / tứ giác |
| **Phép toán Boolean** | **Hỗ trợ đầy đủ** (Cộng, Trừ, Giao nhau dễ dàng) | Giới hạn (chỉ cắt xén Trim/Extend bề mặt) | Không hỗ trợ Boolean trực tiếp |
| **Gia công mép** | Hỗ trợ bo tròn `FILLETEDGE`, vát `CHAMFEREDGE` | Rất khó bo cạnh sắc | Làm mịn bằng cách tăng mật độ lưới Smooth |
| **Tính toán kỹ thuật** | **Tra cứu khối lượng, trọng tâm bằng `MASSPROP`** | Không có khối lượng | Không có khối lượng |
| **Lĩnh vực ứng dụng** | **Cơ khí chính xác, xây dựng, kết cấu, máy móc** | Thiết kế vỏ xe hơi, thân tàu thủy, mặt cong tự do | Game 3D, phim hoạt hình, điêu khắc nghệ thuật |

## 1. Khối đặc 3D Solid: Tiêu chuẩn vàng của kỹ thuật

Khối đặc Solid là đối tượng quan trọng nhất mà bạn đã học từ đầu chặng 9 đến giờ (`BOX`, `CYLINDER`, `EXTRUDE`, `UNION`, `SUBTRACT`):
- Nó đại diện cho một cục kim loại hoặc một khối bê tông đúc ngoài đời thực.
- Bạn có thể khoan lỗ, cắt gọt, phay rãnh mà khối hình vẫn luôn đảm bảo tính khép kín kín đặc.

### Tra cứu đặc tính vật lý với lệnh MASSPROP
Bạn muốn biết chi tiết cơ khí bằng thép này nặng bao nhiêu kg và điểm đặt trọng tâm nằm ở đâu để móc cáp cẩu?
1. Gõ `MASSPROP` rồi nhấn [Enter].
2. Bấm chọn chi tiết 3D Solid, nhấn [Enter].
3. Một bảng báo cáo kỹ thuật xuất hiện ngay lập tức:
   - `Mass` (Khối lượng thể tích).
   - `Volume` (Thể tích chính xác tính bằng $mm^3$).
   - `Bounding box` (Kích thước bao phủ bì X, Y, Z).
   - `Centroid` (Toạ độ trọng tâm tuyệt đối).
   - `Moments of inertia` (Mô men quán tính các trục).
4. Nhấn `Y` để lưu toàn bộ báo cáo này thành tệp văn bản `.mpr` phục vụ tính toán kết cấu!

## 2. Bề mặt 3D Surface: Nghệ thuật của các đường cong khí động học

Khác với Solid cục mịch, Surface là những màng bọc mỏng manh uốn lượn:
- Thường được tạo từ các đường cong NURBS hoặc lệnh `LOFT` qua các đường biên hở.
- Ứng dụng: Thiết kế vỏ ngoài bóng bẩy của chuột máy tính, nắp capo ô tô, cánh quạt tuabin gió.
- Khi các mặt Surface được khâu kín lại với nhau bằng lệnh `SURFSCULPT`, chúng sẽ tự động biến hóa thành một khối đặc Solid hoàn chỉnh!

## 3. Lưới đa giác 3D Mesh: Sức mạnh uốn nắn điêu khắc

Mesh cấu tạo từ các mắt lưới đỉnh, cạnh và mặt:
- Giống như một tấm lưới thép hoặc đất sét kỹ thuật số.
- Bạn có thể kéo từng đỉnh (Vertex) nhô lên hoặc ấn lõm xuống để tạo mặt đồi núi mấp mô, địa hình trắc địa phức tạp hoặc các chi tiết điêu khắc nghệ thuật.

## Chuyển đổi qua lại giữa các định dạng

AutoCAD cung cấp các lệnh hoán đổi linh hoạt:
- **`CONVTOSOLID`:** Chuyển đổi bề mặt kín Surface hoặc lưới Mesh thành khối đặc Solid.
- **`CONVTOSURFACE`:** Biến các mặt của khối Solid thành các bề mặt mỏng Surface.
- **`CONVTOMESH`:** Chuyển khối Solid thành lưới đa giác Mesh để phục vụ uốn nắn.

> [!TIP]
> Trong thiết kế kỹ thuật chế tạo, hãy luôn ưu tiên sử dụng **3D Solid** làm định dạng chuẩn mực vì nó có thể chuyển đổi trực tiếp sang các phần mềm gia công cơ khí CAM (phay tiện CNC) và máy in 3D (xuất file `.stl`).

## Tự kiểm tra

```quiz
id: q-ac-09-09-1
type: single
question: "Lệnh nào trong AutoCAD giúp người kỹ sư tra cứu toàn bộ các đặc tính vật lý như thể tích, toạ độ trọng tâm và mô men quán tính của khối 3D Solid?"
options:
  - text: "MASSPROP"
    correct: true
    why: "MASSPROP tính toán toàn diện các thuộc tính khối lượng và trọng tâm của khối đặc 3D Solid."
  - text: "LIST"
    why: "LIST chỉ hiển thị thông số hình học cơ bản."
  - text: "DIST"
    why: "DIST chỉ đo khoảng cách giữa 2 điểm."
  - text: "AREA"
    why: "AREA tính chu vi và diện tích 2D phẳng."
explain: "Lệnh MASSPROP (Mass Properties) là công cụ chuyên nghiệp phục vụ tính toán trọng lượng và kiểm tra cơ học kết cấu."
```

```quiz
id: q-ac-09-09-2
type: single
question: "Khác biệt bản chất giữa mô hình 3D Solid và 3D Surface trong AutoCAD là gì?"
options:
  - text: "Solid là khối đặc ruột có thể tích và khối lượng, còn Surface là lớp vỏ rỗng ruột không có chiều dày"
    correct: true
    why: "Solid chứa đựng thể tích vật chất bên trong, Surface chỉ là bề mặt bao bọc bên ngoài."
  - text: "Solid chỉ có màu đen, Surface chỉ có màu trắng"
    correct: false
    why: "Cả hai đều đổi màu sắc bình thường theo Layer."
  - text: "Solid không thể in ra giấy được"
    correct: false
    why: "Mọi đối tượng đều in ra giấy bình thường."
  - text: "Surface luôn luôn vẽ nhanh hơn gấp 10 lần"
    correct: false
    why: "Tốc độ vẽ phụ thuộc vào độ phức tạp của hình học."
explain: "Tính đặc ruột và khả năng thực hiện các phép toán Boolean là đặc trưng nhận diện cốt lõi của 3D Solid."
```

```quiz
id: q-ac-09-09-3
type: truefalse
question: "Bạn có thể chuyển đổi một tập hợp các bề mặt Surface khép kín thành một khối đặc 3D Solid hoàn chỉnh bằng lệnh SURFSCULPT hoặc CONVTOSOLID."
answer: true
explain: "AutoCAD hỗ trợ chuyển đổi từ vỏ bề mặt kín thành khối đặc kỹ thuật phục vụ gia công CNC."
```

## Lỗi thường gặp

- **Chạy lệnh MASSPROP nhưng phần mềm báo 'No solids selected':** Do vật thể bạn chọn là bề mặt Surface hoặc lưới Mesh chứ không phải khối Solid đặc. Hãy dùng `CONVTOSOLID` trước khi kiểm tra trọng lượng.
- **Không thể thực hiện SUBTRACT hay UNION:** Do vật thể được tạo từ các đoạn thẳng hở của Surface hoặc Mesh.

## Bài tập thực hành

- [ ] Gõ `CYLINDER`, vẽ một hình trụ tròn bán kính 50mm, chiều cao 100mm. <!-- expect: CYLINDER -->
- [ ] Gõ lệnh `MASSPROP`, bấm chọn hình trụ vừa vẽ để mở bảng báo cáo đặc tính khối lượng. <!-- expect: MASSPROP -->
- [ ] Đọc các thông số thể tích `Volume` và toạ độ trọng tâm `Centroid` hiển thị trên màn hình.
- [ ] Đóng cửa sổ báo cáo và lưu lại kết quả.

## Nguồn tham khảo

```links
- title: "So sánh Solid, Surface và Mesh từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+3D+Models"
  kind: official
- title: "Lệnh MASSPROP tra cứu đặc tính vật lý từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=MASSPROP"
  kind: official
```
