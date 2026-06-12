# Create Your First AWS Lambda Function 

## 🔹 What is Lambda?

**AWS Lambda** is a service from
**Amazon Web Services** where you can:

👉 Run code **without managing servers**

---

## 🎯 Key Idea

👉 Traditional way:

* Launch server
* Install software
* Maintain it

👉 Lambda way:

* Write code
* Deploy
* Run instantly ⚡

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Go to Lambda Console

* Login to AWS
* Search → **Lambda**
* Click **Create Function**

---

## 🔹 Step 2: Create Function

### Choose:

* **Author from scratch**

### Fill:

* Function name: `my-first-lambda`
* Runtime: Python 3.x

👉 Click **Create Function**

---

## 🔹 Step 3: Write Your First Code

You’ll see default code. Replace with this:

```python id="g5k1eh"
def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Hello Rajiv! This is your first Lambda 🚀'
    }
```

👉 Click **Deploy**

---

## 🔹 Step 4: Test Your Function

1. Click **Test**
2. Create test event (default is fine)
3. Click **Test again**

---

## 🔍 Output:

```json id="ngux1k"
{
  "statusCode": 200,
  "body": "Hello Rajiv! This is your first Lambda 🚀"
}
```

🔥 Congratulations — your first serverless app is running!

---

## 🔹 Step 5: View Logs

Use:
👉 Amazon CloudWatch

Steps:

* Click **Monitor → View logs in CloudWatch**

👉 You’ll see execution logs

---

## 🔹 Step 6: Add Event Input (Important)

Modify code:

```python id="fryir6"
def lambda_handler(event, context):
    name = event.get('name', 'Guest')
    
    return {
        'statusCode': 200,
        'body': f'Hello {name}, welcome to Lambda!'
    }
```

### Test Event:

```json id="4nf7sn"
{
  "name": "Rajiv"
}
```

👉 Output becomes dynamic 🔥

---

# 🚀 Mini Real-World Example

👉 Use Lambda to:

* Process API requests
* Handle alerts from SNS
* Automate DevOps tasks

---
