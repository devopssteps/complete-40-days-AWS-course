# API Gateway + AWS Lambda — Hands-on demo 

![API GateWay](https://github.com/devopssteps/complete-40-days-AWS-course/blob/main/Phase-05-Serverless-and-Modern-AWS/api-gateway-with-lambda.png)

### What is API
An API, which stands for Application Programming Interface, is a software intermediary that allows two different applications to talk to each other.In simple terms, 
it acts as a messenger that takes your request, tells a system what you want to do, and then returns the response back to you


# What is API Gateway
**AWS Lambda** is serverless compute — you write a function, AWS runs it on demand. No servers to manage, you pay only when it executes.

**API Gateway** sits in front of Lambda as the HTTP layer — it receives HTTP requests from the internet, triggers your Lambda function, and returns the response. Together they form a complete serverless API.Now let's build a real working API step by step.

---
# 🎯 Concept

👉 API Gateway acts like a **front door** 🚪

```id="api1"
Client (Browser/Postman) → API Gateway → Lambda → Response
```
---

# 🔥 Why API Gateway is Important?

* Build REST APIs easily
* Connect frontend to backend
* Secure and scalable
* Works perfectly with **AWS Lambda**

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Create Lambda Function

Go to Lambda → Create Function

Now replace the default code with this:

```python id="apicode1"
def lambda_handler(event, context):
    name = event.get('queryStringParameters', {}).get('name', 'Guest')
    
    return {
        'statusCode': 200,
        'body': f'Hello {name}, welcome to API Gateway 🚀'
    }
```

👉 Click **Deploy**

---

### Step 2 — Test Lambda Directly

Before connecting API Gateway, test Lambda alone:

1. Click **Test** tab → **Create new test event**
2. Paste this test payload:
  ```sh
name=rajiv
```
3. Click **Test** — you should see:
```sh
Hello rajiv, welcome to API Gateway 🚀'
```
✅ Lambda is working. Now connect API Gateway.

### Step 3 — Create API Gateway

1. Go to **API Gateway → Create API**
2. Choose **REST API** → click **Build**
3. Settings:
   - Select New API
   - API name : `my-api`
   - Security Policy: SecurityPolicy_TLS13_1_2_2021_06
   - Endpoint type: **Regional**
5. Click **Create API**

---

### Step 4 — Create Method
Setting:
   * Method type : Select Get
   * Choose : Lambda Function
   * Enable : Lambda proxy integration
   * Lambda function:  Select your created lambda function
   * Click Create Method

### Step 5 — Test API Gateway
   * Click Test Tab
   * Query strings type : name=rajiv
   * Click Test and we can see the message "Hello rajiv, welcome to API Gateway" 


### Step 6: Deploy API Gateway
   * Click Deploy API - If deploy API not enable then refresh or back
   * Stage : Select New Stage
   * Stage name: dev
   * click Deploy
   * copy the URL like https://krld7h0vs1.execute-api.us-east-1.amazonaws.com/dev
   * Now pest it to browser and pass a quesry string like ?name=rajiv ( https://krld7h0vs1.execute-api.us-east-1.amazonaws.com/dev?name=rajiv)
   * Now we can see the message in browser - if right way message not showing propery wait 30 sec

### Step 7: Create resources
   * Resource path : /
   * Resource name : dhaka
   * Same way create a method with new lambda function
   * Now browse ( https://krld7h0vs1.execute-api.us-east-1.amazonaws.com/dev/dhaka?name=siddiqui)

### Check the log 
  * Add pring(event) in function
  * Now browse it and then go to monitor and check cloudwatch log





