---
title : "Environment Setup and Application Deployment"
date : 2026-07-26
weight : 3
chapter : false
pre : " <b> 5.5.3 </b> "
---

# Environment Setup and Application Deployment (Deploy)

In this section, we will connect to the private EC2 instance using **AWS Systems Manager Session Manager (SSM)**, install Node.js environment, clone the Perfume Store Backend source code, configure environment variables for **Amazon RDS** and **Amazon S3** connectivity, run database migrations (Prisma Migrate & Seed), launch the backend application using **PM2**, and verify health status through the **Application Load Balancer (ALB)**.

---

### Step 1: Connect to Private EC2 Instance via AWS Systems Manager (SSM)

Because the EC2 instance resides in a Private Subnet without a Public IP, we use **SSM Session Manager** to establish a secure connection without opening SSH port 22.

1. Open the **AWS Management Console** -> navigate to **Systems Manager** (or search `Session Manager`).
2. On the left navigation pane, choose **Session Manager** -> click **Start session**.
3. Select the EC2 instance `MonaPerfume-EC2-PRIVATE-01` -> click **Start session**.
4. A new browser terminal tab will open with the shell prompt `sh-4.2$`.

Switch to the `ec2-user` and navigate to the home directory:
```bash
sudo su - ec2-user
cd ~
```

---

### Step 2: Install Node.js, Git, and PM2

1. Update system package repositories on Amazon Linux 2023:
```bash
sudo dnf update -y
```

2. Install **Git**:
```bash
sudo dnf install git -y
git --version
```

3. Install **Node.js 22.x** (compatible version for the application):
```bash
curl -fsSL https://rpm.nodesource.com/setup_22.x | sudo bash -
sudo dnf install -y nodejs
node -v
npm -v
```

4. Install **PM2** process manager globally:
```bash
sudo npm install -g pm2
```

---

### Step 3: Clone Backend Source Code and Install Dependencies

1. Clone the repository containing the Perfume Store backend codebase:
```bash
git clone https://github.com/uyentrn/web-project.git
cd web-project/backend
```

2. Install application dependencies:
```bash
npm install
```

---

### Step 4: Configure Environment Variables (.env)

Create a `.env` file to connect the application to **Amazon RDS** and **Amazon S3**:

```bash
nano .env
```

Enter the configuration values matching the AWS infrastructure resources created in previous steps:

```env
PORT=3000
NODE_ENV=production

# Amazon RDS Database Connection String (Database Endpoint from step 5.4)
DATABASE_URL="postgresql://dbadmin:YourStrongPassword123@monaperfume-rds.c123456789.us-east-1.rds.amazonaws.com:5432/monaperfumedb?schema=public"

# Amazon S3 Bucket Configuration (from step 5.6)
AWS_REGION=us-east-1
S3_BUCKET_NAME=monaperfume-assets-bucket

# Application Security Key
JWT_SECRET="MonaPerfumeSecretKey2026"
```

Save and exit the file (`Ctrl + O`, `Enter`, `Ctrl + X`).

---

### Step 5: Execute Database Migrations and Start Backend

1. Generate Prisma client and deploy database schema migrations:
```bash
npx prisma generate
npx prisma migrate deploy
```

2. Seed initial sample database records:
```bash
npm run db:seed
```

3. Launch the backend application on port `3000` using **PM2**:
```bash
pm2 start src/server.js --name "monaperfume-backend"
pm2 save
```

4. Configure **PM2** to start automatically on system reboot:
```bash
pm2 startup systemd
```

5. Verify application status:
```bash
pm2 status
curl http://localhost:3000/api/health
```

---

### Step 6: Verify Traffic Routing via Application Load Balancer (ALB)

1. Open **EC2 Console** -> choose **Target Groups** -> select `MonaPerfume-TG`.
2. Select the **Targets** tab and verify the health status of `MonaPerfume-EC2-PRIVATE-01`. The status must display **Healthy**.
3. Open **EC2 Console** -> choose **Load Balancers** -> select `MonaPerfume-ALB`.
4. Copy the ALB **DNS name** (e.g., `MonaPerfume-ALB-123456789.us-east-1.elb.amazonaws.com`).
5. Test connectivity from your local terminal or browser:
```bash
curl http://MonaPerfume-ALB-123456789.us-east-1.elb.amazonaws.com/api/health
```

---

### Step 7: Create AMI (Amazon Machine Image) to Launch Second EC2 Instance

Once the first EC2 instance is configured and successfully deployed:

1. Open **EC2 Console** -> choose **Instances** -> right-click `MonaPerfume-EC2-PRIVATE-01`.
2. Select **Image and templates** -> click **Create image**.
3. Enter Image name: `MonaPerfume-Backend-AMI` -> click **Create image**.
4. Once the AMI is available, use it to launch `MonaPerfume-EC2-PRIVATE-02` in **Subnet Private 2** (AZ us-east-1b) to complete the **Multi-AZ High Availability** architecture.
