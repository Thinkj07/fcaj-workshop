---
title : "Tạo Auto Scaling Group và Application Balancer"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

Trong phần này, ta sẽ tạo Auto Scaling Group và Application Balancer

---
### Tạo Target group
 **EC2 -> Target groups -> Create target group**

 1. **Create target group**
 - Settings - immutable

| Trường                    | Giá trị                        |
| ------------------------- | ------------------------------ |
| **Target group name**                   | `MonaPerfume-TG`               |
| **Protocol**                | HTTP     |
| **Port** | 3000                         |
| **IP address type**              | IPv4 |
| **VPC**        | MonaPerfume-VPC            |

![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg1.png)

- Health checks
| Trường                    | Giá trị                        |
| ------------------------- | ------------------------------ |
| **Health check protocol**                   | HTTP               |
| **Health check path**                | / (nếu trong backend có mục healthcheck thì thay vào, không thì giữ nguyên)     |

![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg2.png)

- Advanced health check settings
| Trường                    | Giá trị                        |
| ------------------------- | ------------------------------ |
| **Interval**                   | 10               |

2. Register targets - recommended
- Available instances (2)

Click chọn 2 instance ta đã tạo với port **3000** và **Includes as pending below**
Nhấn **Next** và **Create target group**

![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg3.png)
![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg4.png)


### Tạo Application Load Balancer
 **EC2 -> Load balancers -> Create load balancer**
1. Chọn Application Load Balancer
![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb1.png)
![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb2.png)
![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb3.png)
![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb4.png)
![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb5.png)
![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb6.png)

