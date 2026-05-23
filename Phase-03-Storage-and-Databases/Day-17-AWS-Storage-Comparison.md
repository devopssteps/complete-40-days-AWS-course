# Day-17: AWS Storage Comparison | EBS vs EFS vs S3 (Hands-on Demo)

---

# 1️⃣ Introduction 

> In AWS, choosing the right storage is critical. In this video, we’ll compare EBS, EFS, and S3 with real hands-on demos so you understand exactly when to use each.

---

# 2️⃣ Quick Comparison Table (Explain Clearly)

| Feature  | EBS        | EFS          | S3                   |
| -------- | ---------- | ------------ | -------------------- |
| Type     | Block      | File         | Object               |
| Attach   | Single EC2 | Multiple EC2 | Internet/API         |
| Use Case | OS, DB     | Shared apps  | Backup, static files |
| Mount    | Yes        | Yes          | No (API access)      |

---

# 3️⃣ Hands-on Demo 1 – EBS (Block Storage)

Service:

Amazon Elastic Block Store

---

## Step 1: Attach EBS to EC2

(Already shown in previous video—brief recap)

---

## Step 2: Mount Volume

```bash
lsblk
sudo mkfs -t ext4 /dev/xvdf
sudo mkdir /data
sudo mount /dev/xvdf /data
```

---

## Step 3: Test

```bash
cd /data
touch ebs-file.txt
```

👉 Explanation:

 - ✔ Works like a hard disk
 - ❌ Only one EC2 can use it

---

# 4️⃣ Hands-on Demo 2 – EFS (Shared File Storage)

Service:

Amazon Elastic File System

---

## Step 1: Mount EFS

```bash
sudo mkdir /efs
sudo mount -t efs fs-xxxx:/ /efs
```

---

## Step 2: Test

```bash
cd /efs
touch efs-file.txt
```

---

## Step 3: Multi-Instance Demo

 - 👉 Connect another EC2
 - 👉 Mount same EFS

```bash
ls /efs
```

✔ Same file visible

👉 Explain:

 - ✔ Shared storage
 - ✔ Multiple EC2 access

---

# 5️⃣ Hands-on Demo 3 – S3 (Object Storage)

Service:

Amazon S3

---

## Step 1: Create Bucket

```bash
aws s3 mb s3://my-demo-bucket-12345
```

---

## Step 2: Upload File

```bash
echo "hello s3" > file.txt
aws s3 cp file.txt s3://my-demo-bucket-12345
```

---

## Step 3: Access File

```bash
aws s3 ls s3://my-demo-bucket-12345
```

---

👉 Explain:

 - ✔ No mounting
 - ✔ Access via API/CLI
 - ✔ Unlimited storage

---

# 6️⃣ Real-Time Comparison 

---

## Scenario 1: Database Storage

 - ✔ Use → EBS
 - ❌ Not EFS / S3

---

## Scenario 2: Shared App (Multiple Servers)

✔ Use → EFS

---

## Scenario 3: Backup / Images / Videos

✔ Use → S3

---

# 7️⃣ Architecture Example (Explain Visually)

* EC2 + EBS → OS + DB
* EC2 + EFS → shared files
* S3 → backup + static content

---

# 8️⃣ Real DevOps Use Cases

 - ✔ Kubernetes → EFS
 - ✔ CI/CD artifacts → S3
 - ✔ Database → EBS

---

# 9️⃣ Common Mistakes

 - ❌ Using S3 as disk
 - ❌ Using EBS for multiple servers
 - ❌ Ignoring cost differences

---

# 🔟 Summary 

* EBS = Single server disk
* EFS = Shared file system
* S3 = Object storage (internet-based)

---

# 1️⃣1️⃣ Homework

 - 1️⃣ Create EBS → mount
 - 2️⃣ Create EFS → share
 - 3️⃣ Upload file to S3
