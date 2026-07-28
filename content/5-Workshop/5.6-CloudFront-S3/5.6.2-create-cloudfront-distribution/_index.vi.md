---
title : "Tạo CloudFront Distribution kết nối S3 Origin"
date : 2026-07-28
weight : 2
chapter : false
pre : " <b> 5.6.2 </b> "
---

Sau khi đã lưu trữ mã nguồn frontend trên Amazon S3, bước tiếp theo là tạo một **Amazon CloudFront Distribution** để phân phối nội dung qua mạng lưới Content Delivery Network (CDN).

---

### Bước 1: Khởi tạo CloudFront Distribution

1. Mở **AWS Management Console**, truy cập dịch vụ **CloudFront**.
2. Chọn nút **Create distribution**.

![Tạo CloudFront Distribution](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-create.png)

---

### Bước 2: Cấu hình Origin Settings

1. **Origin domain**: Nhấp vào ô tìm kiếm và chọn S3 Bucket vừa tạo ở bước trước:
   - Ví dụ: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`
2. **Origin path**: Để trống (nếu file `index.html` nằm tại thư mục gốc S3).
3. **Name**: AWS sẽ tự động điền tên origin (ví dụ: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`).
4. **Origin access**:
   - Chọn tùy chọn **Origin access control settings (recommended)**.
   - Nhấp vào nút **Create new OAC**.
   - Bảng điều khiển hiện ra với thông tin mặc định (Name: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`, Origin type: `S3`, Signing behavior: `Sign requests`).
   - Chọn **Create**.

![Cấu hình Origin & OAC](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-origin-oac.png)

---

### Bước 3: Cấu hình Default Cache Behavior

1. **Viewer protocol policy**: Chọn **Redirect HTTP to HTTPS** (Tự động chuyển hướng truy cập HTTP thường sang chuẩn bảo mật HTTPS).
2. **Allowed HTTP methods**: Chọn **GET, HEAD** (Phù hợp cho trang web tĩnh).
3. **Restrict viewer access**: Chọn **No**.
4. **Cache key and origin requests**: Chọn **CachingOptimized (recommended)**.

![Default Cache Behavior](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-behavior.png)

---

### Bước 4: Cấu hình Web Application Firewall (WAF) & Settings

1. **Web Application Firewall (WAF)**: Chọn **Do not enable security protections** (để tiết kiệm chi phí cho bài workshop lab).
2. **Price class**: Chọn **Use all edge locations (best performance)** hoặc **Use only North America and Europe**.
3. **Alternate domain name (CNAME)**: Để trống (hoặc điền tên miền tùy chỉnh nếu có).
4. **Default root object**: Điền **`index.html`** *(Bắt buộc - Đây là trang mặc định khi người dùng truy cập trang chủ)*.

![Cấu hình Settings & Default Root Object](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-settings.png)

5. Nhấp nút **Create distribution**.

---

### Bước 5: Cấu hình Custom Error Responses (Tùy chọn cho SPA - React/Vue/Angular)

Nếu dự án Perfume là một ứng dụng trang đơn (Single Page Application) sử dụng Client-side Routing:

1. Vào tab **Custom error responses** của Distribution vừa tạo.
2. Chọn **Create custom error response**:
   - **HTTP error code**: `403: Forbidden` hoặc `404: Not Found`.
   - **Customize error response**: Chọn **Yes**.
   - **Response page path**: `/index.html`
   - **HTTP response code**: `200: OK`
3. Nhấp **Create custom error response**.

![Cấu hình Custom Error Page](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-error-pages.png)
