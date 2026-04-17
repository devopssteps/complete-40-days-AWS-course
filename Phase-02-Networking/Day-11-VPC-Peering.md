# Day-11-VPC Peering

# 1️⃣ Introduction 

> What if you have two VPCs and want them to communicate securely? That’s where VPC Peering comes in.

---

# 2️⃣ What is VPC Peering?

👉 VPC Peering = **Private connection between two VPCs**

 - ✔ No internet used
 - ✔ Low latency
 - ✔ Secure communication

---

# 3️⃣ Architecture Overview

We will create:

 - ✔ VPC-1 (10.0.0.0/16)
 - ✔ VPC-2 (20.0.0.0/16)
 - ✔ EC2 in each VPC
 - ✔ Peering connection

👉 Goal:

```text
EC2 (VPC-1) ↔ EC2 (VPC-2)
```

---

# 4️⃣ Hands-on Demo – Create VPCs

---

## Step 1: Create VPC-1

Go to:

Amazon Virtual Private Cloud

```text
Name: vpc-1
CIDR: 10.0.0.0/16
```

---

## Step 2: Create VPC-2

```text
Name: vpc-2
CIDR: 20.0.0.0/16
```

---

# 5️⃣ Create Subnets

---

## VPC-1 Subnet

```text
10.0.1.0/24
```

---

## VPC-2 Subnet

```text
20.0.1.0/24
```

---

# 6️⃣ Launch EC2 Instances

Service:

Amazon EC2

---

## EC2 in VPC-1

 - ✔ Subnet: 10.0.1.0
 - ✔ Private IP example: 10.0.1.10

---

## EC2 in VPC-2

 - ✔ Subnet: 20.0.1.0
 - ✔ Private IP example: 20.0.1.10

---

# 7️⃣ Create VPC Peering Connection

---

## Step 1: Go to Peering

```text
VPC → Peering Connections → Create
```

---

## Step 2: Configure

```text
Name: my-peering
Requester VPC: vpc-1
Accepter VPC: vpc-2
```

---

## Step 3: Accept Peering

👉 Go to requests → Accept

---

# 8️⃣ Update Route Tables (VERY IMPORTANT)

---

## Route for VPC-1

Add:

```text
Destination: 20.0.0.0/16 → Peering Connection
```

---

## Route for VPC-2

Add:

```text
Destination: 10.0.0.0/16 → Peering Connection
```

---

# 9️⃣ Update Security Groups

Allow:

```text
Type: All traffic
Source: VPC CIDR
```

Example:

```text
10.0.0.0/16
20.0.0.0/16
```

---

# 🔟 Test Connectivity (Hands-on)

---

## Step 1: SSH into EC2-1

```bash
ssh -i my-key.pem ec2-user@PUBLIC_IP_VPC1
```

---

## Step 2: Ping EC2-2

```bash
ping 20.0.1.10
```

👉 Result:

✔ Success → VPC Peering working ✅

---

# 1️⃣1️⃣ Real DevOps Use Cases

Explain clearly:

 - ✔ Multi-VPC architecture
 - ✔ Microservices in separate VPCs
 - ✔ Dev & Prod isolation

---

# 1️⃣2️⃣ Limitations (Important for Interview)

 - ❌ No transitive peering
 - ❌ No overlapping CIDR
 - ❌ Manual route update

---

# 1️⃣3️⃣ Common Mistakes

 - ❌ Route table not updated
 - ❌ Security group blocking
 - ❌ CIDR overlap

---

# 1️⃣4️⃣ Summary

👉 Say clearly:

* VPC Peering = private communication
* Works via route tables
* No internet required

---

# 1️⃣5️⃣ Homework

 - 1️⃣ Create 2 VPCs
 - 2️⃣ Setup peering
 - 3️⃣ Launch EC2
 - 4️⃣ Test ping
