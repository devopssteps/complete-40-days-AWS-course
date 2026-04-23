# Day-17: AWS Auto Scaling Groups (ASG) 

### ✅ What is Auto Scaling Group?

An **Auto Scaling Group (ASG)** automatically:

* Launches EC2 instances when load increases 📈
* Terminates instances when load decreases 📉
* Maintains a fixed number of healthy instances

👉 It works together with:

* Amazon Web Services
* Amazon EC2
* Elastic Load Balancing

---

### 🎯 Why ASG is Important?

* High availability (no downtime)
* Cost optimization (no idle servers)
* Automatic scaling (no manual intervention)
* Self-healing (replaces unhealthy instances)

---

# 🏗️ Architecture Overview

```
User Traffic → Load Balancer → Auto Scaling Group → EC2 Instances
```

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Create Launch Template

1. Go to AWS Console → EC2
2. Click **Launch Templates → Create Launch Template**
3. Configure:

   * AMI: Amazon Linux 2
   * Instance type: t2.micro (Free tier)
   * Key pair: select/create
   * Security Group: Allow HTTP (80) + SSH (22)

### 🔧 Add User Data (Important)

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "Hello from Auto Scaling Instance $(hostname -f)" > /var/www/html/index.html
```

👉 This creates a simple web server.

---

## 🔹 Step 2: Create Target Group

1. Go to **EC2 → Target Groups**
2. Create:

   * Type: Instance
   * Protocol: HTTP
   * Port: 80

---

## 🔹 Step 3: Create Load Balancer

1. Go to **Load Balancers**
2. Choose:

   * Application Load Balancer
3. Configure:

   * Internet-facing
   * Listener: HTTP (80)
   * Attach Target Group

---

## 🔹 Step 4: Create Auto Scaling Group

1. Go to **Auto Scaling Groups**
2. Click **Create Auto Scaling Group**
3. Select Launch Template

### ⚙️ Configure:

* VPC + Subnets (at least 2 AZs)
* Attach Load Balancer
* Set:

  * Desired capacity: 2
  * Min: 1
  * Max: 4

---

## 🔹 Step 5: Configure Scaling Policy

Choose:

### 📈 Target Tracking Policy

* Metric: Average CPU Utilization
* Target: 50%

👉 Meaning:

* If CPU > 50% → Add instance
* If CPU < 50% → Remove instance

---

## 🔹 Step 6: Test Auto Scaling

### 💥 Generate Load

SSH into one instance:

```bash
sudo yum install -y stress
stress --cpu 2 --timeout 300
```

👉 This increases CPU usage

---

### 🔍 Observe:

* New instance will launch automatically
* Load Balancer distributes traffic
* When load drops → instance terminates
