---
title: "Worklog Tuần 4"
date: 2026-06-22
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Tìm hiểu tổng quan dịch vụ CSDL trên AWS (Relational vs Non-Relational).
* Khởi tạo, cấu hình mạng và kết nối thành công tới Amazon RDS (MySQL/PostgreSQL).
* Hiểu kiến trúc Multi-AZ giúp tối ưu tính sẵn sàng cao (High Availability).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------| ------------ | --------------- | -------------- |
| 2   | - Tổng quan về CSDL trên AWS: Amazon RDS, Aurora, DynamoDB <br> - So sánh Tự cài CSDL trên EC2 vs Sử dụng Amazon RDS | 22/06/2026   | 22/06/2026 |
| 3, 4   | - Tìm hiểu Kiến trúc RDS: <br>&emsp; + DB Instance Engines (MySQL, PostgreSQL) <br>&emsp; + DB Subnet Groups & VPC Setup <br>&emsp; + Security Groups cho Database  | 23/06/2026 | 24/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - **Thực hành**: <br>&emsp; + Tạo DB Subnet Group trong VPC <br>&emsp; + Khởi tạo 1 RDS MySQL Instance | 25/06/2026 | 25/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Tìm hiểu khái niệm Multi-AZ Deployment (Synchronous replication, Failover) <br> - **Thực hành:** <br>&emsp; + Dùng DBeaver/MySQL Workbench kết nối vào RDS | 26/06/2026 | 26/06/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 4:

* Biết khi nào nên dùng CSDL quan hệ (RDS) và phi quan hệ (DynamoDB).
* Khởi tạo thành công Amazon RDS MySQL instance đạt chuẩn cấu hình mạng riêng tư trong VPC.
* Hiểu nguyên lý hoạt động của Multi-AZ phục vụ cho bài toán khắc phục sự cố (Failover).
