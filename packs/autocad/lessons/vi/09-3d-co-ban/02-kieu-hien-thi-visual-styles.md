---
id: ac-09-02
title: Điều khiển kiểu hiển thị trực quan với Visual Styles
category: Mô hình hoá 3D
tags: [visual-styles, vscurrent, shaded, conceptual, wireframe, x-ray]
level: intermediate
minutes: 20
needs: [ac-09-01]
appVersions: ['2024', '2025']
edition: full-only
---
# Điều khiển kiểu hiển thị trực quan với Visual Styles

> **Mục tiêu:**
> - Sử dụng lệnh `VSCURRENT` để chuyển đổi linh hoạt giữa các kiểu hiển thị mô hình 3D.
> - Phân biệt đặc tính và ứng dụng của các kiểu: 2D Wireframe, Conceptual, Hidden, Shaded with Edges và X-Ray.
> - Tối ưu hóa hiệu năng hiển thị đồ họa card màn hình khi thao tác trên các mô hình 3D dung lượng lớn.

## Trực quan hóa mô hình: Từ khung dây đến vật thể sống động

Khi bạn mới dựng một khối hộp 3D trong AutoCAD, mặc định phần mềm hiển thị nó dưới dạng các đường viền khung dây rỗng ruột (**2D Wireframe**). Với chế độ này, bạn rất khó phân biệt đâu là mặt trước, đâu là mặt sau, và không thể cảm nhận được độ lồi lõm của hình khối.

Hệ thống **[[Visual Styles]] (Kiểu hiển thị trực quan)** cung cấp các bộ lọc đồ họa thời gian thực giúp bạn biến các khung dây khô khan thành những khối đặc đổ bóng chân thực, bóng bẩy hoặc bán trong suốt như tia X-quang.

Bạn có thể chuyển đổi nhanh kiểu hiển thị ở menu chữ nhỏ góc trên bên trái của vùng vẽ (mặc định đang ghi chữ `[2D Wireframe]`), hoặc sử dụng lệnh **`VSCURRENT`**.

## 6 kiểu hiển thị thông dụng nhất

1. **2D Wireframe (Khung dây 2D):**
   - Chỉ hiển thị các đường nét và cạnh của vật thể, không có bề mặt.
   - *Ưu điểm:* Cực kỳ nhẹ máy, tốc độ xoay mượt mà nhất. Thích hợp khi vẽ phác thảo hoặc bắt điểm ở các góc khuất.
2. **Hidden (Nét khuất):**
   - Ẩn toàn bộ các cạnh và bề mặt nằm ở phía sau vật thể bị che khuất.
   - Trông giống như một bức vẽ tay kỹ thuật mực đen trên giấy trắng.
3. **Conceptual (Ý niệm):**
   - Bề mặt được tô màu mịn màng chuyển tông màu mát (Cool colors) sang tông màu ấm (Warm colors).
   - Rất dễ nhìn thấy độ uốn lượn và góc cong của chi tiết máy.
4. **Shaded with Edges (Đổ bóng kèm nét cạnh - Khuyên dùng nhiều nhất):**
   - Bề mặt được đổ bóng 3D chân thực, đồng thời **các đường cạnh viền (Edges) được tô đậm sắc nét**.
   - Đây là kiểu hiển thị lý tưởng nhất cho kỹ sư thiết kế vì vừa nhìn thấy khối đặc vừa dễ dàng bắt điểm chính xác vào các cạnh.
5. **Realistic (Vật liệu thực):**
   - Hiển thị đầy đủ vật liệu (gỗ, kính, kim loại) và ánh sáng môi trường thực tế. Thích hợp khi chuẩn bị xuất ảnh phối cảnh.
6. **X-Ray (Tia X-quang bán trong suốt):**
   - Toàn bộ khối đặc trở nên bán trong suốt 50%.
   - Cho phép bạn nhìn xuyên thấu vào các trục xoay, lò xo hoặc lỗ khoét nằm sâu bên trong ruột máy mà không cần phải cắt đôi chi tiết!

## Cách dùng từng bước

### 1. Đổi kiểu hiển thị qua menu chữ trên màn hình (Nhanh nhất)
1. Nhìn lên góc trên bên trái của khung vẽ, bạn sẽ thấy 3 chữ nằm trong dấu ngoặc vuông: `[-] [Top] [2D Wireframe]`.
2. Bấm chuột trái vào chữ **`[2D Wireframe]`**.
3. Một danh sách xổ xuống: Bấm chọn **Shaded with Edges** (hoặc **Conceptual**).
4. Khối mô hình lập tức biến thành vật thể đặc đổ bóng sắc nét và bắt mắt!

### 2. Sử dụng lệnh VSCURRENT
1. Gõ `VSCURRENT` rồi nhấn [Enter].
2. Dòng lệnh nhắc các tùy chọn: `[2wireframe/Wireframe/Hidden/Realistic/Conceptual/Shaded/shades of Gray/SKetchy/X-ray]`.
3. Gõ chữ cái viết tắt tương ứng (ví dụ: gõ `C` cho Conceptual, gõ `X` cho X-ray) rồi nhấn [Enter].

## Mẹo tối ưu hóa card đồ họa cho mô hình 3D nặng

