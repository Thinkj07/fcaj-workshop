---
title : "Cài đặt môi trường và Deploy"
date : 2026-07-26
weight : 3
chapter : false
pre : " <b> 5.5.3 </b> "
---

# Cài đặt môi trường và Triển khai ứng dụng (Deploy)

Trong phần này, chúng ta sẽ kết nối vào EC2 Instance nằm ở Private Subnet bằng **AWS Systems Manager Session Manager (SSM)**, tiến hành cài đặt môi trường Node.js, clone mã nguồn Backend dự án Perfume, cấu hình biến môi trường kết nối đến **Amazon RDS** và **Amazon S3**, thực thi lệnh di trú cơ sở dữ liệu (Prisma Migrate & Seed), khởi chạy server backend với **PM2** và kiểm tra khả năng hoạt động qua **Application Load Balancer (ALB)**.

---

### Bước 1: Kết nối vào EC2 Instance qua AWS Systems Manager (SSM)

Vì EC2 instance nằm trong Private Subnet và không gán Public IP, chúng ta sử dụng **SSM Session Manager** để kết nối an toàn mà không cần mở port SSH (22).

1. Truy cập **AWS Management Console** -> chọn **Systems Manager** (hoặc gõ `Session Manager` vào thanh tìm kiếm).
2. Tại menu bên trái, chọn **Session Manager** -> chọn **Start session**.
3. Chọn EC2 instance `MonaPerfume-EC2-PRIVATE-01` -> chọn **Start session**.
4. Trình duyệt sẽ mở một tab terminal làm việc với giao diện lệnh `sh-4.2$`.

Chuyển sang người dùng `ec2-user` và di chuyển về thư mục cá nhân:
```bash
sudo su - ec2-user
cd ~
```

---

### Bước 2: Cài đặt Node.js, Git và PM2

1. Cập nhật danh sách gói hệ thống trên Amazon Linux 2023:
```bash
sudo dnf update -y
```

2. Cài đặt **Git**:
```bash
sudo dnf install git -y
git --version
```

3. Cài đặt **Node.js 22.x** (phiên bản phù hợp với ứng dụng):
```bash
curl -fsSL https://rpm.nodesource.com/setup_22.x | sudo bash -
sudo dnf install -y nodejs
node -v
npm -v
```

4. Cài đặt công cụ quản lý tiến trình **PM2** toàn cục:
```bash
sudo npm install -g pm2
```

---

### Bước 3: Tải mã nguồn Backend và Cài đặt thư viện

1. Clone repository chứa mã nguồn backend cửa hàng nước hoa (Perfume Store):
```bash
git clone <link-repo>
cd web-project/backend
```

2. Tiến hành cài đặt các thư viện phụ thuộc (dependencies):
```bash
npm install
```

---

### Bước 4: Cấu hình biến môi trường (.env)

Tạo tệp `.env` để kết nối ứng dụng với cơ sở dữ liệu **Amazon RDS** và lưu trữ tài nguyên trên **Amazon S3**:

```bash
nano .env
```

Nhập các thông tin cấu hình tương ứng với tài nguyên hạ tầng AWS đã khởi tạo ở các bước trước:

```env
PORT=3000
NODE_ENV=production

# Đường dẫn kết nối Amazon RDS (Database Endpoint từ bước 5.4)
DATABASE_URL="postgresql://postgres:<YourPassword>@monaperfume-rds.c123456789.us-east-1.rds.amazonaws.com:5432/monaperfumedb?schema=public"

# Thông tin Amazon S3 Bucket (từ bước 5.6)
AWS_REGION=us-east-1
S3_BUCKET_NAME=monaperfume-assets-bucket

# Khóa bảo mật ứng dụng
JWT_SECRET="MonaPerfumeSecretKey2026"
```

Lưu và đóng tệp (`Ctrl + O`, `Enter`, `Ctrl + X`).

---

### Bước 5: Thực thi di trú Database và Khởi chạy Backend

1. Tạo cấu trúc bảng và di trú dữ liệu (Prisma Migration):
```bash
npx prisma generate
npx prisma migrate deploy
```

2. Khởi tạo dữ liệu mẫu ban đầu (Seed Database):
```bash
npm run db:seed
```

3. Khởi chạy ứng dụng backend trên cổng `3000` bằng **PM2**:
```bash
pm2 start src/server.js --name "monaperfume-backend"
pm2 save
```

4. Cấu hình **PM2** tự động khởi chạy cùng hệ thống khi EC2 reboot:
```bash
pm2 startup systemd
```

5. Kiểm tra trạng thái ứng dụng:
```bash
pm2 status
curl http://localhost:3000/api/health
```

---

### Bước 6: Kiểm tra kết nối qua Application Load Balancer (ALB)

1. Truy cập **EC2 Console** -> chọn **Target Groups** -> chọn `MonaPerfume-TG`.
2. Chọn tab **Targets** và kiểm tra trạng thái của `MonaPerfume-EC2-PRIVATE-01`. Trạng thái phải hiển thị **Healthy**.
3. Truy cập **EC2 Console** -> chọn **Load Balancers** -> chọn `MonaPerfume-ALB`.
4. Copy tên **DNS name** của ALB (ví dụ: `MonaPerfume-ALB-123456789.us-east-1.elb.amazonaws.com`).
5. Kiểm tra kết nối từ máy local hoặc trình duyệt:
```bash
curl http://MonaPerfume-ALB-123456789.us-east-1.elb.amazonaws.com/api/health
```

---

### Bước 7: Tạo AMI (Amazon Machine Image) để mở rộng EC2 thứ hai

Sau khi EC2 đầu tiên đã cấu hình và deploy thành công:

1. Vào **EC2 Console** -> chọn **Instances** -> nhấp chuột phải vào `MonaPerfume-EC2-PRIVATE-01`.
2. Chọn **Image and templates** -> chọn **Create image**.
3. Đặt tên Image: `MonaPerfume-Backend-AMI` -> chọn **Create image**.
4. Sau khi AMI sẵn sàng, sử dụng AMI này để khởi tạo `MonaPerfume-EC2-PRIVATE-02` ở **Subnet Private 2** (AZ us-east-1b) để hoàn thiện kiến trúc **Multi-AZ High Availability**.
