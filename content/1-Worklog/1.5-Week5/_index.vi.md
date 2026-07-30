---
title: "Worklog Tuần 5"
date: 2026-06-29
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Tiếp cận tư duy Serverless Architecture trên AWS.  
* Làm quen với AWS Lambda cơ bản để làm backend cho API.  
* Khởi tạo và cấu hình các HTTP API / REST API đơn giản qua Amazon API Gateway.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------| ------------ | --------------- | -------------- |
| 2   | - Tìm hiểu mô hình Điện toán Serverless (Không máy chủ) <br> - Tìm hiểu AWS Lambda cơ bản (Triggers, Execution Role, Handlers)| 29/06/2026   | 29/06/2026      |
| 3   | - **Thực hành:** <br>&emsp; + Viết 1 hàm Lambda đơn giản (Node.js/Python) trả về JSON data | 30/06/2026 | 30/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4, 5  | - Tìm hiểu tổng quan Amazon API Gateway: <br>&emsp; + REST API vs HTTP API vs WebSocket API <br>&emsp; + Resources, Methods (GET, POST, PUT, DELETE) <br>&emsp; + Integration Types (Lambda Integration, HTTP Endpoint, AWS Service) | 01/07/2026 | 02/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6, 7   | - **Thực hành:** <br>&emsp; + Tạo REST API mới trên API Gateway Console <br>&emsp; + Tạo Resource /users và Method GET, POST  <br>&emsp; + Tạo Deployment Stage (dev, prod) <br>&emsp; + Kiểm thử API bằng Postman / cURL qua URL Public | 03/07/2026 | 04/07/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 5:

* Hiểu tư duy thiết kế kiến trúc Serverless không cần quản lý máy chủ.
* Viết và triển khai thành công Serverless Function với AWS Lambda.
* Nắm được luồng xử lý cơ bản request/response của Amazon API Gateway.
* Xây dựng và Deploy thành công một hệ thống API endpoints công khai kết nối trực tiếp với AWS Lambda backend.
