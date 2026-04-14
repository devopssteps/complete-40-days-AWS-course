# Complete 40 days AWS Course (day 7) - EFS with Hands on

## Toyday's video will cover:
 * Introduction to EFS
 * EFS vs EBS (Quick Comparison)
 * Hands-on Demo – Create EFS
 * Launch EC2 Instance, Install EFS Client and connect to EFS
 * Mount EFS (Hands-on) the best way
 * Test Shared Storage
 * Make Mount Permanent
 * Real DevOps Use Cases
 * Common Mistakes
 * Homework

# 1️⃣ Introduction to EFS

What is EFS:

> Amazon EFS is a scalable file storage service that allows multiple EC2 instances to share the same file system.

 - ✔ Shared storage (like NFS)
 - ✔ Auto scaling
 - ✔ Multi-instance access

---

# 2️⃣ EFS vs EBS (Quick Comparison)

| Feature  | EFS          | EBS           |
| -------- | ------------ | ------------- |
| Type     | File storage | Block storage |
| Attach   | Multiple EC2 | One EC2       |
| Scaling  | Auto         | Manual        |
| Use case | Shared apps  | Database      |


---

# 3️⃣ Hands-on Demo – Create EFS

---

## Step 1: Go to EFS Dashboard

Search:

Amazon Elastic File System

Click:

```text id="5d3f2k"
Create file system
```

---

## Step 2: Configure EFS

```text id="h7k2p1"
Name: my-efs-demo
Region: ap-south-1
```

Click:

```text id="j8w1c2"
Create
```

---

## Step 3: Create Mount Targets

👉 This is VERY important

EFS must be accessible from EC2 via VPC.

Select VPC → Subnets → Security Group

---

## Step 4: Configure Security Group

Allow:

```text id="p3k9f0"
NFS (2049) → From EC2 security group
```

---

# 4️⃣ Launch EC2 Instance (if not already)

Use:

Amazon EC2

Make sure:

 - ✔ Same VPC
 - ✔ Same region

---

# 5️⃣ Connect to EC2

```bash id="1c7h3d"
ssh -i my-key.pem ec2-user@YOUR_PUBLIC_IP
```

---

# 6️⃣ Install EFS Client (Important Step)

---

## For Amazon Linux

```bash id="l9z8q0"
sudo yum install amazon-efs-utils -y
```

---

## For Ubuntu

```bash id="4g8m2d"
sudo apt update
sudo apt install nfs-common -y
```

---

# 7️⃣ Mount EFS (Hands-on)

---

## Step 1: Create Directory

```bash id="7v2b1s"
sudo mkdir /efs
```

---

## Step 2: Mount EFS

Use EFS DNS name:

```bash id="8y4n6k"
sudo mount -t efs fs-xxxx:/ /efs
```

👉 Replace `fs-xxxx` with your File System ID

---

## Step 3: Verify Mount

```bash id="3k5v9p"
df -h
```

You will see:

```bash id="6j1p4r"
/efs mounted
```

---

# 8️⃣ Test Shared Storage 

---

## Create File

```bash id="3d7j8n"
cd /efs
sudo touch shared-file.txt
```

---

## Multi-Instance 

 - 👉 Launch another EC2 instance
 - 👉 Mount same EFS

Now check:

```bash id="1n2x3m"
ls /efs
```

✔ Same file visible → proves shared storage ✅

---

# 9️⃣ Make Mount Permanent

---

Edit fstab:

```bash id="z9p2x6"
sudo nano /etc/fstab
```

Add:

```bash id="8c2h7n"
fs-xxxx:/ /efs efs defaults,_netdev 0 0
```

---

Test:

```bash id="0v6s3m"
sudo mount -a
```

---

# 🔟 Real DevOps Use Cases

 - ✔ Shared application storage
 - ✔ Kubernetes shared volumes
 - ✔ CI/CD shared workspace
 - ✔ WordPress multi-server setup

Used with:

* Kubernetes
* Docker

---

# 1️⃣1️⃣ Common Mistakes

 - ❌ Port 2049 not open
 - ❌ Different VPC
 - ❌ Missing mount target

---

# 1️⃣2️⃣ Homework

 - 1️⃣ Create EFS
 - 2️⃣ Mount in EC2
 - 3️⃣ Create file
 - 4️⃣ Check from another EC2

---
