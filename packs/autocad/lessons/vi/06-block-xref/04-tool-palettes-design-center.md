---
id: ac-06-04
title: Khai thác kho thư viện với Design Center và Tool Palettes
category: Khối và Tham chiếu
tags: [adcenter, toolpalettes, thu-vien, nang-suat, keo-tha]
level: intermediate
minutes: 20
needs: [ac-06-01]
appVersions: ['2024', '2025']
edition: all
---
# Khai thác kho thư viện với Design Center và Tool Palettes

> **Mục tiêu:**
> - Sử dụng AutoCAD Design Center (`ADCENTER`) để "mượn" Block, Layer, Dimstyle từ bản vẽ khác mà không cần mở file.
> - Thiết lập bảng công cụ kéo thả nhanh Tool Palettes (`TOOLPALETTES` / `Ctrl + 3`).
> - Tạo các tab thư viện tùy biến phục vụ công việc thiết kế chuyên ngành.

## Cơn ác mộng tìm kiếm thư viện và giải pháp

Trong công việc hàng ngày, các kiến trúc sư và kỹ sư thường gặp tình huống:
- Bạn nhớ đã vẽ một cái bồn cầu rất đẹp ở dự án biệt thự năm ngoái, nhưng không muốn mất công mở file đó lên rồi copy-paste.
- Bạn muốn lấy toàn bộ hệ thống Layer và Dimstyle chuẩn từ một file mẫu mà không muốn vẽ lại từ đầu.

AutoCAD cung cấp 2 siêu công cụ khai thác tài nguyên:
1. **AutoCAD DesignCenter ([[DesignCenter]]) (Lệnh tắt `DC` hoặc tổ hợp phím `Ctrl + 2`):** Trình duyệt khám phá bên trong các tệp DWG trên máy tính. Bạn có thể nhìn thấy mọi Block, Layer, Linetype, Dimstyle đang nằm trong bất kỳ file nào và kéo thả trực tiếp vào bản vẽ hiện tại.
2. **Tool Palettes (Lệnh tắt `TP` hoặc tổ hợp phím `Ctrl + 3`):** Bảng công cụ đồ họa trực quan chứa sẵn hàng trăm biểu tượng Block, mẫu Hatch và lệnh vẽ. Bạn chỉ việc bấm giữ chuột và kéo thả chi tiết thẳng vào màn hình làm việc!

## Cách dùng từng bước

### 1. Khai thác tài nguyên với DesignCenter (Ctrl + 2)
1. Nhấn [Ctrl + 2] hoặc gõ lệnh `ADCENTER` (hoặc `DC`) rồi nhấn [Enter].
2. Cây thư mục bên trái cho phép bạn duyệt đến thư mục chứa các tệp DWG trên ổ cứng máy tính.
3. Bấm vào dấu `[+]` bên cạnh một file DWG bất kỳ:
   - Thư mục con sẽ hiện ra: `Blocks`, `Dimstyles`, `Layers`, `Linetypes`, `Textstyles`...
4. Bấm vào mục **Blocks**: Danh sách tất cả các khối hình trong tệp đó sẽ hiện ra dưới dạng biểu tượng thumbnail trực quan ở khung bên phải.
5. Chỉ việc bấm giữ chuột trái vào khối mong muốn và **kéo thả (Drag & Drop)** vào màn hình bản vẽ hiện tại!
6. Bấm vào mục **Layers** hoặc **Dimstyles**, chọn kiểu mong muốn và nhấp chuột phải chọn **Add Layer(s)** để sao chép nguyên vẹn cài đặt sang bản vẽ của bạn.

### 2. Sử dụng và tuỳ biến Tool Palettes (Ctrl + 3)
1. Nhấn [Ctrl + 3] hoặc gõ lệnh `TOOLPALETTES` (hoặc `TP`).
2. Một bảng điều khiển thanh lịch xuất hiện với nhiều thẻ chuyên ngành: *Mechanical*, *Architectural*, *Civil*, *Electrical*...
3. Thử nghiệm: Chuyển sang thẻ *Architectural*, bấm chọn biểu tượng cái cây hoặc cửa sổ, đưa chuột ra ngoài màn hình và bấm để đặt chi tiết. Cực kỳ nhanh chóng!

### 3. Tự tạo thẻ thư viện riêng cho công ty bạn
1. Nhấp chuột phải vào thanh tiêu đề hoặc gáy tab của Tool Palettes > chọn **New Palette**.
2. Đặt tên tab mới: ví dụ `KHO-CUA-DI` hoặc `THIET-BI-CO-DIEN`.
3. Mở DesignCenter ([Ctrl + 2]) duyệt đến tệp DWG chứa các khối block đã chuẩn bị sẵn.
4. Quét chọn hàng loạt các khối block trong DesignCenter, bấm giữ chuột phải và kéo thả thẳng sang tab mới tạo bên Tool Palettes!
5. Toàn bộ các block đã nằm ngăn nắp trong tab riêng, sẵn sàng cho bạn bấm dùng hàng ngày chỉ với 1 cú click!

## Tuỳ chọn và mẹo nâng cao hiệu suất

