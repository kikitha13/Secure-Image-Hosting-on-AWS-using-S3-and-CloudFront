#  Secure Image Hosting on AWS using S3 & CloudFront

> **Author**: Ravilla Kikitha  
> **Use Case**: DevOps | AWS Cloud | Static Content Hosting | Secure Content Delivery  
> **Level**: Beginner to Intermediate

---

##  Project Description

This project demonstrates how to **securely host and deliver static content (images)** using two key AWS services:

- **Amazon S3** (Simple Storage Service) — to store the image privately
- **Amazon CloudFront** — to deliver the image publicly via a secure CDN (Content Delivery Network)

Even though public access is blocked at the S3 level, the image can still be accessed via CloudFront, ensuring **security**, **performance**, and **global availability**.

---

##  What is Amazon S3?

> **Amazon S3 (Simple Storage Service)** is AWS's object storage service that stores data in buckets.

###  Key Features:
- Secure, scalable, durable storage
- Stores any type of file as "objects"
- Used for backups, static websites, images, logs, etc.
- Offers fine-grained **access control** via bucket policies and IAM roles
- Default setting: **private access only**

---

## What is Amazon CloudFront?

> **Amazon CloudFront** is a global Content Delivery Network (CDN) service that delivers content with low latency.

###  Key Features:
- Caches and delivers data from **AWS edge locations**
- Increases speed and performance for global users
- Supports **private content delivery** using **Origin Access Control (OAC)**
- Works with S3, EC2, API Gateway, Load Balancer, etc.
- Supports access controls like **Signed URLs**

---

##  Simple Analogy

- **S3** is a **locked vault** where your file lives.
- **CloudFront** is the **authorized delivery service** that can securely fetch your file from the vault and deliver it quickly to users around the world.

---

##  AWS Services Used

| Service           | Purpose                                                       |
|------------------|---------------------------------------------------------------|
| **Amazon S3**     | Store image (`beach.png`) privately in a secure bucket       |
| **Amazon CloudFront** | Deliver the image securely and globally via CDN          |
| **IAM** (optional)     | Used behind the scenes to manage access (via OAC)        |
| **Route 53** (optional) | For custom domain mapping (not used here)              |

---

##  Project Workflow

 Step-by-Step Guide
🔹 Step 1: Create S3 Bucket
Open AWS S3 Console → Click Create Bucket

Set a unique name (e.g., secure-image-hosting)

Leave default settings or enable versioning

Upload the image beach.png to the bucket

🔹 Step 2: Block Public Access
Go to the Permissions tab in your bucket

Ensure Block all public access is enabled

No public bucket policies or ACLs should exist

Test: Accessing https://<bucket-name>.s3.amazonaws.com/beach.png should show Access Denied

🔹 Step 3: Create CloudFront Distribution
Open CloudFront Console → Click Create Distribution

For Origin domain, select the S3 bucket

Enable Origin Access Control (OAC)

Click Create Distribution

Wait ~10 minutes for deployment

🔹 Step 4: Allow CloudFront to Access S3
CloudFront creates an OAC (Origin Access Control)

Go back to your S3 bucket and confirm that:

The OAC IAM role is allowed to read from the bucket

Use the suggested bucket policy or create your own

🔹 Step 5: Test CloudFront Delivery
Visit:

arduino
Copy
Edit
https://<your-distribution-id>.cloudfront.net/beach.png
✅ You should see the image load successfully!

✅ Access Verification
Access Method	Result
https://<bucket>.s3.amazonaws.com/beach.png	❌ Access Denied
https://<distribution>.cloudfront.net/beach.png	✅ Image Loads