Khi mô hình của bạn có hàng ngàn chi tiết máy phức tạp, việc để chế độ `Realistic` liên tục có thể làm quạt tản nhiệt máy tính kêu to và thao tác xoay bị giật khung hình:
- Hãy chuyển về **Shaded with Edges** hoặc **Conceptual** trong quá trình dựng hình hàng ngày.
- Gõ lệnh `GRAPHICSCONFIG` rồi nhấn Enter để kiểm tra card màn hình rời (NVIDIA / AMD) đã được bật tính năng tăng tốc phần cứng **Hardware Acceleration** hay chưa.

> [!TIP]
> Kiểu hiển thị `Sketchy` mô phỏng nét vẽ phác thảo nghệ thuật bằng bút chì chì tay rất thích hợp để gửi cho khách hàng xem ý tưởng sơ bộ phương án kiến trúc!

## Tự kiểm tra

```quiz
id: q-ac-09-02-1
type: single
question: "Kiểu hiển thị Visual Style nào được các kỹ sư cơ khí và xây dựng ưa chuộng nhất khi dựng hình 3D vì vừa thấy khối đặc vừa thấy rõ đường nét cạnh để bắt điểm?"
options:
  - text: "Shaded with Edges"
    correct: true
    why: "Shaded with Edges kết hợp giữa đổ bóng bề mặt và làm nổi bật các đường viền cạnh."
  - text: "2D Wireframe"
    correct: false
    why: "2D Wireframe không có bề mặt đặc, khó phân biệt độ lồi lõm."
  - text: "Realistic"
    correct: false
    why: "Realistic ẩn đường viền nét cạnh nên khó bắt điểm góc mút."
  - text: "Sketchy"
    correct: false
    why: "Sketchy là kiểu nét chì nghệ thuật, không dùng cho gia công chính xác."
explain: "Shaded with Edges là chế độ làm việc tối ưu nhất cân bằng giữa tính thẩm mỹ khối đặc và sự chính xác của các điểm bắt cạnh hình học."
```

```quiz
id: q-ac-09-02-2
type: single
question: "Kiểu hiển thị nào làm vật thể trở nên bán trong suốt 50%, giúp người vẽ quan sát xuyên thấu vào các bộ phận lỗ khoan nằm trong ruột máy?"
options:
  - text: "X-Ray"
    correct: true
    why: "X-Ray mô phỏng tia X xuyên thấu hiển thị chi tiết ngầm bên trong."
  - text: "Hidden"
    correct: false
    why: "Hidden che giấu hoàn toàn các chi tiết phía sau."
  - text: "Conceptual"
    correct: false
    why: "Conceptual là khối đặc đục hoàn toàn."
  - text: "2D Wireframe"
    correct: false
    why: "Wireframe là khung dây, không có hiệu ứng bán trong suốt."
explain: "Sử dụng chế độ X-Ray khi cần kiểm tra độ ăn khớp của trục, ổ bi hoặc bulông lắp chìm trong thân máy."
```

```quiz
id: q-ac-09-02-3
type: truefalse
question: "Lệnh VSCURRENT cho phép chuyển đổi chế độ hiển thị đồ họa trực quan trực tiếp thông qua thanh dòng lệnh."
answer: true
explain: "VSCURRENT hỗ trợ gọi nhanh các kiểu hiển thị bằng các ký tự viết tắt trên thanh dòng lệnh CLI."
```

## Lỗi thường gặp

- **Không nhìn thấy mặt phẳng tô bóng dù đã đổi sang Shaded:** Do vật thể bạn vẽ chỉ là các đoạn thẳng `LINE` 2D hở chứ không phải là khối đặc `3D Solid`. Hãy chuyển sang bài tiếp theo để học cách đùn khối đặc.
- **Màn hình bị đen xì khi chuyển sang Realistic:** Do môi trường chưa bật đèn chiếu sáng hoặc độ sáng mặc định bị kéo xuống 0. Khắc phục: Chuyển về kiểu `Shaded with Edges` hoặc bật đèn mặc định `DEFAULTLIGHTING = 1`.

## Bài tập thực hành

- [ ] Gõ lệnh `BOX`, vẽ một khối hộp kích thước 150 x 150 x 100 mm. <!-- expect: BOX -->
- [ ] Gõ lệnh `CYLINDER`, vẽ một khối trụ tròn bán kính 40mm, cao 120mm xuyên qua khối hộp. <!-- expect: CYLINDER -->
- [ ] Gõ lệnh `VSCURRENT`, chọn chế độ `Conceptual` để quan sát khối đổi sang màu ý niệm. <!-- expect: VSCURRENT -->
- [ ] Gõ tiếp `VSCURRENT`, chọn chế độ `X-ray` để quan sát độ xuyên thấu của khối trụ bên trong hộp. <!-- expect: VSCURRENT -->
- [ ] Đổi lại kiểu hiển thị sang `Shaded with Edges` để sẵn sàng cho các bài thực hành sau. <!-- expect: VSCURRENT -->

## Nguồn tham khảo

```links
- title: "Quản lý Visual Styles trong không gian 3D từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=About+Visual+Styles"
  kind: official
- title: "Lệnh VSCURRENT chuyển kiểu hiển thị từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=VSCURRENT"
  kind: official
```
