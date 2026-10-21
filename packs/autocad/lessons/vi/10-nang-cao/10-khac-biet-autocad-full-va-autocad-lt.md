---
id: ac-10-10
title: "Phân biệt AutoCAD Full và AutoCAD LT: Lựa chọn đúng phiên bản"
category: Nâng cao và Tự động hoá
tags: [autocad-lt, autocad-full, so-sanh, ban-quyen, nang-cao]
level: advanced
minutes: 20
needs: [ac-09-01, ac-10-03]
appVersions: ['2024', '2025']
edition: all
---
# Phân biệt AutoCAD Full và AutoCAD LT: Lựa chọn đúng phiên bản

> **Mục tiêu:**
> - Nắm rõ sự khác biệt bản chất giữa phiên bản AutoCAD tiêu chuẩn đầy đủ (**AutoCAD Full**) và phiên bản rút gọn (**AutoCAD LT** - Light).
> - Hiểu rõ các giới hạn về mô hình hoá không gian 3D, khả năng lập trình tự động hóa và các gói công cụ chuyên ngành chuyên sâu (**Specialized Toolsets**).
> - Đưa ra quyết định đầu tư bản quyền chính xác, tối ưu hóa ngân sách tài chính cho cá nhân và văn phòng thiết kế kỹ thuật.

## AutoCAD Full vs AutoCAD LT: Bức tranh tổng quan

Khi tìm hiểu để mua bản quyền hoặc triển khai hệ thống phần mềm cho doanh nghiệp, bạn sẽ luôn bắt gặp hai phiên bản chính của Autodesk: **AutoCAD** (thường gọi là bản Full) và **AutoCAD LT** (viết tắt của *Light* hoặc *Laptop*):

