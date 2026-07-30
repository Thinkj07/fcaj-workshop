---
title: "Worklog Tuần 7"
date: 2026-07-13
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Hiểu tư duy Đóng gói ứng dụng (Containerization) với Docker trong phát triển phần mềm.
* Thành thạo cách đẩy và quản lý Docker Image trên kho lưu trữ AWS ECR (Elastic Container Registry).
* Triển khai ứng dụng Web từ Container lên AWS bằng dịch vụ AWS App Runner đơn giản, tự động.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------| ------------ | --------------- | -------------- |
| 2   | - Tìm hiểu khái niệm Containerization & So sánh Docker với Virtual Machine (EC2) <br> - Viết `Dockerfile` đơn giản để đóng gói một ứng dụng Web (Node.js/Python/React) | 13/07/2026   | 13/07/2026      |
| 3   | - Tìm hiểu dịch vụ AWS ECR (Kho chứa Docker Image) <br> - **Thực hành:** Tạo Repository trên ECR, dùng AWS CLI đăng nhập và push Docker Image lên ECR | 14/07/2026 | 14/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4, 5 | - Tìm hiểu dịch vụ AWS App Runner (Dịch vụ chạy Container tự động dành cho Software Developer không cần quản lý hạ tầng) <br> - **Thực hành:** Cấu hình App Runner pull image từ ECR và tự động Deploy ứng dụng Web ra internet | 15/07/2026 | 16/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6, 7 | - **Thực hành:** Kiểm thử kết nối Public URL của App Runner, cấu hình biến môi trường (Environment Variables) cho Container | 17/07/2026 | 18/07/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 7:

* Đóng gói thành công ứng dụng phần mềm thành Docker Image chuẩn.
* Lưu trữ và quản lý các phiên bản Container Image an toàn trên AWS ECR.
* Triển khai hoàn chỉnh một trang Web Containerized lên môi trường Cloud với AWS App Runner.
