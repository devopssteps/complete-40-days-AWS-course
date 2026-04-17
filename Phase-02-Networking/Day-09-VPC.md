# Complete 40 days AWS Course (day 9) - VPC

---

# 1️⃣ Introduction 

What is VPC:

> VPC is the foundation of AWS networking. In this video, we’ll build a complete VPC from scratch with public and private subnets, route tables, and NAT Gateway — with real hands-on demo.

---

# 2️⃣ Architecture Overview 

We will create:

 - ✔ 1 VPC
 - ✔ 2 Subnets
 - ✔ 1 Internet Gateway
 - ✔ 1 NAT Gateway
 - ✔ 2 Route Tables

👉 We will create 2 subnet as follows:

* Public subnet → Internet access
* Private subnet → No direct internet

---

# 3️⃣ Hands-on Demo – Create VPC

---

## Step 1: Create VPC

Go to:

Amazon Virtual Private Cloud

Click:

```text id="6r2k1p"
Create VPC
```

---

## Step 2: Configure VPC

```text id="2h9x7m"
Name: my-vpc
CIDR: 10.0.0.0/16
```

---

# 4️⃣ Create Subnets

---

## Public Subnet

```text id="m2k8c1"
Name: public-subnet
CIDR: 10.0.1.0/24
```

---

## Private Subnet

```text id="z3p9q2"
Name: private-subnet
CIDR: 10.0.2.0/24
```

---

# 5️⃣ Create Internet Gateway (IGW)

---

## Step 1: Create IGW

```text id="6d2k1x"
Create Internet Gateway
```

---

## Step 2: Attach to VPC

```text id="4f8m2p"
Attach to my-vpc
```

---

# 6️⃣ Create Route Table (Public)

---

## Step 1: Create Route Table

```text id="k2p8x1"
public-rt
```

---

## Step 2: Add Route

```text id="3v9c1m"
0.0.0.0/0 → Internet Gateway
```

---

## Step 3: Associate Subnet

Attach:

```text id="9k2v1x"
public-subnet
```

---

# 7️⃣ Launch EC2 in Public Subnet

Service:

Amazon EC2

 - ✔ Enable Public IP
 - ✔ Security group allow SSH

---

## Test SSH

```bash id="b2k9x3"
ssh -i my-key.pem ec2-user@PUBLIC_IP
```

👉 Works ✅

---

# 8️⃣ Create NAT Gateway (Important)

---

## Step 1: Allocate Elastic IP

```text id="2n8k3p"
Allocate Elastic IP
```

---

## Step 2: Create NAT Gateway

```text id="7x1k9p"
Select public-subnet
Attach Elastic IP
```

---

# 9️⃣ Create Private Route Table

---

## Step 1: Create Route Table

```text id="8p2m1k"
private-rt
```

---

## Step 2: Add Route

```text id="4x9k2m"
0.0.0.0/0 → NAT Gateway
```

---

## Step 3: Associate

```text id="6k3p1v"
private-subnet
```

---

# 🔟 Launch EC2 in Private Subnet

---

## Important

 - ❌ No public IP
 - ❌ Cannot SSH directly

---

# 1️⃣1️⃣ Test NAT Gateway 

---

## Step 1: Connect via Public EC2 (Bastion Host)

```bash id="8v2k1x"
ssh -i my-key.pem ec2-user@PUBLIC_EC2
```

---

## Step 2: SSH to Private EC2

```bash id="9x1p2k"
ssh ec2-user@PRIVATE_IP
```

---

## Step 3: Test Internet Access

```bash id="3k8p1m"
sudo yum update -y
```

👉 Works ✅ (via NAT Gateway)

---

# 1️⃣2️⃣ Real DevOps Architecture

Explain clearly:

 - ✔ Public subnet → Load Balancer / Bastion
 - ✔ Private subnet → App / DB
 - ✔ NAT → Secure internet access

---

# 1️⃣3️⃣ Common Mistakes

 - ❌ No route to IGW → no internet
 - ❌ NAT in wrong subnet
 - ❌ Wrong route table association

---

# 1️⃣4️⃣ Summary

* VPC = Network
* Subnet = Segment
* IGW = Internet access
* NAT = Private subnet internet

---

# 1️⃣5️⃣ Homework

 - 1️⃣ Create VPC
 - 2️⃣ Add public/private subnet
 - 3️⃣ Configure NAT
 - 4️⃣ Test connectivity

---
