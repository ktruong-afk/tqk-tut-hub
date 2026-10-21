---
id: ac-09-05
title: Làm chủ phép toán hợp, trừ và giao khối Boolean
category: Mô hình hoá 3D
tags: [boolean, union, subtract, intersect, solid, cat-khoi]
level: intermediate
minutes: 25
needs: [ac-09-03]
appVersions: ['2024', '2025']
edition: full-only
---
# Làm chủ phép toán hợp, trừ và giao khối Boolean

> **Mục tiêu:**
> - Sử dụng lệnh `UNION` để gộp nhiều khối đặc rời rạc thành một vật thể duy nhất.
> - Sử dụng lệnh `SUBTRACT` để trừ khối và khoét các hốc rỗng, lỗ ren cơ khí phức tạp.
> - Áp dụng lệnh `INTERSECT` để trích xuất phần thể tích giao nhau chung giữa các khối 3D.

## Phép toán Boolean: Phương pháp điêu khắc khối 3D cơ bản

Trong hình học không gian, nhà toán học George Boole đã phát minh ra đại số logic, và các phần mềm CAD hiện đại đã ứng dụng nguyên lý này để tạo ra bộ ba **Phép toán [[Boolean]]**:
1. **Phép cộng (Hợp nhất - UNION):** $A \cup B$
2. **Phép trừ (Khấu trừ - SUBTRACT):** $A \setminus B$
3. **Phép nhân (Giao nhau - INTERSECT):** $A \cap B$

Thay vì cố gắng vẽ một khối phức tạp từ một nét vẽ duy nhất, người kỹ sư chuyên nghiệp sẽ chia chi tiết thành các khối hình học sơ khai đơn giản (khối hộp `BOX`, khối trụ `CYLINDER`, khối nón `CONE`), sau đó dùng các phép toán Boolean để ghép nối hoặc đục khoét thành hình thể mong muốn.

![Ba phép toán Boolean trên khối 3D](media/ac-09-05-boolean-operations.svg)

```hotspots
image: media/ac-09-05-boolean-operations.svg
alt: Ba phép toán Boolean trên khối đặc 3D UNION SUBTRACT INTERSECT
layout: central
points:
  - id: spot-1
    x: 18
    y: 35
    title: 1. Hợp nhất (UNION)
    text: "Gộp khối hộp và khối trụ thành một thực thể đặc duy nhất, xóa bỏ vách ngăn bên trong."
  - id: spot-2
    x: 50
    y: 35
    title: 2. Trừ khối (SUBTRACT)
    text: "Chọn vật giữ lại A [Enter], chọn vật khoét lỗ B [Enter] để đục rỗng thể tích."
  - id: spot-3
    x: 82
    y: 35
    title: 3. Lấy phần giao (INTERSECT)
    text: "Chỉ giữ lại phần không gian thể tích chung nhau giữa hai vật thể giao cắt."
```

## Cách dùng từng bước

### 1. Hợp nhất nhiều khối với UNION (Lệnh tắt UNI)
1. Đặt 2 khối 3D (ví dụ một khối hộp `BOX` và một khối trụ `CYLINDER`) dính chạm hoặc lồng một phần vào nhau.
2. Gõ `UNI` hoặc `UNION` rồi nhấn [Enter].
3. Quét chọn cả 2 khối, nhấn [Enter].
4. Hai khối lập tức hàn dính thành một khối đặc duy nhất. Các mặt phẳng giao nhau bên trong ruột được tự động tiêu biến hoàn toàn!

### 2. Khoét lỗ và cắt gọt với SUBTRACT (Lệnh tắt SU)
*QUY TẮC SỐNG CÒN TRONG SUBTRACT:* Phải chọn đúng thứ tự theo 2 bước:
1. Gõ `SU` hoặc `SUBTRACT` rồi nhấn [Enter].
2. **Bước 1 (Chọn vật giữ lại):** Bấm chọn khối lớn cần giữ lại thịt (ví dụ thân khối hộp), nhấn [Enter].
3. **Bước 2 (Chọn vật cắt bỏ):** Bấm chọn khối đóng vai trò là "mũi khoan" (ví dụ khối trụ đâm xuyên), nhấn [Enter].
4. BÙM! Khối trụ biến mất và để lại một lỗ khoan tròn hoàn hảo xuyên suốt qua thân khối hộp!

### 3. Lấy phần thể tích giao nhau với INTERSECT (Lệnh tắt IN)
1. Đặt hai khối giao cắt nhau (ví dụ một hình cầu giao với một hình hộp).
2. Gõ `IN` hoặc `INTERSECT` rồi nhấn [Enter].
3. Quét chọn các khối giao nhau, nhấn [Enter].
4. Toàn bộ các phần thể tích thừa thãi bên ngoài bị cắt bỏ sạch sẽ, chỉ giữ lại duy nhất phần thể tích lõi nằm chung giữa các khối.

## Ứng dụng thực tế: Dựng chi tiết mặt bích có 4 lỗ bu lông