- **AutoCAD LT**: Được thiết kế là giải pháp vẽ và phác thảo kỹ thuật 2D tinh gọn, tập trung tối đa vào tốc độ và chi phí bản quyền hợp lý (thường chỉ bằng khoảng 1/4 đến 1/3 giá của bản Full).
- **AutoCAD Full**: Là nền tảng thiết kế toàn diện, bao gồm cả môi trường dựng hình 3D Solid/Mesh/Surface, khả năng mở rộng lập trình không giới hạn (C#, .NET, ObjectARX, LISP nâng cao) và tích hợp sẵn 7 bộ công cụ chuyên ngành chuyên sâu (Architecture, Electrical, Mechanical, MEP...).

```
┌────────────────────────────────────────────────────────┐
│                      AutoCAD Full                      │
│ ┌──────────────────────────┐ ┌───────────────────────┐ │
│ │  Vẽ & Hiệu chỉnh 2D CAD  │ │ Dựng hình 3D Solid    │ │
│ │  (Toàn bộ tính năng LT)  │ │ Render & Trích xuất   │ │
│ └──────────────────────────┘ └───────────────────────┘ │
│ ┌──────────────────────────┐ ┌───────────────────────┐ │
│ │  7 Toolsets Chuyên ngành │ │ Lập trình .NET, ARX   │ │
│ │  (Kiến trúc, Cơ điện...) │ │ Express Tools, VLIDE  │ │
│ └──────────────────────────┘ └───────────────────────┘ │
└────────────────────────────────────────────────────────┘
                    ▲
                    │ Bản quyền chuyên sâu
┌───────────────────┴────────────────────────────────────┐
│                      AutoCAD LT                        │
│ ┌──────────────────────────┐ ┌───────────────────────┐ │
│ │  Vẽ & Hiệu chỉnh 2D CAD  │ │ Hỗ trợ AutoLISP cơ bản│ │
│ │  (Layer, Dim, Block, Xref)│ │ (Kể từ bản LT 2024)   │ │
│ └──────────────────────────┘ └───────────────────────┘ │
└────────────────────────────────────────────────────────┘
```

## Khác biệt 1: Dựng hình 3D Solid và kết xuất hình ảnh

Đây là ranh giới kỹ thuật lớn nhất giữa hai phiên bản:

- **AutoCAD Full**: Sở hữu đầy đủ không gian làm việc 3D Modeling. Bạn có thể dùng các lệnh tạo khối rắn `EXTRUDE`, `PRESSPULL`, xoay khối `REVOLVE`, thực hiện phép toán cộng trừ khối [[Boolean]], bo tròn cạnh 3D `FILLETEDGE`, trích xuất hình chiếu 2D `FLATSHOT` và kết xuất ảnh chân thực (Render phối cảnh có vật liệu và ánh sáng mặt trời).
- **AutoCAD LT**: Không có không gian làm việc 3D Modeling và không thể tạo hoặc chỉnh sửa khối 3D Solid. Nếu bạn mở một file 3D trên AutoCAD LT, bạn chỉ có thể quan sát, xoay góc nhìn bằng lệnh 3DORBIT và in ấn các góc nhìn đó, chứ không thể sửa đổi hình học của khối rắn.

## Khác biệt 2: Khả năng lập trình và tự động hóa (AutoLISP, API, Express Tools)

Khả năng tự động hóa bằng mã nguồn bên ngoài là thước đo năng suất của người dùng CAD chuyên nghiệp:

- **Bộ công cụ tiện ích Express Tools**: Chỉ có sẵn trên bản AutoCAD Full (bao gồm các lệnh mở rộng cực mạnh như `BURST`, `FLATTEN`, `OVERKILL`, `ALIGNSPACE`...). Bản AutoCAD LT không được tích hợp bộ công cụ này.
- **Hỗ trợ AutoLISP**:
  - *Trước năm 2024*: AutoCAD LT bị khóa hoàn toàn tính năng nạp mã nguồn Lisp.
  - *Từ bản AutoCAD LT 2024 trở đi*: Autodesk đã chính thức mở khóa hỗ trợ [[AutoLISP]] cơ bản cho bản LT (người dùng có thể tải file `.lsp` bằng lệnh `APPLOAD` hoặc gõ biểu thức Lisp trên dòng lệnh). Tuy nhiên, môi trường lập trình Visual LISP Editor (`VLIDE`) và các hàm mở rộng cấp cao phức tạp vẫn chỉ chạy mượt mà nhất trên bản Full.
- **Lập trình cấp cao .NET, C++ (ObjectARX)**: Chỉ duy nhất AutoCAD Full hỗ trợ biên dịch và chạy các ứng dụng plugin mở rộng viết bằng C#, VB.NET hoặc ObjectARX từ các nhà phát triển thứ ba.

## Khác biệt 3: Bản quyền mạng và các bộ công cụ chuyên ngành (Toolsets)

- **Specialized Toolsets**: Khi đăng ký thuê bao AutoCAD Full, người dùng được tặng kèm 7 bộ phần mềm chuyên ngành mạnh mẽ:
  1. *AutoCAD Architecture*: Thư viện tường, cửa, cầu thang kiến trúc thông minh 3D.
  2. *AutoCAD Mechanical*: Thư viện 700.000 chi tiết cơ khí tiêu chuẩn (bulong, đai ốc, bánh răng).
  3. *AutoCAD Electrical*: Thiết kế sơ đồ nguyên lý mạch điện điều khiển và đi dây tủ điện.
  4. *AutoCAD MEP*: Thiết kế hệ thống thông gió HVAC, cấp thoát nước và đường ống kỹ thuật.
  5. *AutoCAD Plant 3D*: Thiết kế đường ống nhà máy công nghiệp hóa chất, dầu khí.
  6. *AutoCAD Map 3D*: Tích hợp dữ liệu GIS địa lý bản đồ.
  7. *AutoCAD Raster Design*: Chuyển đổi và số hóa bản đồ ảnh quét sang đường nét vector.
- Trong khi đó, AutoCAD LT chỉ là phiên bản độc lập duy nhất phục vụ phác thảo bản vẽ 2D tổng quát.

## Bảng so sánh chi tiết tính năng giữa hai phiên bản

| Tiêu chí so sánh | AutoCAD Full | AutoCAD LT |
| :--- | :---: | :---: |
| **Bản vẽ phác thảo 2D** (Line, Circle, Layer, Dim, Xref) | Có đầy đủ | Có đầy đủ |
| **Dựng hình 3D Solid / Mesh / Surface** | Đầy đủ toàn bộ | Không hỗ trợ tạo mới |
| **Kết xuất phối cảnh chân thực (Rendering / Lights)** | Có | Không |
| **Tạo và sửa Dynamic Block** | Có | Có |
| **Liên kết dữ liệu Excel (Data Link)** | Có | Có |
| **Quản trị tập hợp bản vẽ (Sheet Set Manager)** | Có | Có |
| **Nạp và chạy mã AutoLISP (.lsp)** | Toàn diện (kèm VLIDE) | Có (kể từ bản 2024) |
| **Ứng dụng mở rộng C#, .NET, ObjectARX** | Có hỗ trợ | Không hỗ trợ |
| **Bộ công cụ mở rộng Express Tools** | Có sẵn | Không có |
| **7 Gói Toolsets chuyên ngành (Kiến trúc, Điện, Cơ khí...)** | Tích hợp sẵn | Không có |
| **Chi phí bản quyền hàng năm** | Cao hơn (~3x - 4x) | Tiết kiệm, kinh tế |

## Tự kiểm tra

```quiz
id: q-ac-10-10-1
type: single
question: "Điểm khác biệt lớn nhất về mặt hình học giữa AutoCAD Full và AutoCAD LT là gì?"
options:
  - text: "AutoCAD LT không vẽ được đường tròn CIRCLE"
    why: "Cả hai phiên bản đều vẽ được đầy đủ các hình học 2D cơ bản."
  - text: "AutoCAD LT không hỗ trợ các lệnh tạo và chỉnh sửa khối đặc 3D Solid (như EXTRUDE, REVOLVE, UNION)"
    correct: true
    why: "Chính xác. Dựng hình 3D Solid là tính năng độc quyền của bản Full."
  - text: "AutoCAD LT không thể tạo được Layer"
    why: "Cả hai phiên bản đều quản lý hệ thống Layer hoàn toàn giống nhau."
  - text: "AutoCAD LT không thể in bản vẽ ra giấy"
    why: "Cả hai phiên bản đều in ấn xuất sắc ra giấy và PDF."
explain: "AutoCAD LT là phần mềm chuyên biệt cho vẽ kỹ thuật 2D, không tích hợp các công cụ dựng hình và chỉnh sửa mô hình khối 3D Solid như phiên bản AutoCAD Full."
tags: [autocad-lt, 3d-solid, so-sanh]
```

```quiz
id: q-ac-10-10-2
type: single
question: "Kể từ phiên bản AutoCAD LT nào, Autodesk đã chính thức bổ sung khả năng nạp và chạy các tệp mã nguồn AutoLISP (.lsp)?"
options:
  - text: "AutoCAD LT 2010"
    why: "Các bản LT 2010 hoàn toàn bị khóa tính năng AutoLISP."
  - text: "AutoCAD LT 2018"
    why: "AutoCAD LT 2018 chưa có AutoLISP."
  - text: "AutoCAD LT 2021"
    why: "AutoCAD LT 2021 vẫn chưa hỗ trợ AutoLISP."
  - text: "AutoCAD LT 2024"
    correct: true
    why: "Chính xác. Bắt đầu từ bản 2024, người dùng AutoCAD LT có thể chạy các tệp .lsp tiện ích."
explain: "Bước ngoặt lớn diễn ra vào bản phát hành AutoCAD LT 2024 khi Autodesk chính thức mở khóa khả năng chạy mã nguồn AutoLISP cho người dùng phiên bản LT."
tags: [autocad-lt, autolisp, lich-su]
```

```quiz
id: q-ac-10-10-3
type: truefalse
question: "Một bản vẽ DWG chứa mô hình 3D được tạo từ AutoCAD Full vẫn có thể được mở và quan sát, đo đạc hoặc in ấn trên AutoCAD LT."
answer: true
explain: "Đúng. Định dạng tệp DWG là tương thích hoàn toàn giữa hai phiên bản. Người dùng AutoCAD LT vẫn có thể mở bản vẽ 3D để xem góc nhìn, đo kích thước và in ấn bình thường, chỉ không thể chỉnh sửa hình học của khối rắn."
tags: [dwg, tuong-thich, 3d-view]
```

```quiz
id: q-ac-10-10-4
type: multi
question: "Đối tượng người dùng nào sau đây nên ưu tiên lựa chọn bản quyền AutoCAD LT để tối ưu hóa chi phí? (Chọn 2 phương án)"
options:
  - text: "Kỹ sư thiết kế cơ khí chuyên chế tạo khuôn mẫu phức tạp 3D Solid"
    why: "Thiết kế khuôn mẫu 3D bắt buộc phải dùng bản Full hoặc Inventor."
  - text: "Họa viên kiến trúc chuyên triển khai bản vẽ chi tiết kỹ thuật thi công 2D (mặt bằng, mặt đứng, chi tiết cửa)"
    correct: true
    why: "Chính xác. Triển khai hồ sơ 2D là thế mạnh vượt trội của AutoCAD LT."
  - text: "Kỹ sư dự toán và bóc tách khối lượng cần kiểm tra bản vẽ 2D và liên kết bảng tính Excel"
    correct: true
    why: "Chính xác. Đọc bản vẽ và liên kết bảng tính Excel với LT giúp doanh nghiệp tiết kiệm chi phí lớn."
  - text: "Lập trình viên phát triển ứng dụng plugin mở rộng viết bằng ngôn ngữ C# ObjectARX"
    why: "Phát triển ứng dụng C# ObjectARX bắt buộc phải có môi trường AutoCAD Full."
explain: "AutoCAD LT là lựa chọn lý tưởng, tiết kiệm chi phí cho các họa viên triển khai bản vẽ 2D và kỹ sư bóc tách khối lượng vì đáp ứng trọn vẹn 100% nhu cầu công việc với giá bản quyền tối ưu."
tags: [lua-chon, chi-phi, doanh-nghiep]
```

## Hướng dẫn lựa chọn: Khi nào nên mua bản LT, khi nào bắt buộc dùng bản Full?

Để tối ưu chi phí đầu tư phần mềm trong doanh nghiệp:

1. **Nên chọn AutoCAD LT khi**:
   - 100% công việc hàng ngày của bạn là triển khai hồ sơ thiết kế 2D (mặt bằng, mặt đứng, mặt cắt, chi tiết cấu tạo).
   - Bạn chỉ cần các tiện ích Lisp vẽ nhanh thông dụng (trên phiên bản từ 2024 trở lên) mà không cần cài thêm các plugin ngoài viết bằng C# / ObjectARX.
   - Bạn cần trang bị bản quyền số lượng lớn cho đội ngũ họa viên triển khai với ngân sách tiết kiệm nhất.

2. **Bắt buộc phải chọn AutoCAD Full khi**:
   - Bạn cần dựng hình mô hình hóa 3D Solid/Surface, kết xuất hình ảnh phối cảnh kiến trúc hoặc chi tiết máy cơ khí.
   - Bạn cần sử dụng các bộ thư viện chuyên ngành tự động sinh sơ đồ mạch điện (`AutoCAD Electrical`) hoặc bố trí ống thông gió tự động (`AutoCAD MEP`).
   - Doanh nghiệp của bạn phụ thuộc vào các phần mềm plugin chuyên dụng phát triển riêng bằng công nghệ .NET hoặc ObjectARX.

## Bài tập thực hành

- [ ] Tạo bản vẽ mới từ template `acadiso.dwt`. Khởi động hộp thoại tùy chọn hệ thống bằng lệnh `OPTIONS`. <!-- expect: OPTIONS -->
- [ ] Quan sát thẻ **System** trong hộp thoại Options để kiểm tra chế độ đồ họa phần cứng 3D và thông tin phiên bản.
- [ ] Nhấn nút Cancel để đóng hộp thoại Options.
- [ ] Khởi động trình nạp ứng dụng mở rộng bằng lệnh `APPLOAD` để kiểm tra khả năng hỗ trợ mã nguồn AutoLISP trên hệ thống của bạn. <!-- expect: APPLOAD -->
- [ ] Quan sát danh sách các tệp nạp vào bộ nhớ và đóng hộp thoại Load Application.

## Nguồn tham khảo

```links
- title: "So sánh tính năng giữa AutoCAD và AutoCAD LT (Trang chính thức Autodesk)"
  url: "https://www.autodesk.com/products/autocad/compare"
  kind: official
- title: "Khả năng hỗ trợ AutoLISP trên phiên bản AutoCAD LT (Autodesk Docs)"
  url: "https://help.autodesk.com/view/ACDLT/2025/ENU/?guid=GUID-002F642B-BA10-43F4-8149-B943BF2A1F82"
  kind: official
- title: "Hướng dẫn lựa chọn giải pháp CAD phù hợp cho doanh nghiệp (Autodesk)"
  url: "https://www.autodesk.com/solutions/cad-software"
  kind: official
```
