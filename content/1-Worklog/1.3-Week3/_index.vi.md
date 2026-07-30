---
title: "Worklog Tuần 3"
date: 2026-06-15
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Biết cách dùng S3 để lưu trữ và chạy một trang web tĩnh (Static Website).
* Quản lý các phiên bản của file bằng tính năng S3 Versioning.
* Đặt quy tắc tự động xóa hoặc lưu trữ file cũ (Lifecycle Rules).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------| ------------ | --------------- | -------------- |
| 2   | - Tìm hiểu tính năng Static Website Hosting trên Amazon S3 | 15/06/2026   | 15/06/2026      |
| 3   | - Thực hành: Tải một file index.html đơn giản lên S3 và bật tính năng Hosting để chạy web trên trình duyệt | 16/06/2026 | 16/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tìm hiểu tính năng S3 Versioning (Lưu lại phiên bản cũ khi ghi đè file) | 17/06/2026 | 17/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Thực hành: Bật Versioning, chỉnh sửa file HTML, khôi phục lại phiên bản file cũ | 18/06/2026 | 18/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Tìm hiểu & Thực hành tạo Lifecycle Rule: Tự động chuyển file cũ sang S3 Glacier hoặc tự xóa sau 30 ngày | 19/06/2026 | 19/06/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 3:

* Đã tự xuất bản thành công một trang web HTML tĩnh chạy trực tiếp từ S3.
* Biết cách bảo vệ file chống ghi đè/xóa nhầm bằng S3 Versioning.
* Đã thiết lập được quy tắc dọn dẹp dữ liệu tự động giúp tiết kiệm chi phí.
