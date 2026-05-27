# Day-22: SQS with hands on demo

# 🚀 What is SQS?

**Amazon Simple Queue Service (SQS)** is a **fully managed message queue service** in
**Amazon Web Services**.

👉 It allows systems to:

* Send messages 📩
* Store them in a queue
* Process them later (asynchronously)

---

# 🎯 Key Concept (Very Important)

## 📦 Queue-Based Architecture

```id="j55c1g"
Producer (App) → SQS Queue → Consumer (Worker)
```

* **Producer** → sends message
* **Queue** → holds message
* **Consumer** → processes message

---

# 🔥 Why SQS is Important?

* Decouples services
* Handles traffic spikes
* Improves reliability
* Prevents system crashes

---

# 🧠 Real-Life Example

👉 E-commerce order system:

* User places order
* App sends message to SQS
* Worker processes:

  * Payment
  * Email
  * Inventory

🔥 Even if system is busy → no data loss

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Create SQS Queue

1. Go to SQS Console
2. Click **Create Queue**

### Configure:

* Type: Standard
* Name: `devops-queue`

---

## 🔹 Step 2: Send Message (Producer)

1. Open queue
2. Click **Send Message**

Example message:

```json id="y9ryux"
{
  "order_id": "12345",
  "user": "rajiv",
  "action": "process_order"
}
```

👉 Message is now stored in queue

---

## 🔹 Step 3: Receive Message (Consumer)

1. Click **Poll for messages**
2. Select message → View

👉 This simulates worker processing

---

## 🔹 Step 4: Delete Message

👉 After processing:

* Click **Delete message**

🔥 Important:
If not deleted → message returns to queue

---
