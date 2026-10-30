# Cuios · Bản hoạt động tốt + 94 ghi chú

Bản **4.0.1** kế thừa đúng [commit 696fe10](https://github.com/Cuongqtx11/locket_cuios_stable/tree/696fe103b34aae9ad41ed920685deb8a7808997f) mà người dùng xác nhận có đầy đủ chức năng sau khi cài lại. Chỉ đổi danh mục ghi chú và nhãn phiên bản; luồng xử lý Gold, mic/âm thanh, video, cache, asset và khung Aura giữ nguyên theo bản đó.

Cấu hình vẫn là **60s/100 MiB** như bản được xác nhận. Người dùng báo **video từ thư viện vẫn chỉ đăng được 10s**; bản này không thay đổi giới hạn đó và không khẳng định server chấp nhận video dài một phút hoặc file 100 MiB.

## Hai repo được giữ

| Repo | Nội dung |
| --- | --- |
| [locket_cuios_stable](https://github.com/Cuongqtx11/locket_cuios_stable) | Engine từ 696fe10, bộ 94 ghi chú mới |
| [locket_cuios_10s_6mb](https://github.com/Cuongqtx11/locket_cuios_10s_6mb) | Bản v4.1.0 riêng: mục tiêu quay 60s, nhập 10s/6 MiB, runtime được giữ nguyên |

Các link ghim commit `696fe10` và `4b3ebce` trong repo này vẫn giữ nội dung cũ. Artifact JS đã phát hành được giữ để các module đó tiếp tục tải đúng file. Nội dung ghi chú mới nằm ở bản 4.0.1, không sửa đè link cũ.

## Cài bộ 94 ghi chú

Chỉ bật một module Locket trong cấu hình Shadowrocket đang dùng:

```text
https://raw.githubusercontent.com/Cuongqtx11/locket_cuios_stable/main/locket_cuios_stable.sgmodule
```

Bật HTTPS Decryption/MITM và chứng chỉ CA đã tin cậy; kết nối Shadowrocket trước khi mở Locket. Module chính dùng đúng tham số `aura-frame` của bản được xác nhận. Tất cả rule dùng cùng runtime mới có hash trong tên. Bản `locket_cuios_no_widget.sgmodule` chỉ giữ khung server như nhánh cũ, không cài chồng.

## Ghi chú đã đổi

- Dòng đầu: **t.me/tomqtx1111**. Ba mẫu thương hiệu còn lại giữ **Bản quyền Cuios**, **Cưn🍤**, **tom11th5**.
- Bỏ toàn bộ nhóm **Dịu dàng** gồm 10 mẫu.
- Thêm **50 câu mới**: 20 trêu đùa, 15 hài hước, 5 bạn bè, 5 đời thường và 5 tự tin/yêu đời.
- Tổng **94 mẫu**, ưu tiên nhóm Trêu đùa và Hài hước ngay sau thương hiệu. Những nhóm Tình yêu, Vui vẻ, Cảm xúc vẫn có mặt.
- Giữ cấu trúc caption, đăng ký ID, nền ảnh/màu và renderer của engine được xác nhận. Nhóm mới dùng lại các nền có sẵn; không thay URL hoặc dữ liệu PNG của nền và khung widget.

Một số câu mới: “Nhìn gì, thích tớ à?”, “Ảnh miễn phí, nhớ tớ tính tiền”, “Ví mỏng, tâm hồn phú hộ”, “Dậy rồi, hồn chưa tới”, “Bạn thân, nghiệp ai nấy giữ”.

![94 mẫu ghi chú](assets/captions-preview.jpg)

Chỉ thay danh sách trong picker; các ghi chú đã đăng không bị sửa. Việc hiển thị bản mới vẫn phụ thuộc app fetch/activate cấu hình; không cần tiếp tục gỡ app nếu bản hiện tại đã hoạt động tốt.

## Kiểm tra và dựng lại

```bash
python3 tools/build_script.py
python3 tools/build_modules.py
npm run check
npm test
```

**41 test offline**: giữ các kiểm tra media, mic flags, cache/ETag, RevenueCat/Firebase, schema và báo cáo của v4.0; cập nhật kiểm tra danh mục 94 mẫu. Một kiểm tra đối chiếu toàn bộ JS xác nhận ngoài catalogue và nhãn phiên bản/số lượng, engine giống từng byte với runtime v4.0.0 đã được giữ lại.

Kiểm thử mã không thay thế xác nhận các chức năng trên iPhone; nhận định hoạt động tốt của bản gốc dựa trên báo cáo người dùng. Các tài liệu v4.0/v4.1 trong `docs` là phân tích lịch sử. Repo 10s/6 MiB chứa bản 4.1.0 đầy đủ riêng.

Muốn dựng lại ảnh xem trước mà không thay PNG nền/khung:

```bash
python3 tools/build_artwork.py --preview-only
```

Artwork chỉ cần Pillow ở bước authoring. Runtime không có dependency hoặc request ra ngoài; danh mục được nhúng trong file JS. Mã kế thừa theo MIT.