1. Dùng lệnh `CYLINDER` vẽ hình trụ lớn làm thân bích (đường kính 120mm, cao 20mm).
2. Dùng lệnh `CYLINDER` vẽ hình trụ ở tâm làm lỗ trục chính (đường kính 40mm, cao 30mm).
3. Dùng lệnh `CYLINDER` vẽ một trụ nhỏ làm lỗ bu lông (đường kính 12mm, cao 30mm) cách tâm 45mm.
4. Dùng lệnh `ARRAYPOLAR` sao chép trụ nhỏ thành 4 lỗ bu lông phân bố đều 360 độ quanh tâm.
5. Dùng lệnh `SUBTRACT`:
   - Chọn hình trụ lớn (nhấn [Enter]).
   - Quét chọn trụ tâm và 4 trụ nhỏ (nhấn [Enter]).
6. Một mặt bích 4 lỗ bu lông sắc sảo hoàn thành chỉ sau 30 giây!

> [!TIP]
> Nếu bạn vô tình trừ nhầm vật thể trong lệnh `SUBTRACT`, hãy nhấn ngay tổ hợp phím [Ctrl + Z] để quay lại và chọn lại đúng thứ tự vật giữ lại trước, vật trừ sau.

## Tự kiểm tra

```quiz
id: q-ac-09-05-1
type: single
question: "Thứ tự bấm chọn đối tượng CHÍNH XÁC khi thực hiện lệnh khoét lỗ SUBTRACT (SU) là gì?"
options:
  - text: "Chọn vật cần giữ lại [Enter], sau đó chọn vật cần cắt bỏ [Enter]"
    correct: true
    why: "SUBTRACT luôn yêu cầu: Đối tượng gốc (giữ) trước, đối tượng dao cắt (trừ) sau."
  - text: "Chọn vật cần cắt bỏ trước rồi mới chọn vật giữ lại"
    why: "Chọn ngược sẽ khiến phần mềm giữ lại mũi khoan và xóa mất thân máy."
  - text: "Quét chọn tất cả các vật thể cùng một lúc rồi nhấn Enter"
    why: "Quét chọn cùng lúc phần mềm sẽ không hiểu đâu là vật giữ và đâu là vật trừ."
  - text: "Chỉ cần bấm đúp chuột vào màn hình"
    why: "Nhấp đúp chuột không kích hoạt lệnh trừ khối."
explain: "Hãy luôn ghi nhớ khẩu quyết của lệnh SUBTRACT: 'Giữ trước - Trừ sau'."
```

```quiz
id: q-ac-09-05-2
type: single
question: "Phép toán Boolean nào chỉ giữ lại phần thể tích giao nhau chung giữa hai hoặc nhiều khối đặc 3D?"
options:
  - text: "INTERSECT (lệnh tắt IN)"
    correct: true
    why: "INTERSECT lấy phần giao nhau (A ∩ B) của các khối đặc 3D."
  - text: "UNION"
    why: "UNION hợp nhất toàn bộ thể tích lại."
  - text: "SUBTRACT"
    why: "SUBTRACT trừ thể tích."
  - text: "SLICE"
    why: "SLICE dùng mặt phẳng cắt đôi khối vật thể."
explain: "INTERSECT giữ lại vùng không gian giao nhau duy nhất giữa các khối hình học."
```

```quiz
id: q-ac-09-05-3
type: truefalse
question: "Sau khi thực hiện lệnh UNION trên nhiều khối đặc 3D giao nhau, toàn bộ các vách ngăn hình học bên trong ruột sẽ được tự động xóa bỏ để tạo thành một khối liền khối."
answer: true
explain: "UNION tạo ra một khối Solid duy nhất đồng nhất về mặt cấu trúc thể tích và khối lượng."
```

## Lỗi thường gặp

- **Chọn ngược thứ tự trong SUBTRACT:** Muốn khoét lỗ vào hộp nhưng lại chọn hình trụ trước $\to$ Kết quả hộp biến mất, chỉ còn trơ lại cái lõi hình trụ. Khắc phục: Nhấn `Ctrl + Z`, gõ lại `SU`, bấm chọn khối hộp trước rồi nhấn Enter, sau đó mới bấm chọn hình trụ và nhấn Enter.
- **UNION báo lỗi không hợp nhất được:** Do hai khối 3D nằm cách xa nhau không có điểm chạm tiếp xúc nào. Hai khối phải có phần giao hoặc tiếp xúc bề mặt mới Union thành một thể thống nhất được.

## Bài tập thực hành

- [ ] Gõ `BOX`, vẽ một khối hộp kích thước 100 x 100 x 40 mm. <!-- expect: BOX -->
- [ ] Gõ `CYLINDER`, vẽ một hình trụ có tâm ở chính giữa khối hộp, bán kính 25mm, chiều cao 60mm đâm xuyên qua khối hộp. <!-- expect: CYLINDER -->
- [ ] Gõ lệnh `SUBTRACT` (hoặc `SU`), bấm chọn khối hộp [Enter], sau đó bấm chọn khối trụ [Enter] để khoét lỗ tròn xuyên thân hộp. <!-- expect: SUBTRACT -->
- [ ] Gõ `CYLINDER`, vẽ thêm một khối trụ bán kính 15mm cao 30mm đặt trên góc của khối hộp. <!-- expect: CYLINDER -->
- [ ] Gõ lệnh `UNION` (hoặc `UNI`), quét chọn cả hai khối để hợp nhất thành một chi tiết duy nhất. <!-- expect: UNION -->

## Nguồn tham khảo

```links
- title: "Các phép toán Boolean trên Solid 3D từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=Boolean+Operations"
  kind: official
- title: "Lệnh SUBTRACT khoét khối từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=SUBTRACT"
  kind: official
```
