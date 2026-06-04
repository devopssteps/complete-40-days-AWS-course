# Day-19: Launch Templates & Multi-AZ Architecture 
 
## 🔹 What is a Launch Template?

A **Launch Template** is a reusable configuration to launch EC2 instances.

It defines:

* AMI (OS)
* Instance type
* Security group
* Key pair
* User data (startup script)

👉 Used with:

* Amazon EC2
* Auto Scaling Groups

---

## 🔹 What is Multi-AZ Architecture?

A **Multi-AZ (Availability Zone) architecture** means:

* Your application runs in **multiple data centers**
* Even if one AZ fails → your app stays UP ✅

👉 Example:

* AZ-1 → running instances
* AZ-2 → backup/active instances

Used with:

* Amazon Web Services
* Elastic Load Balancing

---

## 🎯 Why These Matter Together?

| Feature         | Benefit                          |
| --------------- | -------------------------------- |
| Launch Template | Consistent instance setup        |
| Multi-AZ        | High availability                |
| Combined        | Scalable + Fault-tolerant system |

---

# 🏗️ Architecture Overview

```id="j6xj0b"
User → Load Balancer → Multi-AZ (AZ1 + AZ2) → EC2 (via Launch Template)
```

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Create Launch Template

Go to EC2 → Launch Templates → Create

### Configure:

* Name: `devops-lt`
* AMI: Amazon Linux 2
* Instance type: t2.micro
* Security Group:

  * HTTP (80)
  * SSH (22)

---

### 🔧 Add User Data

```bash id="bgd1pl"
#!/bin/bash
sudo yum update -y
sudo yum install -y httpd

sudo systemctl start httpd
sudo systemctl enable httpd

TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
-H "X-aws-ec2-metadata-token-ttl-seconds: 21600" -s)

AZ=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" \
-s http://169.254.169.254/latest/meta-data/placement/availability-zone)

echo "<h1>Server running in AZ: $AZ</h1>" > /var/www/html/index.html
```

👉 This shows which AZ your instance is running in.

---

## 🔹 Step 2: Create Target Group

* Type: Instance
* Protocol: HTTP
* Port: 80

---

## 🔹 Step 3: Create Application Load Balancer

* Scheme: Internet-facing
* Listener: HTTP (80)
* Select **at least 2 Availability Zones**

👉 This is key for Multi-AZ!

---

## 🔹 Step 4: Create Auto Scaling Group (Multi-AZ Setup)

1. Select Launch Template
2. Choose:

   * VPC
   * **Select 2+ subnets (different AZs)**

### ⚙️ Capacity:

* Desired: 2
* Min: 2
* Max: 4

👉 Ensures instances run in multiple AZs

---

## 🔹 Step 5: Attach Load Balancer

* Select existing Load Balancer
* Attach Target Group

---

## 🔹 Step 6: Test Multi-AZ Behavior

### 🌐 Open Load Balancer DNS

Refresh browser multiple times:

👉 Output:

```
Server running in AZ: ap-south-1a
Server running in AZ: ap-south-1b
```

🔥 This proves traffic is distributed across AZs

---

## 🔹 Step 7: Simulate Failure (Important Demo)

* Stop one instance manually

👉 Observe:

* ASG launches new instance automatically
* Traffic still works (no downtime)

---

# 🎥 Pro Recording Tips

* Show:

  * Instances in different AZs
  * Load balancer switching responses
  * Instance termination + auto recovery
* Highlight AZ names clearly

---

# 🧠 Real-World Use Case

* Banking apps (no downtime)
* E-commerce platforms
* SaaS applications
* Kubernetes worker nodes (EKS)
