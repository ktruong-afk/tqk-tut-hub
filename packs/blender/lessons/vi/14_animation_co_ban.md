# Bài 14: Nguyên Lý Hoạt Họa Cơ Bản (Keyframe & Action) Cho Nhân Vật Game

> **Danh mục:** Gắn Xương & Hoạt Họa
> **Tags:** animation, keyframe, dopesheet, grapheditor, action, idle, run, walk, unity

---

## 1. Triết Lý Hoạt Họa Cho Game: Vòng Lặp và Hành Động (Action Clips)

Trong khi hoạt họa cho phim điện ảnh diễn ra theo một kịch bản tuyến tính dài từ đầu đến cuối, thì **Hoạt họa cho Game (Game Animation)** lại được thiết kế theo dạng các khối cử động độc lập gọi là **Hành Động (Actions / Animation Clips)**:
* **Idle (Đứng thở chờ lệnh):** Lặp vô tận khi người chơi không bấm phím.
* **Walk / Run Cycle (Vòng lặp bước đi / chạy):** Lặp liên tục theo nhịp chân di chuyển.
* **Attack / Jump / Hurt (Tấn công / Nhảy / Bị thương):** Các cử động đơn lẻ ngắt quãng kích hoạt theo sự kiện nút bấm.

Một hoạt họa game xuất sắc phải đảm bảo tính **Chu kỳ vòng lặp hoàn hảo (Seamless Loop)**: Khung hình kết thúc của hành động phải khớp nối mượt mà 100% với khung hình khởi đầu để nhân vật không bị giật cục khi lặp lại cử động.

```text
       Vòng Lặp Hoạt Họa Khép Kín (Seamless Loop)
  ┌────────────────────────────────────────────────────────┐
  │ Frame 1 (Dáng A) ──→ Frame 15 (Dáng B) ──→ Frame 30    │
  │                                           (Dáng A cũ)  │
  └────────────────────────────────────────────────────────┘
```

---

## 2. Hệ Thống Khung Khóa (Keyframes) Cốt Lõi

Khung khóa (Keyframe) là điểm ghi nhận trạng thái không gian của một hoặc nhiều đoạn xương tại một thời điểm khung hình nhất định trên dòng thời gian:
* **Chèn Keyframe (Phím `[I]`):** Trong Pose Mode, chọn các xương muốn ghi nhận, nhấn phím `[I]`, chọn kênh muốn khóa:
  * *Location (Vị trí):* Thường dùng cho xương trọng tâm `Hips` hoặc xương điều khiển chân IK.
  * *Rotation (Góc xoay):* Kênh quan trọng nhất trong hoạt họa nhân vật (áp dụng cho 90% các khớp cổ, vai, tay, chân).
* **Xóa Keyframe (Tổ hợp `[Alt + I]`):** Xóa dữ liệu khung khóa của xương được chọn tại khung hình hiện tại.
* **Ghi khóa tự động (Auto Keying):** Bấm vào nút tròn màu đỏ cạnh các nút Play trên thanh Timeline. Bất cứ khi nào bạn xoay hay dịch chuyển một khúc xương, Blender sẽ tự động tạo một keyframe ngay tại khung hình đó mà không cần nhấn phím `[I]`.

---

## 3. Bộ Ba Công Cụ Điều Khiển Hoạt Họa trong Blender 5.2

Để làm chủ nhịp điệu (Timing) và gia tốc (Spacing), bạn cần phối hợp ba trình biên tập chuyên dụng:

### 1. Dòng Thời Gian (Timeline)
* **Start:** Đặt khung hình bắt đầu (thường là `1`).
* **End:** Đặt khung hình kết thúc của chu kỳ hành động (ví dụ `30` cho bước đi, `60` cho dáng đứng thở).
* **FPS (Tốc độ khung hình):** Chuẩn game quốc tế thường là **30 FPS** hoặc **60 FPS** (cấu hình trong thẻ *Output Properties*).

### 2. Bảng Ghi Dữ Liệu Hoạt Họa (Dope Sheet)
Hiển thị tổng thể các điểm vàng đại diện cho từng keyframe:
* Nhấn phím `[G]`: Trượt dịch chuyển thời điểm diễn ra keyframe sang trái hoặc phải để điều chỉnh nhịp điệu nhanh chậm.
* Nhấn phím `[S]`: Thu phóng kéo dãn khoảng cách giữa các keyframe để làm chậm lại hoặc tăng tốc độ toàn bộ đòn đánh.

### 3. Trình Biên Tập Đồ Thị (Graph Editor)
Mọi chuyển động trong tự nhiên đều có gia tốc: Nắm đấm vung ra từ từ rồi lao nhanh xé gió, sau đó giật lùi nhẹ do quán tính.
* Graph Editor hiển thị chuyển động dưới dạng các đường cong toán học **Bézier Curves**.
* **Phím `[T]` (Interpolation Mode):** Chọn kiểu chuyển tiếp giữa các keyframe:
  * *Bézier:* Mượt mà tự nhiên, có gia tốc vào (Ease-In) và giảm tốc ra (Ease-Out).
  * *Linear:* Chuyển động đều tăm tắp như robot cơ khí.
  * *Constant:* Đột ngột nhảy góc nhìn (dùng cho hiệu ứng giật khung hoạt hình Stop-motion).

---