> [!TIP]
> Trong Tool Palettes, bạn có thể nhấp chuột phải vào từng biểu tượng chi tiết > chọn **Properties**. Tại đây, bạn có thể ép sẵn: Khi chi tiết này được kéo vào bản vẽ, nó sẽ **tự động nằm vào layer quy định** (ví dụ block bàn ghế tự chui vào layer `NOI_THAT`) mà bạn không cần phải chuyển layer thủ công!

> [!TIP]
> Bấm [Ctrl + 2] và [Ctrl + 3] để bật/tắt nhanh các bảng này khi không dùng, giúp mở rộng tối đa không gian vẽ trên màn hình làm việc.

## Tự kiểm tra

```quiz
id: q-ac-06-04-1
type: single
question: "Tổ hợp phím tắt kinh điển để mở nhanh bảng công cụ đồ họa Tool Palettes trong AutoCAD là gì?"
options:
  - text: "Ctrl + 3"
    correct: true
    why: "Ctrl + 3 là phím tắt mặc định mở Tool Palettes."
  - text: "Ctrl + 1"
    correct: false
    why: "Ctrl + 1 mở bảng Properties."
  - text: "Ctrl + 2"
    correct: false
    why: "Ctrl + 2 mở DesignCenter."
  - text: "Ctrl + 9"
    correct: false
    why: "Ctrl + 9 bật tắt Command Line."
explain: "Nhớ bộ phím tắt thần thánh: Ctrl+1 (Properties), Ctrl+2 (DesignCenter), Ctrl+3 (Tool Palettes)."
```

```quiz
id: q-ac-06-04-2
type: single
question: "Ưu điểm vượt trội của DesignCenter (ADCENTER) khi muốn lấy Block từ bản vẽ khác là gì?"
options:
  - text: "Cho phép trích xuất Block, Layer, Dimstyle trực tiếp mà không cần mở tệp DWG đó lên"
    correct: true
    why: "DesignCenter đọc dữ liệu cấu trúc ngầm của file DWG mà không tốn tài nguyên mở tệp đồ họa."
  - text: "Tự động đổi đơn vị bản vẽ sang đơn vị thiên văn"
    correct: false
    why: "DesignCenter giữ nguyên thiết lập hình học chuẩn của đối tượng."
  - text: "Tự động gửi bản vẽ lên mạng xã hội"
    correct: false
    why: "AutoCAD DesignCenter là công cụ quản lý tài nguyên cục bộ."
  - text: "Xóa toàn bộ bản vẽ cũ sau khi sao chép"
    correct: false
    why: "Tệp nguồn hoàn toàn không bị ảnh hưởng hay xóa dữ liệu."
explain: "DesignCenter duyệt nội dung tệp DWG như một thư mục, cho phép kéo thả tài nguyên nhanh gọn nhẹ mà không làm nặng máy tính."
```

```quiz
id: q-ac-06-04-3
type: truefalse
question: "Bạn có thể thiết lập sẵn một layer cố định cho từng biểu tượng trong Tool Palettes để khi kéo ra bản vẽ nó tự động nằm đúng layer đó."
answer: false
explain: "Tính năng này giúp người vẽ kéo cửa, thiết bị, ký hiệu ra màn hình mà không bao giờ lo bị nhầm layer hiện hành."
```

## Lỗi thường gặp

- **Kéo Block từ Tool Palettes ra bị báo lỗi Source drawing not found:** Do tệp DWG gốc chứa định nghĩa block đã bị xóa, đổi tên hoặc di dời sang thư mục khác trên máy tính. Khắc phục: Để các file thư viện CAD vào một thư mục cố định trên ổ đĩa (ví dụ `D:\CAD_LIBRARY\`) và không bao giờ đổi tên thư mục đó.
- **Thư viện Tool Palettes quá nhiều tab gây rối mắt:** Khắc phục: Nhấp chuột phải chọn *Customize Palettes* để gom các tab vào từng nhóm chuyên đề (Palette Groups) như Kiến Trúc, Kết Cấu, Điện Nước.

## Bài tập thực hành

- [ ] Nhấn `Ctrl + 2` hoặc gõ `ADCENTER` để mở giao diện DesignCenter. <!-- expect: ADCENTER -->
- [ ] Duyệt cây thư mục và quan sát cấu trúc các mục con `Blocks`, `Layers`, `Dimstyles` của tệp bản vẽ hiện hành.
- [ ] Nhấn `Ctrl + 3` hoặc gõ `TOOLPALETTES` để mở bảng Tool Palettes. <!-- expect: TOOLPALETTES -->
- [ ] Nhấp chuột phải tạo một Palette mới có tên `THU-VIEN-CA-NHAN`.
- [ ] Vẽ một chi tiết nhỏ bất kỳ và kéo thả vào tab vừa tạo để kiểm tra khả năng lưu trữ.

## Nguồn tham khảo

```links
- title: "Tổng quan AutoCAD DesignCenter từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=ADCENTER"
  kind: official
- title: "Tùy biến Tool Palettes chính thức từ Autodesk"
  url: "https://help.autodesk.com/view/ACD/2024/ENU/?query=TOOLPALETTES"
  kind: official
```
