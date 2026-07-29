---
title : "Tạo CloudFront Distribution kết nối S3 Origin"
date : 2026-07-29
weight : 2
chapter : false
pre : " <b> 5.6.2 </b> "
---

Sau khi đã lưu trữ mã nguồn frontend trên Amazon S3, bước tiếp theo là tạo một **Amazon CloudFront Distribution** để phân phối nội dung qua mạng lưới Content Delivery Network (CDN).

AWS đã cập nhật giao diện tạo CloudFront Distribution theo từng bước (Wizard). Dưới đây là hướng dẫn chi tiết theo quy trình giao diện mới.

---

### Bước 1: Choose a plan (Chọn gói dịch vụ)

1. Mở **AWS Management Console**, truy cập dịch vụ **CloudFront**.
2. Chọn nút **Create distribution**.
3. Tại giao diện **Choose a plan**, chọn gói **Free ($0/month)**:
   - Gói này dành cho học tập, thực hành (Usage allowance: **1M requests / 100GB per month**, bao gồm bảo vệ DDoS, SSL/TLS Certificate miễn phí, 5GB S3 storage).

![Giao diện chọn gói CloudFront Free Tier](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-choose-plan.png)

4. Nhấp nút **Next** để tiếp tục.

---

### Bước 2: Get started (Bắt đầu cấu hình)

1. Kiểm tra thông tin tổng quan của Distribution.
2. Đặt tên mô tả cho Distribution (hoặc giữ tên mặc định do AWS gợi ý).
3. Nhấp **Next** để chuyển sang bước tiếp theo.

---

### Bước 3: Specify origin (Khai báo Nguồn dữ liệu & Cấu hình Origin)

1. **Origin domain**: Nhấp vào ô tìm kiếm và chọn S3 Bucket vừa tạo ở bước 5.6.1:
   - Ví dụ: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`
2. **Origin path**: Để trống (nếu file `index.html` nằm tại thư mục gốc của S3).
3. **Origin access**:
   - Chọn **Origin access control settings (recommended)**.
   - Nhấp vào nút **Create new OAC**.
   - Giữ thông tin mặc định (Name: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`, Signing behavior: `Sign requests`) ➔ Nhấp **Create**.

![Cấu hình Origin Domain và OAC](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-specify-origin.png)

4. **Viewer protocol policy**: Chọn **Redirect HTTP to HTTPS** (Tự động chuyển hướng mọi truy cập HTTP sang chuẩn bảo mật HTTPS).
5. **Default root object**: Điền **`index.html`** *(Bắt buộc - Tệp mặc định tải ra khi người dùng truy cập trang chủ)*.
6. Nhấp nút **Next**.

---

### Bước 4: Enable security (Cấu hình Bảo mật)

1. Xem lại thiết lập bảo mật (WAF / DDoS protection đã được tích hợp sẵn trong gói Free).
2. Giữ cấu hình mặc định và chọn **Next**.

---

### Bước 5: Get TLS certificate (Chứng chỉ SSL/TLS)

1. Giữ mặc định sử dụng chứng chỉ SSL/TLS mặc định của CloudFront (`*.cloudfront.net`).
2. Chọn **Next**.

---

### Bước 6: Review and create (Kiểm tra & Khởi tạo)

1. Rà soát lại toàn bộ thông tin cấu hình từ Step 1 đến Step 5.
2. Cuộn xuống cuối trang và nhấp nút **Create distribution**.

![Kiểm tra thông tin và chọn Create Distribution](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-review-create.png)

---

### Bước 7: Cấu hình Custom Error Responses (Tùy chọn cho ứng dụng SPA)

Nếu dự án Perfume là ứng dụng trang đơn (Single Page Application - React/Vue/Angular) có Client-side Routing:

1. Sau khi tạo Distribution thành công, truy cập tab **Custom error responses**.
2. Chọn **Create custom error response**:
   - **HTTP error code**: `403: Forbidden` hoặc `404: Not Found`.
   - **Customize error response**: Chọn **Yes**.
   - **Response page path**: `/index.html`
   - **HTTP response code**: `200: OK`
3. Nhấp **Create custom error response**.

![Cấu hình Custom Error Page](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-error-pages.png)
