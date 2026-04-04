# Complete 40 days AWS Course (day 4) - AWS CLI 
## Toyday's video will cover:
 * AWS CLI Setup 
 * Configure AWS CLI
 * Basic CLI Commands

---

# 1️⃣ Introduction to AWS CLI

What is AWS CLI:

> AWS CLI is a tool that allows you to interact with AWS services directly from your terminal instead of using the web console.

Instead of clicking in UI, you run commands like:

```bash
aws ec2 describe-instances
```

---

# 2️⃣ Why AWS CLI is Important (DevOps Perspective)

Explain clearly:

 * ✔ Automation
 * ✔ Scripting
 * ✔ CI/CD pipelines
 * ✔ Infrastructure as Code

DevOps tools that use CLI heavily:

* Jenkins
* Terraform

---

# 3️⃣ Prerequisites

Before setup:

 * ✔ AWS account
 * ✔ IAM user with programmatic access

Service used:

AWS Identity and Access Management

---

# 4️⃣ Hands-on Demo – Install AWS CLI

---

## 💻 For Windows

Download from:

```bash
https://awscli.amazonaws.com/AWSCLIV2.msi
```

Install normally.

---

## 💻 For Linux (Ubuntu)

```bash
sudo apt update
sudo apt install awscli -y
```

---

## ✅ Verify Installation

```bash
aws --version
```

Example output:

```bash
aws-cli/2.x.x Python/3.x
```

---

# 5️⃣ Create Access Keys (VERY IMPORTANT)

Go to AWS Console → IAM

Service:

AWS Identity and Access Management

---

### Steps:

1. Users → Select user
2. Security credentials
3. Create Access Key

You will get:

```bash
Access Key ID
Secret Access Key
```

⚠️ Download and save it safely

---

# 6️⃣ Configure AWS CLI (Core Part)

Run:

```bash
aws configure
```

Enter:

```bash
AWS Access Key ID: XXXX
AWS Secret Access Key: XXXX
Default region name: ap-southeast-1
Default output format: json
```

---

# 📍 Important

Region example:

```bash
ap-south-1
ap-southeast-1
us-east-1
```

---

# 7️⃣ Test Configuration

Run:

```bash
aws sts get-caller-identity
```

If successful → CLI is working ✅

---

# 8️⃣ Basic AWS CLI Commands (Hands-on)

---

## 1. List S3 Buckets

Service:

Amazon S3

```bash
aws s3 ls
```

---

## 2. List EC2 Instances

Service:

Amazon EC2

```bash
aws ec2 describe-instances
```

---

## 3. Create S3 Bucket

```bash
aws s3 mb s3://my-demo-bucket-12345
```

---

## 4. Upload File to S3

```bash
aws s3 cp file.txt s3://my-demo-bucket-12345
```

---

## 5. List Files in Bucket

```bash
aws s3 ls s3://my-demo-bucket-12345
```

---

## 6. Delete Bucket

```bash
aws s3 rb s3://my-demo-bucket-12345 --force
```

---

# 9️⃣ Real DevOps Use Case

Explanation:

Instead of manual steps:

 * ✔ CI/CD pipelines use CLI
 * ✔ Automation scripts use CLI

Example:

```bash
aws ec2 run-instances
```

Used in:

* Jenkins pipelines
* Terraform automation

---

# 🔟 Common Errors 

 * ❌ Invalid credentials
 * ❌ Wrong region
 * ❌ Permission denied

Fix:

 * ✔ Check IAM policies
 * ✔ Verify access keys

---

# Homework

Your home work:

1. Install AWS CLI
2. Configure it
3. Create S3 bucket
4. Upload file

---

