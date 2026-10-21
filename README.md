# Kho gói học Companion

Kho này chứa **gói học** cho từng phần mềm và **gói nhận diện** (brand). App vỏ "Companion" đọc kho qua đường link raw của GitHub — người dùng không cần cài git.

```
catalog.json                 # danh mục (tự sinh — đừng sửa tay)
brand/brand.json, logo.svg   # hệ thống nhận diện: tên, logo, font, bảng màu sáng/tối
packs/<id>/pack.src.json     # thông tin gói (sửa tay: tên, mô tả, icon, version, status, app, plugin)
packs/<id>/pack.json         # danh sách file + sha256 (tự sinh)
packs/<id>/lessons/<ngôn ngữ>/*.md   # bài học (vi, en, ...)
packs/<id>/data/*.json       # phím tắt, từ điển công cụ, lỗi thường gặp, mẹo
packs/<id>/plugin/*.zip      # plugin cầu nối cài vào phần mềm đó
tools/build-registry.js      # sinh lại catalog.json + pack.json
```

## Đưa lên GitHub lần đầu
1. Tạo repo trên GitHub (vd `companion-packs`, để Public — app tải không cần đăng nhập).
2. Trong thư mục này:
   ```
   git init
   git add -A
   git commit -m "Kho gói học đầu tiên"
   git branch -M main
   git remote add origin https://github.com/<tài khoản>/companion-packs.git
   git push -u origin main
   ```
3. Link nguồn cho app: `https://raw.githubusercontent.com/<tài khoản>/companion-packs/main/`
   - Đặt trong app: nút **Phần mềm đang học** → biểu tượng GitHub → dán link → Lưu.
   - Hoặc đặt mặc định cho bản build: `companion_app/package.json` → `"companionRegistry": "<link>"`.

## Cập nhật bài học / thêm phần mềm
1. Sửa bài trong `packs/<id>/lessons/vi/` (hoặc thêm thư mục gói mới, copy `pack.src.json` mẫu).
2. **Tăng `version`** trong `packs/<id>/pack.src.json` (vd 1.0.0 → 1.0.1). Không tăng thì app không thấy bản mới.
3. `node tools/build-registry.js`
4. `git add -A && git commit -m "Cập nhật bài Blender" && git push`

App người dùng: bấm **Phần mềm đang học** → làm mới → **Cập nhật** → nội dung mới nạp ngay, không cần mở lại app. (Mở app cũng tự kiểm tra; có bản mới thì nút hiện chấm đỏ.)

Gói chưa phát hành: `"status": "coming-soon"` → hiện "Sắp có", chưa tải được.

## Đổi nhận diện (logo, màu, font)
Sửa `brand/brand.json` (+ file logo), **tăng `version`**, chạy `node tools/build-registry.js`, push. Mọi app đọc kho này đổi theo, không cần build lại app. Trang hướng dẫn nhận diện `brand/guidelines.html` tự sinh lại từ brand.json (kèm kiểm tra độ tương phản màu).
Lưu ý thương hiệu: logo không được nhái logo của phần mềm được dạy (Blender, Photoshop...).

## An toàn
Mỗi file có mã sha256 trong `pack.json`; app tải xong kiểm mã, sai là từ chối và giữ bản đang dùng. Gói chỉ chứa dữ liệu (bài học, JSON, plugin zip), không chứa code chạy trong app.
