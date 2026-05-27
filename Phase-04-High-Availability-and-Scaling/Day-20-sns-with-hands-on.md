# Day-20: SNS (Simple Notification Service)
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

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Create SNS Topic

1. Go to SNS Console
2. Click **Create Topic**
3. Choose:

   * Type: Standard
   * Name: `devops-alerts`

---

## 🔹 Step 2: Create Subscription

1. Open the topic
2. Click **Create Subscription**

### Configure:

* Protocol: Email
* Endpoint: Your email address

👉 Confirm subscription from your email 📧

---

## 🔹 Step 3: Publish Message (Test)

1. Inside Topic → Click **Publish Message**
2. Add:

   * Subject: Test Alert
   * Message: "Hello from SNS Demo"

👉 Check your email — you’ll receive it instantly 🚀

---

## 🔹 Step 4: Integrate with CloudWatch 🚨

Use:
👉 Amazon CloudWatch

### Steps:

1. Go to CloudWatch → Alarms
2. Create alarm:

   * Metric: EC2 CPUUtilization
   * Threshold: > 70%
3. Select SNS Topic:

   * `devops-alerts`

---

## 🔹 Step 5: Generate Load (Trigger Alert)

SSH into EC2:

```bash id="1x9c9e"
sudo yum install -y stress
stress --cpu 2 --timeout 300
```

---

## 🔍 Observe:

* CPU increases 📈
* Alarm triggers
* SNS sends email 📧

🔥 Full automation working!

---

## 🔹 Step 6: Advanced 

The following are mostly commonly use subscribers:

* Email
* SMS
* Lambda function

👉 One message → multiple endpoints

---

# 🧠 Real-World Use Cases

* Server alerts (CPU, memory)
* Deployment notifications
* Security alerts
* Order notifications (e-commerce)
