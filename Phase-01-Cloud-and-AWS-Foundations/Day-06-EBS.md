# Complete 40 days AWS Course (day 6) - EBS with Hands on

## Toyday's video will cover:
 * Introduction to EBS
 * Types of EBS Volumes 
 * Hands-on Demo – Create EBS Volume
 * Attach Volume to EC2 (Hands-on)
 * Connect to EC2 via SSH
 * Hands-on – Mount EBS Volume
 * Test Storage
 * Make Mount Permanent
 * Real DevOps Use Cases
 * Common Mistakes
 
---
# 1️⃣ Introduction to EBS

What is EBS volume:

> Amazon EBS is a block storage service that provides persistent storage for EC2 instances.

 - ✔ Works like a hard disk
 - ✔ Data is NOT lost after stop/start
 - ✔ Used for databases, apps, logs

---

# 2️⃣ Types of EBS Volumes (Short Explanation)

| Type      | Use Case             |
| --------- | -------------------- |
| gp2 / gp3 | General purpose      |
| io1 / io2 | High performance     |
| st1       | Throughput optimized |
| sc1       | Cold storage         |

👉 For demo, we use **gp3 **

---

# 3️⃣ Hands-on Demo – Create EBS Volume

---

## Step 1: Go to EBS Dashboard

Search:

Amazon Elastic Block Store

Click:

```text
Volumes → Create Volume
```

---

## Step 2: Configure Volume

Example:

```text
Size: 5 GiB
Type: gp3
Availability Zone: ap-south-1a
```

⚠️ Important:

👉 Must be same AZ as your EC2 instance

---

## Step 3: Create Volume

Click:

```text
Create Volume
```

---

# 4️⃣ Attach Volume to EC2 (Hands-on)

---

## Step 1: Select Volume

Click:

```text
Actions → Attach Volume
```

---

## Step 2: Choose Instance

Select your EC2 instance:

Amazon EC2

Device name:

```text
/dev/xvdf
```

---

## Step 3: Attach

Click:

```text
Attach
```

---

# 5️⃣ Connect to EC2 via SSH

```bash
ssh -i my-key.pem ec2-user@YOUR_PUBLIC_IP
```

---

# 6️⃣ Hands-on – Mount EBS Volume

---

## Step 1: Check Disk

```bash
lsblk
```

Example output:

```bash
xvda   8:0    0   8G  0 disk
└─xvda1
xvdf   8:16   0   5G  0 disk
```

👉 New disk = `/dev/xvdf`

---

## Step 2: Format Disk

```bash
sudo mkfs -t ext4 /dev/xvdf
```

---

## Step 3: Create Mount Directory

```bash
sudo mkdir /data
```

---

## Step 4: Mount Volume

```bash
sudo mount /dev/xvdf /data
```

---

## Step 5: Verify Mount

```bash
df -h
```

You will see:

```bash
/dev/xvdf   mounted on /data
```

---

# 7️⃣ Test Storage (Important)

```bash
cd /data
sudo touch testfile
ls
```

👉 File created successfully ✅

---

# 8️⃣ Make Mount Permanent (VERY IMPORTANT)

If you restart instance, mount will be lost ❌

---

## Step 1: Get UUID

```bash
sudo blkid
```

---

## Step 2: Edit fstab

```bash
sudo vi /etc/fstab
```

Add:

```bash
UUID=xxxx  /data  ext4  defaults,nofail  0  2
```

---

## Step 3: Test

```bash
sudo mount -a
```

---

# 9️⃣ Real DevOps Use Cases

 - ✔ Store application data
 - ✔ Database storage
 - ✔ Logs storage
 - ✔ Kubernetes persistent volume

Used with:

* Docker
* Kubernetes

---

# 🔟 Common Mistakes

 - ❌ Wrong AZ → cannot attach
 - ❌ Forgot format → mount fails
 - ❌ Not added in fstab → data not mounted after reboot

---
# Increase Volume 
 - Increase volume from AWS console
 - Now run the following command 

```bash
sudo growpart /dev/nvme0n1 1
sudo xfs_growfs -d /
```

---
# Homework

 - 1️⃣ Create EBS volume
 - 2️⃣ Attach to EC2
 - 3️⃣ Mount it
 - 4️⃣ Create file inside

---
