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
## Step 1: Create S3 Bucket
Open AWS S3 Console → Click Create Bucket

Set a unique name (e.g., secure-image-hosting)

Leave default settings or enable versioning

Upload the image beach.png to the bucket
![WhatsApp Image 2025-08-06 at 16 45 03_77e286c4](https://github.com/user-attachments/assets/9418e227-bb77-4212-86a0-24e9ea520a29)


## Step 2: Block Public Access
Go to the Permissions tab in your bucket

Ensure Block all public access is enabled

No public bucket policies or ACLs should exist

Test: Accessing https://<bucket-name>.s3.amazonaws.com/beach.png should show Access Denied
![WhatsApp Image 2025-08-06 at 16 48 51_f33c5280](https://github.com/user-attachments/assets/63093f19-1d59-43ab-b368-934b4dac180d)



## Step 3: Create CloudFront Distribution
Open CloudFront Console → Click Create Distribution

For Origin domain, select the S3 bucket

Enable Origin Access Control (OAC)

Click Create Distribution

Wait ~10 minutes for deployment
![WhatsApp Image 2025-08-06 at 16 50 00_9e7ebeba](https://github.com/user-attachments/assets/812afee7-90cb-4eb9-b203-94ced7c2c4e1)


 ## Step 4: Allow CloudFront to Access S3
CloudFront creates an OAC (Origin Access Control)

Go back to your S3 bucket and confirm that:

The OAC IAM role is allowed to read from the bucket

Use the suggested bucket policy or create your own

## Step 5: Test CloudFront Delivery
Visit:


https://<your-distribution-id>.cloudfront.net/beach.png
 You should see the image load successfully!
 ![WhatsApp Image 2025-08-06 at 16 50 51_926d0a75](https://github.com/user-attachments/assets/cd566490-cb8e-4dfd-8704-2c22037f8828)


 Access Verification
Access Method	Result
https://<bucket>.s3.amazonaws.com/beach.png	 Access Denied
https://<distribution>.cloudfront.net/beach.png	 Image Loads

##  Final Conclusion

After thoroughly verifying each step and configuration, this project confirms the correct and secure setup of static content delivery using AWS services. The image `beach.png` was uploaded to a **private Amazon S3 bucket** with **public access blocked**, ensuring data privacy. Despite the restricted access, the image was successfully delivered via **Amazon CloudFront**, demonstrating the effectiveness of **Origin Access Control (OAC)** in securely linking CloudFront with private S3 buckets.

This validates the project’s key objective:  
> **To securely deliver static content from S3 using CloudFront without exposing the S3 bucket to the public.**

This mini project reflects real-world DevOps and cloud architecture best practices and is an excellent addition to your portfolio. It also lays a strong foundation for future enhancements like signed URLs, custom domain routing with Route 53, and content lifecycle policies.






