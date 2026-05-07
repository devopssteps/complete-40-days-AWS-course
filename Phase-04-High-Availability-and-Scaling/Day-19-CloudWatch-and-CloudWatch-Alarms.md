# Day-19: CloudWatch and CloudWatch Alarms with hands on
---

# 🚀 What is CloudWatch?

**Amazon CloudWatch** is a monitoring and observability service in
**Amazon Web Services**.

It helps you:

* Monitor EC2, RDS, Lambda, etc.
* Collect logs 📄
* Create alarms 🚨
* Visualize metrics 📊

---

# 🎯 Why CloudWatch is Important?

* Detect server issues early
* Get alerts automatically
* Monitor CPU, memory, disk
* Centralized logging

👉 Used by every DevOps Engineer in production

---
# SNS (Simple Notification Service)
---
# What is SNS?

**Amazon Simple Notification Service (SNS)** is a **fully managed messaging service** in
**Amazon Web Services**.

👉 It is used to:

* Send notifications 📩
* Trigger automation ⚙️
* Connect multiple services

---

# 🎯 Key Concept (Very Important)

### 📡 Pub/Sub Model

* **Publisher** → sends message
* **Topic** → message channel
* **Subscriber** → receives message

👉 Example:

```id="s9a7hp"
CloudWatch → SNS Topic → Email / SMS / Lambda
```

---

# 🔥 Why SNS is Important?

* Real-time alerts 🚨
* Decoupled architecture
* Scalable messaging
* Works with many AWS services

---


---
# 🏗️ Architecture Overview

```id="g2i2wx"
EC2 → CloudWatch Metrics → Alarm → SNS → Email Notification
```

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Launch EC2 Instance

Go to EC2:

* AMI: Amazon Linux 2
* Instance: t2.micro
* Allow SSH

👉 Service: Amazon EC2

---

## 🔹 Step 2: Check Default Metrics

Go to:
👉 CloudWatch → Metrics → EC2

You will see:

* CPUUtilization
* NetworkIn/Out

---

## 🔹 Step 3: Create CloudWatch Alarm 🚨

### 🎯 Goal:

Trigger alert when CPU > 70%

### Steps:

1. Go to **CloudWatch → Alarms → Create Alarm**
2. Select Metric:

   * EC2 → Per Instance → CPUUtilization
3. Set Condition:

   * Threshold: **> 70%**
4. Configure Notification:

   * Create SNS topic

---

## 🔹 Step 4: Setup Notification (SNS)

Use:
👉 Amazon SNS

Steps:

* Create topic
* Add your email
* Confirm subscription

---

## 🔹 Step 5: Generate CPU Load (Test Alarm)

SSH into EC2:

```bash id="o5skq7"
sudo yum install -y stress
stress --cpu 2 --timeout 300
```

---

## 🔍 Observe:

* CPU increases 📈
* Alarm state changes:

  * OK → ALARM
* Email notification received 📧

---

## 🔹 Step 6: Create Dashboard 📊

1. Go to CloudWatch → Dashboards
2. Add:

   * CPUUtilization graph
   * Network traffic

👉 You now have real-time monitoring

---

## 🔹 Step 7: Enable Logs (Advanced Demo)

Install CloudWatch Agent:

```bash id="ql5q5d"
sudo yum install amazon-cloudwatch-agent -y
```

Configure:

* Collect system logs
* Push to CloudWatch Logs

👉 Centralized logging system

---

# 🧠 Real-World Use Cases

* Monitor production servers
* Alert when app crashes
* Track API performance
* Debug logs centrally
