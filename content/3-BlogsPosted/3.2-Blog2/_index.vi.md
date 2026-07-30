---
title : "Blog 2"
date : "2026-07-27"
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---

# LỢI ÍCH CỦA REGIONAL NAT GATEWAY: BẢO MẬT, MỞ RỘNG VÀ TÍCH HỢP IPAM

Ngoài việc đơn giản hóa kiến trúc mạng, Regional NAT Gateway (RNAT) còn mang lại nhiều lợi ích thiết thực về bảo mật, khả năng mở rộng tự động và khả năng tích hợp với các công cụ quản lý IP của AWS.

![Kiến trúc VPC](/images/5-Workshop/5.3-vpc/vpc_archi2.png)

### Những điểm chính cần biết

- Tăng cường bảo mật: vì không cần public subnet để lưu trú NAT Gateway, các tổ chức có yêu cầu bảo mật cao có thể loại bỏ hoàn toàn nguy cơ vô tình triển khai tài nguyên nhạy cảm vào public subnet.
- Chống cạn kiệt cổng (port exhaustion) tự động: mỗi địa chỉ IP gán cho RNAT hỗ trợ tối đa 55.000 kết nối đồng thời tới một đích duy nhất; khi gần đạt ngưỡng, RNAT tự động cấp thêm IP (tối đa 32 IP mỗi AZ).
- Tích hợp với VPC IPAM: RNAT có thể tự động lấy địa chỉ IP từ pool IPAM khi mở rộng sang AZ mới hoặc khi cần mở rộng do lưu lượng tăng, giúp việc cấp phát IP có kiểm soát và dễ dự đoán hơn.
- Kiểm soát thủ công khi cần: người dùng có thể chọn chế độ manual để tự quản lý AZ và EIP thay vì để RNAT tự động hóa hoàn toàn.
- Hỗ trợ giám sát qua CloudWatch: RNAT phát ra các chỉ số (metrics) tương tự NAT Gateway zonal cho từng AZ, cùng các trường log bổ sung như resource-id, az-id để dễ dàng theo dõi.
- Routing linh hoạt: route table của RNAT cho phép chèn thêm AWS Network Firewall hoặc Gateway Load Balancer vào giữa private subnet và NAT Gateway để kiểm tra lưu lượng (traffic inspection) trước khi ra internet.

Việc mở rộng IP diễn ra khá linh hoạt: quá trình tăng thêm IP mất khoảng 5 phút và bắt đầu khi số kết nối đồng thời tới cùng một đích vượt khoảng 40.000; ngược lại, khi số kết nối giảm xuống dưới 20.000 trong khoảng 1 giờ thì hệ thống mới thu hẹp lại. Cơ chế này được thiết kế theo hướng "mở rộng nhanh, thu hẹp chậm", ưu tiên đảm bảo tính sẵn sàng hơn là tiết kiệm tài nguyên ngay lập tức.

---

### Nguồn tham khảo

- [Introducing Amazon VPC Regional NAT Gateway – AWS Blog](https://aws.amazon.com/blogs/networking-and-content-delivery/introducing-amazon-vpc-regional-nat-gateway)
- [Amazon VPC IP Address Manager (IPAM) Documentation](https://docs.aws.amazon.com/vpc/latest/ipam/how-it-works-ipam.html)