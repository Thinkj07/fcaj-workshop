---
title : "Clean up resources"
date : 2026-07-30
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

#### Clean up resources

In this section, we will clean up all AWS resources created during the lab  to avoid incurring unnecessary charges on your AWS account.

---

#### Cleanup Steps

### Disable and Delete CloudFront Distribution

### Cleaning Up the VPC and Associated Resources
1. Navigate to the **VPC Console**, select **NAT Gateways** from the left navigation pane, choose the regional NAT Gateway created alongside your VPC, and click Delete NAT Gateway. Wait for the status to change to Deleted.
2. Return to the Your **VPCs** section, select the project's VPC, click Actions, and choose Delete VPC.In the confirmation dialog, confirm the deletion. AWS will automatically clean up associated subnets, Internet Gateways (IGW), and custom route tables generated during the VPC provisioning.

### Dọn EC2 và các tài nguyên đi kèm
1. Navigate to the **EC2 Console**, go to Load Balancers, select the project's Application Load Balancer (ALB), and click Delete.
2. Navigate to **Target Groups**, select the target group associated with the project, and click Delete.
3. Navigate to **AMIs**, select the project's custom AMI, and click Deregister. Ensure the checkbox **Delete associated snapshots** is ticked to automatically delete the underlying EBS snapshot.
4. Navigate to **Instances**, select the two EC2 instances provisioned for the project, click Instance state, and select Terminate instance.

1. Open the **AWS Management Console** and navigate to **CloudFront**.
2. From the **Distributions** list, select the distribution created for the MonaPerfume project.
3. Click **Disable** on the top toolbar.
4. Confirm disablement and wait **1 to 3 minutes** until the **Status** changes to `Disabled`.
5. Once the status shows `Disabled`, select the distribution again and click **Delete**.
6. A notification will appear stating that the plan must be cancelled before it can be deleted; select **Cancel plan**.
7. Choose **Delete** again, confirm permanent deletion of the CloudFront Distribution.

![Disable and Delete CloudFront Distribution](/images/5-Workshop/5.7-Cleanup/delete-cloudfront.png)

---

### Empty and Delete Amazon S3 Bucket

1. Open the **AWS Management Console** and navigate to **Amazon S3**.
2. Select your S3 Bucket: **`monaperfume-frontend-bucket-2026`**.
3. Click **Empty** on the toolbar.
4. Type **`permanently delete`** in the confirmation box to purge all static build files and folders.
5. Once emptied successfully, return to the Buckets list.
6. Select **`monaperfume-frontend-bucket-2026`** ➔ Click **Delete**.
7. Type the exact bucket name **`monaperfume-frontend-bucket-2026`** in the confirmation field and click **Delete bucket**.

![Empty and Delete S3 Bucket](/images/5-Workshop/5.7-Cleanup/delete-s3.png)