# Cuios · Thử nghiệm Locket Looks

## Căn cứ

[Google Cloud giới thiệu Locket Looks](https://cloud.google.com/customers/locket): người dùng có thể dùng AI thêm kiểu tóc, trang phục và hiệu ứng vui vào selfie. Bài viết xác nhận Locket dùng Nano Banana 2 Lite để xử lý ảnh. [Locket công bố hợp tác trên trang công ty](https://www.linkedin.com/company/locket-labs-inc), đề cập triển khai tới người dùng trẻ tại Mỹ; thông tin này không xác nhận tài khoản/khu vực khác đã được cấp tính năng.

Tên `camera_filter_config` và ba field bên dưới được đối chiếu trong các triển khai cấu hình công khai. Đây là bằng chứng về cách triển khai của cộng đồng, **không phải tài liệu API hay bản chụp cấu hình từ iPhone của người dùng**. Phần thử nghiệm chỉ dùng tên field, không sao chép catalogue hay các thay đổi khác từ những triển khai đó. Hiệu lực trên bản App Store hiện tại cần được thử thực tế.

## Cấu hình thử

| Entry | Field | Giá trị |
| --- | --- | --- |
| `camera_filter_config` | `show_filter_button` | `true` (boolean trong JSON lồng) |
| `camera_filter_config` | `sheet_enabled` | `true` |
| `camera_filter_config` | `allows_custom_filters` | `true` |

Giữ nguyên mọi field khác, gồm `sheet_filters`, `picker_filters`, thiết lập tự mở bảng, giới hạn, model, endpoint và bộ lọc an toàn nếu server cung cấp. Không tự thêm ID filter, prompt, model hoặc cờ AI phỏng đoán. Nếu entry thiếu, chỉ bổ sung object ba cờ; khi đó chưa có bằng chứng app có catalogue để hiển thị. Nếu entry có schema lạ hoặc JSON lỗi, giữ nguyên giá trị và báo `skipped_schema`.

Các cờ giao diện không tạo quyền xử lý ảnh trên server. Có nút Looks nhưng không dựng được ảnh vẫn có thể do quyền tài khoản, rollout hoặc schema/client; chưa đủ bằng chứng kết luận nguyên nhân. Module không sửa request/response tạo ảnh, không giả kết quả AI, không gọi dịch vụ AI bên ngoài và không tắt bộ lọc an toàn.

## Thử bằng Shadowrocket

1. Thêm [module Looks Protected P1](https://raw.githubusercontent.com/Cuios-shop/locket_cuios_stable/main/locket_cuios_looks_protected.sgmodule). Có thể dùng [bản JS thường](https://raw.githubusercontent.com/Cuios-shop/locket_cuios_stable/main/locket_cuios_looks.sgmodule) để kiểm tra tương thích. Chỉ bật một module Locket.
2. Dùng cấu hình HTTPS Decryption/CA đã hoạt động. Kết nối Shadowrocket trước khi mở lại Locket. Đổi module không đảm bảo app đã fetch và activate cấu hình.
3. Mở camera/chụp ảnh và tìm mục filter/Looks. Việc tạo ảnh, nếu xuất hiện, dùng luồng xử lý của chính Locket.
4. Mở `http://cuios-status.invalid/status` rồi xem báo cáo JSON, phần `observed.firebase.looks`.

`configuration_patched` chỉ xác nhận script đã sửa cấu hình gửi về app. `serverConfigPresent`, `sheetGroups`, `pickerFilters`, `inputFlags` giúp biết đầu vào có cấu hình/danh sách và cờ đang bật hay tắt. Không lưu nội dung prompt, ảnh, ID filter, model, URL hay tài khoản. `generationVerified` luôn là `false` vì script không thể quan sát và chứng minh kết quả tạo ảnh. Xem thêm thời điểm và action của Firebase; dữ liệu chẩn đoán là quan sát đã lưu, không phải trạng thái trực tiếp của app.

Nếu không có fetch Firebase mới hoặc không xuất hiện Looks, cần kiểm tra log/báo cáo trước khi chỉnh tiếp. Không cần xóa dữ liệu hay cài lại app để thử bản module này. Để quay về, tắt module Looks và bật lại module đang dùng trước đó; Locket vẫn cần fetch/activate lại để cập nhật cấu hình đã lưu.

## Phạm vi phát hành

Hai file thử mới nằm ngay trong repo `Cuios-shop/locket_cuios_stable`, không tạo thêm repo. `argument=looks-aura-frame` chỉ gắn trên hook response Firebase hiện có. Module thông thường không bật Looks. Media 60s/100 MiB, 94 ghi chú với 90 nền và bốn mẫu bản quyền, khung Aura cùng phạm vi URL giữ nguyên. Giới hạn upload thực tế vẫn phải kiểm tra trong app.

Kiểm thử offline chạy cả runtime thường và Protected: bảo toàn catalogue và safety, bỏ qua schema lỗi, đúng phạm vi request, validator ổn định và chỉ khác ba field filter khi so với module Aura thông thường. Chưa kiểm chứng trên iPhone và chưa xác nhận dịch vụ AI chấp nhận tài khoản.
