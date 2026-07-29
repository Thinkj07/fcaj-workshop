---
title : "Create CloudFront Distribution connected to S3 Origin"
date : 2026-07-29
weight : 2
chapter : false
pre : " <b> 5.6.2 </b> "
---

After storing your static frontend build on Amazon S3, the next step is creating an **Amazon CloudFront Distribution** to serve assets via AWS Content Delivery Network (CDN).

AWS has updated the CloudFront creation workflow to a step-by-step wizard. Below is the updated step-by-step guide matching the new interface.

---

### Step 1: Choose a plan

1. Open the **AWS Management Console** and navigate to **CloudFront**.
2. Click **Create distribution**.
3. On the **Choose a plan** screen, select the **Free ($0/month)** tier:

![CloudFront Free Tier Selection](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-choose-plan.png)

4. Click **Next** to proceed.

---

### Step 2: Get started

1. Review general details.
2. Enter an optional description or keep default settings.
![CloudFront name](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-name.png)
3. Click **Next**.

---

### Step 3: Specify origin

1. **Origin domain**: Click the search box and select your S3 Bucket created in step 5.6.1:
   - Example: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`
2. **Origin path**: Leave blank (assuming `index.html` resides at the root folder).
3. **Origin access**:
   - Select **Origin access control settings (recommended)**.
   - Click **Create new OAC**.
   - Keep default settings (Name: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`, Signing behavior: `Sign requests`) ➔ Click **Create**.

![Specify Origin & OAC](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-specify-origin.png)

4. **Viewer protocol policy**: Select **Redirect HTTP to HTTPS**.
5. **Default root object**: Enter **`index.html`** *(Required - Specifies the default page served for root requests)*.
6. Click **Next**.

---

### Step 4: Enable security

1. Review security settings (Basic WAF and DDoS protections are included with the Free tier).
2. Leave default settings and click **Next**.

---

### Step 5: Get TLS certificate

1. Retain the default CloudFront SSL/TLS certificate (`*.cloudfront.net`).
2. Click **Next**.

---

### Step 6: Review and create

1. Review configuration parameters from Step 1 through Step 5.
2. Scroll to the bottom and click **Create distribution**.

![Review & Create Distribution](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-review-create.png)

---

### Step 7: Custom Error Responses (Optional for SPA)

If the Perfume application is a Single Page Application using Client-side routing:

1. Go to the **Custom error responses** tab of your distribution.
2. Click **Create custom error response**:
   - **HTTP error code**: `403: Forbidden` or `404: Not Found`.
   - **Customize error response**: Select **Yes**.
   - **Response page path**: `/index.html`
   - **HTTP response code**: `200: OK`
3. Click **Create custom error response**.

![Configure Custom Error Page](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-error-pages.png)
