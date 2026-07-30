---
title: "Worklog Tuần 8"
date: 2026-07-20
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Quản lý thông tin cấu hình nhạy cảm (API Keys, DB Credentials) an toàn bằng AWS Systems Manager Parameter Store.
* Nắm tư duy và luồng hoạt động của tích hợp/triển khai tự động (CI/CD).
* Tự động hóa quá trình Deploy code/máy chủ khi có thay đổi trên Repository (GitHub Actions / AWS CodePipeline).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------| ------------ | --------------- | -------------- |
| 2   | - Tìm hiểu rủi ro khi hardcode bí mật (Secrets/API Keys) trong nguồn mã nguồn <br> - Tìm hiểu dịch vụ AWS Systems Manager (SSM) Parameter Store | 20/07/2026   | 20/07/2026      |
| 3   | - **Thực hành:** Lưu trữ tham số (SecureString) trên Parameter Store và truy xuất trực tiếp từ ứng dụng/Lambda bằng SDK | 21/07/2026 | 21/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4, 5 | - Tìm hiểu tổng quan về CI/CD Pipeline trong dự án phần mềm <br> - **Thực hành:** Thiết lập Workflow đơn giản với GitHub Actions (hoặc AWS CodePipeline) để tự động kiểm thử và deploy mã nguồn lên S3 / App Runner mỗi khi `git push` | 22/07/2026 | 23/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6, 7 | - **Thực hành:** Thử nghiệm thay đổi code, kiểm tra quá trình tự động Build & Deploy, kiểm tra nhật ký lỗi (Build Logs) | 24/07/2026 | 25/08/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 8:

* Tách biệt hoàn toàn thông tin bảo mật và cấu hình ra khỏi source code bằng SSM Parameter Store.
* Hiểu sâu luồng chuyển giao phần mềm tự động trong thực tế (CI/CD).
* Xây dựng thành công quy trình tự động cập nhật ứng dụng Cloud ngay khi lập trình viên đẩy code mới.