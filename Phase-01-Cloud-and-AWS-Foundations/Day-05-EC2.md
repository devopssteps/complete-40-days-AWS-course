# Complete 40 days AWS Course (day 5) - Ec2 

## Toyday's video will cover:
 * Introduction to EC2
 * What is a Key Pair?
 * What is a Security Group?
 * Hands-on Demo – Launch EC2 Instance
 * Connect via SSH (Hands-on)
 * Install Web Server
 * EC2 Instance Types Explained
 * EC2 Pricing Models
 * Real DevOps Use Case
 * Common Mistakes

# 1️⃣ Introduction to EC2

What is Ec2:

> Amazon EC2 is a service that allows you to create virtual servers in the cloud.

You can run:

 - ✔ Applications
 - ✔ Websites
 - ✔ APIs

---

# 2️⃣ What is a Key Pair?

A **Key Pair** is used to securely connect to your EC2 instance.

It consists of:

* Public Key → stored in AWS
* Private Key (.pem) → stored on your computer

Example:

```bash id="b9d6b1"
my-key.pem
```

👉 You need this file to connect via SSH.

---

# 3️⃣ What is a Security Group?

A **Security Group** is like a **firewall**.

It controls:

 - ✔ Incoming traffic (inbound)
 - ✔ Outgoing traffic (outbound)

Example rules:

| Type  | Port | Purpose        |
| ----- | ---- | -------------- |
| SSH   | 22   | Connect server |
| HTTP  | 80   | Website        |
| HTTPS | 443  | Secure web     |

---

# 4️⃣ Hands-on Demo – Launch EC2 Instance

---

## Step 1: Open EC2 Dashboard

Search:

Amazon EC2

Click:

```text id="yy6f0n"
Launch Instance
```

---

## Step 2: Configure Instance

Name:

```text id="r7y4sd"
my-ec2-demo
```

AMI:

```text id="7w8b8g"
Amazon Linux 2
```

Instance Type:

```text id="l3zslp"
t2.micro
```

---

## Step 3: Create Key Pair

Click:

```text id="hpxb0v"
Create new key pair
```

Name:

```text id="c4ym2j"
my-key
```

Download:

```text id="a3q5o8"
my-key.pem
```

---

## Step 4: Configure Security Group

Allow:

```text id="vexj7i"
SSH (22) → My IP
HTTP (80) → Anywhere
```

---

## Step 5: Launch Instance

Click:

```text id="vwn6zz"
Launch Instance
```

Wait until running.

---

# 5️⃣ Connect via SSH (Hands-on)

Copy Public IP.

---

## For Linux / Mac

```bash id="zz7m1k"
chmod 400 my-key.pem
ssh -i my-key.pem ec2-user@YOUR_PUBLIC_IP
```

---

## For Windows (PowerShell / WSL)

```bash id="2m6grr"
ssh -i my-key.pem ec2-user@YOUR_PUBLIC_IP
```

---

## After Login

Run:

```bash id="rb3p3c"
whoami
uptime
```

Explain:

👉 You are now inside a cloud server.

---

# 6️⃣ Install Web Server (Bonus Demo)

```bash id="r41f2d"
sudo yum install nginx -y
sudo systemctl start nginx
```

Open browser:

```text id="t9z8jx"
http://YOUR_PUBLIC_IP
```

---

# 7️⃣ EC2 Instance Types Explained

Instance types define:

 - ✔ CPU
 - ✔ Memory
 - ✔ Storage

Examples:

| Type     | Use Case      |
| -------- | ------------- |
| t2.micro | Free tier     |
| t2.large | Medium apps   |
| m5.large | Balanced      |
| c5.large | CPU intensive |

---

# 8️⃣ EC2 Pricing Models

### 1. On-Demand

 - ✔ Pay per second
 - ✔ No commitment

---

### 2. Reserved Instances

 - ✔ 1–3 years commitment
 - ✔ Cheaper

---

### 3. Spot Instances

 - ✔ Very cheap
 - ✔ Can be stopped anytime

---

### 4. Free Tier

 - ✔ t2.micro free for 12 months

---

# 9️⃣ Real DevOps Use Case

DevOps engineers use EC2 for:

 - ✔ Deploy applications
 - ✔ Run Docker containers
 - ✔ Kubernetes clusters

Tools used:

* Docker
* Kubernetes

---

# 🔟 Common Mistakes

❌ Forgot SSH port → cannot connect
❌ Wrong key → permission denied
❌ Security group blocked

---

# Homework

 - 1️⃣ Launch EC2
 - 2️⃣ Connect via SSH
 - 3️⃣ Install nginx
 - 4️⃣ Access via browser

---
