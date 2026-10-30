# Shopee AI Video Creator

Công cụ tạo video quảng cáo sản phẩm cho Shopee bằng AI, giao diện tiếng Việt, thiết kế cho người không biết lập trình. Người dùng tải ảnh sản phẩm lên, hệ thống phân tích đặc điểm nhận diện, tạo 10 kịch bản quảng cáo dài 30 giây và dựng thành video MP4 dọc 9:16 với giọng đọc nữ tiếng Việt.

## Trạng thái dự án

- Cập nhật 2026-10-30: đang xây dựng. Ứng dụng chạy trong Muse với tên "Shopee AI Video Creator". Repository này lưu tài liệu dự án, mẫu kịch bản và kết quả kiểm thử.
- Mọi con số về năng lực trong tài liệu này đều là số đã kiểm chứng bằng sản phẩm thật, không phải thông số quảng cáo.

## Tính năng chính

1. Tải ảnh sản phẩm và video tham chiếu lên dự án.
2. Phân tích sản phẩm tự động: đặc điểm nhận diện (Product Identity Lock), lợi ích bán hàng. Thông tin chưa xác minh được ghi rõ là chưa xác minh, không suy diễn, không bịa giá hay thông số.
3. Tạo 10 kịch bản quảng cáo khác nhau, mỗi kịch bản 30 giây (6 cảnh × 5 giây), kèm lời thoại và chữ màn hình cho từng cảnh.
4. Sản xuất video theo từng cảnh bằng khả năng tạo video của Muse: mọi cảnh dùng cùng một ảnh tham chiếu và cùng một khóa sản phẩm để hạn chế biến dạng sản phẩm giữa các cảnh. Cảnh nào tạo lỗi thì chỉ tạo lại cảnh đó.
5. Giọng đọc nữ tiếng Việt: thời lượng từng câu được đo thật trước khi ghép để không bị cắt chữ. Phụ đề và chữ màn hình tiếng Việt có dấu đầy đủ.
6. Ghép các cảnh thành MP4 dọc 9:16 dài 30 giây bằng FFmpeg; file hoàn chỉnh được kiểm chứng bằng cách đo thời lượng hình/tiếng và nhận dạng lại giọng đọc.
7. Xem trước video, tải MP4 xuống, lưu lịch sử dự án để dùng lại.

## Quy trình sử dụng

1. Tạo dự án mới và tải ảnh sản phẩm (có thể kèm video tham chiếu).
2. Xem và chỉnh phần phân tích sản phẩm: đặc điểm nhận diện, lợi ích bán hàng, các mục chưa xác minh.
3. Chọn một trong 10 kịch bản, sửa lời thoại hoặc chữ màn hình nếu cần.
4. Bấm sản xuất: hệ thống tạo từng cảnh, đọc lời thoại, ghép thành video 30 giây.
5. Xem trước, tải MP4 xuống hoặc tạo lại riêng cảnh chưa ưng ý.

## Giới hạn kỹ thuật đã kiểm chứng

- Clip do mô hình video tạo ra có độ phân giải 720×1280 và độ dài khoảng 10 giây; một video 30 giây được ghép từ 3 clip. Thông số 1080p không được hứa hẹn vì mô hình không xuất ra mức đó.
- Tối đa 6 clip được tạo trong một lượt yêu cầu, vì vậy việc sản xuất video thực hiện theo từng kịch bản được chọn, không xuất cả 10 video cùng một lúc.
- Không tồn tại API chính thức của Muse cho quy trình này (đã kiểm tra khi khởi tạo dự án). Công cụ hoạt động như một ứng dụng trong Muse; không dùng API giả lập và không dùng video mẫu thay cho video thật.
- Chưa có công cụ tạo nhạc nền và hiệu ứng âm thanh độc lập: âm thanh nền, nếu dùng, được lấy từ chính clip (chỉ khi clip không chứa tiếng nói lạ) và luôn được thông báo rõ trong báo cáo sản xuất.
- Tiếng nói lạ do mô hình video tự phát sinh trong clip luôn bị tắt; chỉ giọng đọc theo kịch bản được giữ lại.

## Định dạng kịch bản

Mỗi kịch bản dùng một khối khóa sản phẩm dùng chung (GLOBAL VISUAL CONSISTENCY + PRODUCT IDENTITY LOCK) và các cảnh theo mẫu:

```text
CẢNH 1 (0–5s)
Hình ảnh: <mô tả cảnh>
Lời thoại: <câu thoại tiếng Việt>
Chữ màn hình: <dòng chữ hiển thị>
```

Khóa sản phẩm mô tả cố định: hình dáng, màu sắc, các chi tiết nhận diện không được thay đổi, vật liệu và kích thước (chỉ khi đã xác minh), cùng danh sách cấm (không thêm nút bấm, không đổi màu, không nhân đôi sản phẩm, không cơ chế điện nếu sản phẩm là cơ khí).

## Tham khảo và giấy phép

- Quy trình làm việc tham khảo 26Flow — https://github.com/bynne2602/museflow (giấy phép GNU GPL v2). Dự án này viết mã và tài liệu mới hoàn toàn theo hướng clean-room: không sao chép mã nguồn GPL, không sửa và không ghi đè repository gốc.
- Giấy phép của chính dự án này: chủ sở hữu sẽ quyết định và bổ sung file LICENSE sau.

## Cấu trúc repository

- `README.md` — tài liệu bạn đang đọc.
- `docs/` — hướng dẫn sử dụng chi tiết và mẫu kịch bản (đang bổ sung).
- Ứng dụng chạy trong Muse; repository này là nơi lưu trữ tài liệu và lịch sử kiểm thử của dự án.
