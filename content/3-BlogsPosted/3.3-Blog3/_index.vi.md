---
title : "Blog 3"
date : "2026-07-27"
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

# AMAZON EVENTBRIDGE LÀ GÌ? XÂY DỰNG ỨNG DỤNG HƯỚNG SỰ KIỆN TRÊN AWS

Amazon EventBridge là dịch vụ serverless giúp kết nối các thành phần trong ứng dụng với nhau thông qua việc phát sinh và xử lý sự kiện (event). Đây là nền tảng để xây dựng kiến trúc hướng sự kiện (event-driven architecture) — một phong cách thiết kế hệ thống theo hướng "lỏng lẻo" (loosely-coupled), trong đó các thành phần giao tiếp bằng cách phát ra và phản hồi sự kiện thay vì gọi trực tiếp lẫn nhau, giúp hệ thống linh hoạt và dễ mở rộng hơn.

![Blog 3](/images/3-BlogsPosted/3.3-Blog3/image3.png)

### Những điểm chính cần biết

- EventBridge cung cấp hai cơ chế chính để xử lý và chuyển tiếp sự kiện: Event bus và Pipes.
- Event bus hoạt động như một bộ định tuyến, nhận sự kiện từ nhiều nguồn (ứng dụng tự xây dựng, dịch vụ AWS, phần mềm bên thứ ba) và gửi đến nhiều đích khác nhau, có thể biến đổi (transform) dữ liệu trước khi gửi.
- Pipes phù hợp cho tích hợp điểm-tới-điểm (point-to-point): mỗi pipe chỉ nhận sự kiện từ một nguồn duy nhất và gửi tới một đích duy nhất, nhưng hỗ trợ biến đổi và làm giàu (enrichment) dữ liệu ở mức nâng cao hơn.
- Pipes và event bus thường được dùng kết hợp: một pipe có thể nhận dữ liệu từ DynamoDB Stream rồi gửi vào event bus, sau đó event bus tiếp tục phân phối tới nhiều đích theo các rule đã cấu hình.
- Ngoài ra, EventBridge còn có EventBridge Scheduler — một trình lập lịch serverless cho phép tạo, chạy và quản lý tác vụ theo lịch (cron hoặc rate expression) hoặc chạy một lần, kèm khả năng cấu hình cửa sổ thời gian linh hoạt và giới hạn số lần thử lại.

Về bản chất, EventBridge giải quyết bài toán thường gặp khi xây dựng hệ thống microservices: làm sao để các thành phần "biết" về sự kiện xảy ra ở nơi khác mà không cần gọi API trực tiếp lẫn nhau. Thay vì phải viết logic gọi qua lại phức tạp, một dịch vụ chỉ cần phát sự kiện lên event bus, còn các dịch vụ quan tâm sẽ tự đăng ký rule để nhận đúng loại sự kiện mình cần. Cách tiếp cận này giúp thêm hoặc bớt một thành phần trong hệ thống mà không ảnh hưởng tới các phần còn lại — rất phù hợp với các dự án cần khả năng mở rộng và bảo trì dễ dàng theo thời gian.


Link bài trên group: https://www.facebook.com/groups/awsstudygroupfcj/permalink/2229202854511341/?rdid=wj3xkTX7M7viFBap#

---

### Nguồn tham khảo

- [What Is Amazon EventBridge? – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [Amazon EventBridge Event Buses – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-event-bus.html)
- [Amazon EventBridge Pipes – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-pipes.html)