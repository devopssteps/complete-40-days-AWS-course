# Day 10: SecurityGroup vs NACL and Elastic IP
---

# 1️⃣ Introduction 

> In AWS networking, Security Groups and NACLs control traffic — but they work very differently. And today we’ll also learn how to assign a static public IP using Elastic IP with hands-on demo.

---

# 2️⃣ Security Group vs NACL (Concept)

---

## 🔐 Security Group

 - ✔ Works at **instance level**
 - ✔ **Stateful** (auto allows response traffic)
 - ✔ Only **Allow rules**

---

## 🚧 NACL (Network ACL)

 - ✔ Works at **subnet level**
 - ✔ **Stateless** (must allow inbound + outbound)
 - ✔ Allow + Deny rules

---

## ⚖️ Key Difference Table

| Feature | Security Group | NACL         |
| ------- | -------------- | ------------ |
| Level   | Instance       | Subnet       |
| Type    | Stateful       | Stateless    |
| Rules   | Allow only     | Allow + Deny |

👉 Say this slowly for SEO

---

# 3️⃣ Hands-on Demo – Security Group

---

## Step 1: Go to EC2

Service:

Amazon EC2

---

## Step 2: Create Security Group

```text
Name: my-sg
```

---

## Step 3: Add Rules

```text
SSH (22) → My IP
HTTP (80) → Anywhere
```

---

## Step 4: Attach to EC2

Launch EC2 with this security group

---

## Step 5: Test

```bash
ssh -i my-key.pem ec2-user@PUBLIC_IP
```

👉 Works ✅

---

# 4️⃣ Hands-on Demo – NACL

---

## Step 1: Go to VPC

Service:

Amazon Virtual Private Cloud

---

## Step 2: Create NACL

```text
Name: my-nacl
```

---

## Step 3: Associate with Subnet

Attach to your subnet

---

## Step 4: Add Rules

---

### Inbound Rule

```text
Allow SSH (22) from your IP
```

---

### Outbound Rule

```text
Allow ALL traffic
```

---

## Step 5: Test Blocking 

👉 Add deny rule:

```text
Deny SSH (22)
```

Now try:

```bash
ssh ec2-user@PUBLIC_IP
```

👉 Connection fails ❌

---

 - ✔ NACL can **block traffic**
 - ✔ Security group cannot deny

---

# 5️⃣ Hands-on Demo – Elastic IP

---

## What is Elastic IP?

👉 Static public IP that doesn’t change

---

## Step 1: Allocate Elastic IP

Go to EC2 → Elastic IPs

```text
Allocate Elastic IP
```

---

## Step 2: Associate with EC2

```text
Select instance → Associate
```

---

## Step 3: Verify

👉 Old IP changes to new static IP

---

## Step 4: Test

```bash
ssh -i my-key.pem ec2-user@ELASTIC_IP
```

👉 Works ✅

---

# 6️⃣ Real DevOps Use Cases

Explain clearly:

 - ✔ Security Group → app-level security
 - ✔ NACL → network-level security
 - ✔ Elastic IP → static server access

---

# 7️⃣ Common Mistakes

 - ❌ Forget outbound rules in NACL
 - ❌ Expect deny in security group
 - ❌ Not releasing unused Elastic IP (cost 💰)

---

# 8️⃣ Summary 

* Security Group = instance firewall
* NACL = subnet firewall
* Elastic IP = static public IP

---

# 9️⃣ Homework

 - 1️⃣ Create security group
 - 2️⃣ Create NACL
 - 3️⃣ Block SSH using NACL
 - 4️⃣ Assign Elastic IP

