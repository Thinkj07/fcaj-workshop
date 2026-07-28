---
title : "Create CloudFront Distribution connected to S3 Origin"
date : 2026-07-28
weight : 2
chapter : false
pre : " <b> 5.6.2 </b> "
---

After storing your static frontend build on Amazon S3, the next step is creating an **Amazon CloudFront Distribution** to serve assets via AWS Content Delivery Network (CDN).

---

### Step 1: Initialize CloudFront Distribution

1. Open the **AWS Management Console** and navigate to **CloudFront**.
2. Click **Create distribution**.

![Create CloudFront Distribution](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-create.png)

---

### Step 2: Configure Origin Settings

1. **Origin domain**: Click the search box and select your S3 Bucket created in step 1:
   - Example: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`
2. **Origin path**: Leave blank (assuming `index.html` is at root level).
3. **Name**: Auto-populated by AWS.
4. **Origin access**:
   - Select **Origin access control settings (recommended)**.
   - Click **Create new OAC**.
   - Maintain default settings (Name: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`, Signing behavior: `Sign requests`).
   - Click **Create**.

![Configure Origin & OAC](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-origin-oac.png)

---

### Step 3: Configure Default Cache Behavior

1. **Viewer protocol policy**: Select **Redirect HTTP to HTTPS**.
2. **Allowed HTTP methods**: Select **GET, HEAD**.
3. **Restrict viewer access**: Select **No**.
4. **Cache key and origin requests**: Select **CachingOptimized (recommended)**.

![Default Cache Behavior](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-behavior.png)

---

### Step 4: Configure WAF & Settings

1. **Web Application Firewall (WAF)**: Select **Do not enable security protections** (to minimize workshop costs).
2. **Price class**: Select **Use all edge locations** or **Use only North America and Europe**.
3. **Default root object**: Enter **`index.html`** *(Required - Specifies home page default document)*.

![Configure Settings & Default Root Object](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-settings.png)

4. Click **Create distribution**.

---

### Step 5: Configure Custom Error Responses (Optional for SPA)

If the Perfume application is a Single Page Application using Client-side routing:

1. Go to the **Custom error responses** tab of your new distribution.
2. Click **Create custom error response**:
   - **HTTP error code**: `403: Forbidden` or `404: Not Found`.
   - **Customize error response**: Select **Yes**.
   - **Response page path**: `/index.html`
   - **HTTP response code**: `200: OK`
3. Click **Create custom error response**.

![Configure Custom Error Page](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-error-pages.png)
