---
title : "Blog 3"
date : "2026-07-27"
weight : 2
chapter : false
pre : " <b> 3.3. </b> "
---

# AMAZON EVENTBRIDGE LÀ GÌ? XÂY DỰNG ỨNG DỤNG HƯỚNG SỰ KIỆN TRÊN AWS

Amazon EventBridge là một dịch vụ serverless event bus giúp kết nối các ứng dụng với nhau bằng dữ liệu từ các ứng dụng của chính bạn, ứng dụng SaaS (Software-as-a-Service) tích hợp và các dịch vụ AWS khác. EventBridge đơn giản hóa việc xây dựng ứng dụng hướng sự kiện (event-driven application) bằng cách tự động định tuyến các sự kiện từ nguồn đến đích mà không cần quản lý hạ tầng.

![Kiến trúc VPC](/images/5-Workshop/5.3-vpc/vpc_archi2.png)

### Những điểm chính cần biết

- **Kiến trúc Event-Driven**: EventBridge cho phép giải quấn (decouple) các thành phần trong hệ thống, giúp các dịch vụ giao tiếp không đồng bộ thông qua sự kiện (events).
- **Event Buses & Event Pipes**:
  - **Event Bus**: Tiếp nhận và định tuyến các sự kiện đến nhiều mục tiêu (targets) dựa trên các quy tắc (rules) lọc linh hoạt.
  - **EventBridge Pipes**: Kết nối trực tiếp giữa điểm đầu và điểm cuối (point-to-point) từ nguồn sự kiện (như SQS, DynamoDB Streams, Kinesis) đến đích mà không cần viết mã trung gian.
- **EventBridge Scheduler**: Cho phép lập lịch chạy các tác vụ định kỳ hoặc vào một thời điểm cụ thể trong tương lai với độ chính xác cao, hỗ trợ hàng triệu lịch trình đồng thời.
- **Tích hợp phong phú**: Hỗ trợ tích hợp sẵn với hơn 200 dịch vụ AWS và hàng chục đối tác SaaS tên tuổi (Zendesk, Datadog, PagerDuty...).
- **Xử lý và lọc dữ liệu**: Cho phép lọc sự kiện (filtering) và biến đổi cấu trúc dữ liệu (transformation) trực tiếp trước khi gửi đến mục tiêu, giảm bớt công việc cho các dịch vụ tiêu thụ (consumers).

Việc áp dụng EventBridge giúp hệ thống trở nên linh hoạt hơn, dễ dàng mở rộng và bảo trì, đồng thời giảm thiểu tối đa lượng code boilerplate cần viết để kết nối các dịch vụ.

---

### Nguồn tham khảo

- [What is Amazon EventBridge? – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [Amazon EventBridge Features](https://aws.amazon.com/eventbridge/features/)