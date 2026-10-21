# Tutorial Hub

**Hub học tập tương tác** cho phần mềm đồ họa / kỹ thuật: bài học tiếng Việt, bảng tra cứu, và khi cài plugin thì Hub nhìn thấy bạn đang dùng lệnh nào để giải thích ngay và tự đánh dấu bước thực hành.

Kho này chứa **dữ liệu bài học** mà ứng dụng tải về. Ứng dụng nằm ở mục **Releases**.

## Tải về

1. Vào **[Releases](https://github.com/ktruong-afk/tqk-tut-hub/releases/latest)** (cột bên phải của trang kho này, mục *Releases*).
2. Tải file **`TutorialHub-…-portable.exe`** (Windows). Không cần cài đặt.
3. Đặt file vào **một thư mục riêng** (ví dụ `D:\TutorialHub\`) rồi mở. Dữ liệu học của bạn (tiến độ, sổ tay, cài đặt) được lưu trong thư mục `BlenderCompanion-data` nằm cạnh file exe, nên giữ chung một chỗ để không mất khi chuyển máy.

> Lần đầu mở, Windows có thể hiện cảnh báo **"Windows protected your PC"** vì ứng dụng chưa ký số. Bấm **More info** → **Run anyway**.

## Cách dùng

**1. Chọn phần mềm muốn học.** Lần đầu mở, ứng dụng hiện bảng *Chọn phần mềm muốn học* với hai danh sách:
- **Đã tải về máy**: các gói bạn đã có, bấm **Học** để vào.
- **Trên kho GitHub** (có thể tải): bấm **Tải về**, tải xong thẻ tự chuyển lên danh sách trên. Gói ghi **Sắp có** là chưa phát hành.

Gói có nhiều phiên bản phần mềm (ví dụ AutoCAD 2024 / 2025 / 2026): bấm vào thẻ để mở danh sách phiên bản và chọn bản bạn đang dùng.

**2. Học.** Mỗi bài chia thành các mục và bước thực hành. Bấm để đánh dấu mục / bước **đã học**; tiến độ lưu riêng cho từng phần mềm. Có bảng tra phím tắt, hỏi nhanh và nghe đọc bài.

**3. Kết nối với phần mềm (không bắt buộc).** Khi cài plugin cầu nối, Hub biết bạn vừa dùng công cụ / lệnh nào, giải thích nó ngay, và **tự tick bước thực hành** khi bạn làm đúng lệnh. Hub chỉ nghe đúng phần mềm của gói bạn đang học (học Blender thì bỏ qua AutoCAD đang mở, và ngược lại); dòng trạng thái ở thanh trên cho biết đã nối hay đang chờ.
- **Blender:** trong bảng chọn phần mềm, bấm biểu tượng phích cắm trên thẻ Blender để cài plugin.
- **AutoCAD:** plugin đang thử nghiệm, mới thử trên AutoCAD 2027. Sẽ có file riêng trong Releases khi sẵn sàng.

**4. Ủng hộ.** Ứng dụng miễn phí. Nút hình trái tim trên thanh trên có thông tin liên hệ và mã QR ủng hộ (hoàn toàn tự nguyện).

## Gói hiện có

| Phần mềm | Trạng thái |
|---|---|
| Blender | Sẵn sàng, 16 bài |
| AutoCAD | Sẵn sàng, 89 bài (từ cơ bản đến nâng cao, nhiều phiên bản 2024 – 2026) |
| Photoshop | Sắp có |

## Hỏi nhanh

- **Mất mạng thì sao?** Gói đã tải học được bình thường; chỉ cần mạng để tải gói mới hoặc cập nhật.
- **Cập nhật bài mới thế nào?** Mở bảng chọn phần mềm → làm mới → **Cập nhật**. Nội dung mới nạp ngay, không cần tải lại ứng dụng.
- **Dữ liệu ở đâu?** Thư mục `BlenderCompanion-data` cạnh file exe. Xóa thư mục này là xóa sạch tiến độ.
- **Ứng dụng có gửi dữ liệu đi đâu không?** Tiến độ học lưu trên máy bạn, không gửi lên máy chủ nào của chúng tôi. Ứng dụng tải gói từ kho này (kiểm mã sha256 từng file, sai là từ chối). Riêng tính năng **Hỏi AI** là tùy chọn: chỉ khi bạn tự nhập khóa API của dịch vụ AI trong Cài đặt thì nội dung câu hỏi mới được gửi tới dịch vụ đó.

---

# Dành cho người soạn gói

Kho này chứa **gói học** cho từng phần mềm và **gói nhận diện** (brand). Ứng dụng đọc kho qua đường link raw của GitHub, người dùng không cần cài git. Nguồn mặc định: `https://raw.githubusercontent.com/ktruong-afk/tqk-tut-hub/main/`.

```
catalog.json                 # danh mục (tự sinh — đừng sửa tay)
brand/brand.json, logo.svg   # hệ thống nhận diện: tên, logo, font, bảng màu sáng/tối
packs/<id>/pack.src.json     # thông tin gói (sửa tay: tên, mô tả, icon, version, status, app, plugin)
packs/<id>/pack.json         # danh sách file + sha256 (tự sinh)
packs/<id>/lessons/<ngôn ngữ>/*.md   # bài học (vi, en, ...)
packs/<id>/data/*.json       # phím tắt, từ điển công cụ, lỗi thường gặp, mẹo
packs/<id>/plugin/*.zip      # plugin cầu nối cài vào phần mềm đó
```

`catalog.json` và `pack.json` do công cụ dựng sinh ra; công cụ này không nằm trong kho (kho chỉ chứa dữ liệu). Mỗi file có mã sha256 trong `pack.json`, và `.gitattributes` giữ nguyên byte của file (không đổi ký tự xuống dòng) để mã băm không bị sai.

## Cập nhật bài học / thêm phần mềm
1. Sửa bài trong `packs/<id>/lessons/vi/` (hoặc thêm thư mục gói mới, copy `pack.src.json` mẫu).
2. **Tăng `version`** trong `packs/<id>/pack.src.json` (vd 1.0.0 → 1.0.1). Không tăng thì ứng dụng không thấy bản mới.
3. Chạy công cụ dựng để sinh lại `catalog.json` + `pack.json`.
4. Commit và push.

Gói chưa phát hành: `"status": "coming-soon"` → hiện "Sắp có", chưa tải được.

## Đổi nhận diện (logo, màu, font)
Sửa `brand/brand.json` (+ file logo), **tăng `version`**, dựng lại, push. Mọi ứng dụng đọc kho này đổi theo, không cần build lại. Logo không được nhái logo của phần mềm được dạy (Blender, Photoshop...).

## An toàn
Gói chỉ chứa dữ liệu (bài học, JSON, plugin zip), không chứa mã chạy trong ứng dụng. Ứng dụng tải xong kiểm mã sha256, sai thì từ chối và giữ bản đang dùng.
