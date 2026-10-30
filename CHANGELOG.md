# Thay đổi

## 4.0.1 — nhánh ghi chú từ bản 696fe10 được xác nhận

- Dùng lại nguyên engine v4.0.0; chỉ catalogue và nhãn phiên bản/số lượng đổi. Không kế thừa thay đổi media của 4.1.0.
- Bỏ 10 mẫu Dịu dàng, thêm 50 mẫu (35 trêu đùa/hài hước), tổng 94 mẫu. Dòng đầu t.me/tomqtx1111.
- Giữ nền/khung/asset và tham số aura-frame; không sửa đè runtime đã phát hành.
- 41 test, có đối chiếu engine nguyên vẹn. Video thư viện 60s chưa được xác nhận; người dùng báo trần đăng thực tế 10s.
- Bản 4.1.0 được lưu riêng ở repo locket_cuios_10s_6mb.


## 4.1.0 — quay 60s, nhập 10s/6 MiB

- Tách ngữ cảnh recording/upload/trim và trần byte nhập; giữ kiểu dữ liệu, đơn vị, codec và trường chưa rõ nghĩa.
- Xử lý audio.enabled trong các nhánh media lồng nhau; chưa xác minh mic native.
- Giữ renderer server cho ghi chú; 54 mẫu nền gradient mặc định, giữ khung widget gốc.
- Trang status/report qua HTTPS host thật, tên/kiểu cờ media root và kho chẩn đoán tách version.
- Module mới locket60s_10s_6mb.sgmodule, runtime hash mới, giữ artifact v4.0.0. 44 test offline; chưa kiểm thử chức năng trên iPhone.


## 4.0.0 — profile thống nhất, chẩn đoán và xử lý revision

- Nhận diện bundle ID, thêm host dự phòng RevenueCat chính thức, chẩn đoán route chưa hỗ trợ.
- ETag theo nội dung Firebase đã sửa, giữ metadata và state UPDATE; không tạo/replay cấu hình thiếu entries.
- Một runtime có tên chứa hash cho toàn bộ rule; một profile 60s/100 MiB/54 ghi chú và một variant giữ khung server.
- Trang trạng thái/report cục bộ, lưu riêng từng service; redaction, lỗi storage và freshness rõ ràng.
- Giữ nội dung mic/media/54 ghi chú/nền/khung của nhánh trước; 39 kiểm thử offline.
- Chưa xác nhận ổn định trên iPhone. Cần báo cáo từ thiết bị để xác định lỗi thực tế còn lại.

Các repo nguồn giữ nguyên. Tên repo stable không phải chứng nhận mọi chức năng native đã hoạt động.
