## Day 8 : AMI (Amazon Machine Image)

# 1️⃣ Introduction to AMI

What is AMI:

> An AMI (Amazon Machine Image) is a pre-configured template used to launch EC2 instances.

It includes:

 - ✔ Operating System
 - ✔ Installed software
 - ✔ Configuration

👉 Example: You install Nginx → create AMI → reuse anytime

---

# 2️⃣ Why AMI is Important (DevOps)

Explain:

 - ✔ Faster deployment
 - ✔ Standardized environment
 - ✔ Used in Auto Scaling
 - ✔ Backup of server

Used in real-world tools like:

* Terraform
* Jenkins

---

# 3️⃣ Hands-on Demo – Launch Base EC2

---

## Step 1: Go to EC2

Service:

Amazon EC2

Click:

```text id="m1z8ab"
Launch Instance
```

---

## Step 2: Configure Instance

```text id="k9c2pq"
Name: ami-demo-server
AMI: Amazon Linux 2
Instance type: t2.micro
```

Launch instance.

---

# 4️⃣ Connect to EC2

```bash id="p8k3x1"
ssh -i my-key.pem ec2-user@YOUR_PUBLIC_IP
```

---

# 5️⃣ Install Application (Important Step)

---

## Install Nginx

```bash id="c4v8z2"
sudo yum install nginx -y
sudo systemctl start nginx
```

---

## Verify

Open browser:

```text id="z2k8vx"
http://YOUR_PUBLIC_IP
```

👉 You should see Nginx page

---

# 6️⃣ Create AMI (Hands-on)

---

## Step 1: Select Instance

Go to:

Amazon EC2 → Instances

---

## Step 2: Create Image

Click:

```text id="h8p3v2"
Actions → Image → Create Image
```

---

## Step 3: Configure AMI

```text id="q4j9zn"
Name: my-custom-ami
Description: Nginx pre-installed
```

Click:

```text id="r1n5mk"
Create Image
```

---

## Step 4: Wait for AMI

Go to:

```text id="6k8t2f"
AMIs section
```

Status → Available ✅

---

# 7️⃣ Launch EC2 from AMI (Powerful Demo)

---

## Step 1: Select AMI

Go to AMIs → Select your AMI

Click:

```text id="g5x2n9"
Launch Instance
```

---

## Step 2: Launch New Server

No need to install Nginx again ❌

---

## Step 3: Test

Open browser:

```text id="n9k3p1"
http://NEW_PUBLIC_IP
```

👉 Nginx already running ✅

---

# 8️⃣ Real DevOps Use Case

 - ✔ Golden Image concept
 - ✔ Auto Scaling uses AMI
 - ✔ Fast server replication

Example:

```text id="2m1n8v"
One AMI → 100 servers in seconds
```

---

# 9️⃣ Types of AMI

| Type            | Description  |
| --------------- | ------------ |
| Public AMI      | AWS provided |
| Private AMI     | Your custom  |
| Marketplace AMI | Paid         |

---

# 🔟 Common Mistakes

 - ❌ Forget to stop services before AMI 
 - ❌ Wrong region → AMI not visible
 - ❌ Not updating AMI

---

# Homework

 - 1️⃣ Launch EC2
 - 2️⃣ Install app (Nginx)
 - 3️⃣ Create AMI
 - 4️⃣ Launch new EC2 from AMI

---

# Next Video

```text id="p2k9c7"
Auto Scaling Group (ASG)
Launch Template using AMI
```