## 4. Quản Lý Hoạt Họa Đa Dạng Bằng Action Editor

Để xuất được nhiều đòn đánh và bước chạy khác nhau vào cùng một file `.fbx` sang Unity, bạn phải dùng **Action Editor**:
1. Trong cửa sổ Dope Sheet, bấm vào menu chọn chế độ đổi sang **Action Editor**.
2. Bấm nút **New Action** (hoặc dấu cộng), đặt tên theo quy chuẩn rõ ràng: `Warrior_Idle`, `Warrior_Walk`, `Warrior_Slash`.
3. **BẢO HIỂM CHỐNG MẤT DỮ LIỆU (Fake User):**
   * Bên cạnh tên Action, luôn bấm vào **biểu tượng chiếc khiên (Fake User)**!
   * *Tác dụng sinh tử:* Trong Blender, nếu một Action không được gán trực tiếp vào nhân vật lúc bạn tắt file, Blender sẽ coi đó là "dữ liệu mồ côi" và tự động xóa sạch khi tắt chương trình! Chiếc khiên sẽ lưu giữ hành động đó vĩnh viễn trong file dự án.

---

## 5. Kỹ Thuật Tạo Vòng Lặp Bước Chân / Dáng Đứng Hoàn Hảo

### Ba phím tắt sao chép dáng thần kỳ trong Pose Mode:
* **`[Ctrl + C]` (Copy Pose):** Sao chép toàn bộ góc xoay của các xương đang được chọn.
* **`[Ctrl + V]` (Paste Pose):** Dán nguyên vẹn dáng đã sao chép.
* **`[Ctrl + Shift + V]` (Paste Flipped Pose):** Dán dáng đối xứng sang nửa người bên kia! (Tay trái vung ra trước đổi thành tay phải vung ra trước).

### Công thức vàng tạo vòng lặp 30 frames:
* **Khung hình 1:** Dựng dáng bước chân trái lên trước $\rightarrow$ Nhấn `[A]` chọn tất cả xương, nhấn `[I] > Rotation` $\rightarrow$ Nhấn `[Ctrl + C]` sao chép dáng.
* **Khung hình 30:** Nhảy đến frame 30 $\rightarrow$ Nhấn `[Ctrl + V]` dán đè dáng frame 1 vào $\rightarrow$ Nhấn `[I] > Rotation`. (Đảm bảo điểm đầu và điểm cuối trùng khớp 100%).
* **Khung hình 15 (Chính giữa):** Nhảy đến frame 15 $\rightarrow$ Nhấn `[Ctrl + Shift + V]` để lật ngược dáng chân phải bước lên trước $\rightarrow$ Nhấn `[I] > Rotation`.
* Bấm phím **Spacebar** để phát chuyển động: Một vòng lặp bước đi tự nhiên xuất hiện ngay tức thì!

---

## Bài tập thực hành

**Mục tiêu:** Tạo một hoạt họa đứng thở chờ lệnh (Idle Animation) dài 60 frames hoàn chỉnh cho nhân vật game trong 15 phút.

1. Mở mô hình nhân vật đã được gắn xương và skinning từ Bài 13.
2. Chọn Armature, nhấn `[Ctrl + Tab]` chuyển sang Pose Mode.
3. Đổi cửa sổ Timeline: Đặt `Start = 1`, `End = 60`.
4. Mở cửa sổ Dope Sheet đổi sang **Action Editor**, tạo Action mới đặt tên là `Char_Idle_Loop`, bấm biểu tượng chiếc khiên để bảo vệ.
5. **Frame 1:**
   * Chọn xương `Hips`, nhấn `[R]` nghiêng nhẹ một chút tạo cảm giác tự nhiên.
   * Chọn xương `Chest` (ngực), ngửa nhẹ ra sau một chút như hít vào.
   * Chọn hai xương bắp tay `UpperArm`, khép nhẹ vào sát người.
   * Nhấn `[A]` chọn toàn bộ xương, nhấn `[I] > Rotation`. Nhấn `[Ctrl + C]` sao chép dáng này.
6. **Frame 60:** Nhảy chuột đến frame 60, nhấn `[Ctrl + V]` dán dáng frame 1 vào, nhấn `[I] > Rotation`.
7. **Frame 30 (Đỉnh thở ra):**
   * Nhảy chuột đến frame 30.
   * Chọn xương `Chest`, gập nhẹ về phía trước khoảng 2 độ (thở ra hạ lồng ngực xuống).
   * Chọn xương `Hips`, nhấn `[G] + [Z]` hạ thấp người xuống một khoảng rất nhỏ `0.02m`.
   * Chọn xương đầu `Head`, gật nhẹ xuống theo nhịp thở.
   * Nhấn `[A]` chọn tất cả, nhấn `[I] > Rotation` (và Location cho xương Hips).
8. Nhấn `[Space]` để xem vòng lặp: Nhân vật nhấp nhô lồng ngực đứng thở sống động và mượt mà, sẵn sàng xuất sang Unity!

---

## Nguồn
- https://docs.blender.org/manual/en/5.2/animation/keyframes/index.html
- https://docs.blender.org/manual/en/5.2/editors/dope_sheet/action.html
- https://docs.blender.org/manual/en/5.2/editors/graph_editor/index.html
- Nội dung tham khảo Blender Manual (CC-BY-SA 4.0)
