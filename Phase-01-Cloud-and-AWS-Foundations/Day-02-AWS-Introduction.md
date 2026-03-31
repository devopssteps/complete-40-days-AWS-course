# Complete 40 days AWS Course (day 2) - Introduction to AWS 


---

# We will discussed the following Topics

 - Introduction to AWS 
 - AWS Global Infrastructure 
 - Regions & Availability Zones (Hands-on) 
 - Create AWS Account
 - AWS Free Tier
 - MFA Setup (Hands-on)
 - Budget setup (Hands-on)
 
Platform we are learning:

Amazon Web Services

---

# 1. Introduction to AWS


**Definition**

> AWS is a cloud platform that provides computing services such as servers, storage, networking, databases, and security over the internet.

Provider:

Amazon Web Services

AWS launched in **2006** and now offers **200+ services**.

Examples of popular services:

* Amazon EC2 – virtual servers
* Amazon S3 – object storage
* Amazon RDS – managed database
* AWS Lambda – serverless computing

Explain simply:

Instead of buying physical servers, companies rent infrastructure from AWS.

Example companies using AWS:

* Netflix
* Airbnb
* Spotify

---

# 2. AWS Global Infrastructure

AWS runs **data centers worldwide**.

AWS global infrastructure consists of:

* 1️⃣ Regions
* 2️⃣ Availability Zones
* 3️⃣ Edge Locations

AWS infrastructure is designed for:

* ✔ High availability
* ✔ Fault tolerance
* ✔ Low latency

---

# 3. What is an AWS Region?

Definition:

> A Region is a **geographical area** where AWS has multiple data centers.

Example regions:

* US East (Virginia)
* Europe (London)
* Asia Pacific (Singapore)

Example region names:

```
us-east-1
eu-west-2
ap-southeast-1
```

Each region is **completely isolated** from others.

Benefits:

* ✔ Disaster recovery
* ✔ Data compliance
* ✔ Low latency

---

# 4. What is an Availability Zone?

Definition:

> An Availability Zone (AZ) is one or more data centers inside a region.

Example:

Region:

```
us-east-1
```

Availability Zones:

```
us-east-1a
us-east-1b
us-east-1c
```

Each AZ has:

* Independent power
* Independent networking
* Separate data center buildings

This design ensures **high availability**.

---

# 5. Example Architecture

Explain with a real example.

If you deploy your application in:

Region

```
us-east-1
```

You can run servers in:

```
us-east-1a
us-east-1b
```

If one data center fails, the other continues running.

This is how companies achieve **99.99% uptime**.

---

# 6. Hands-on Demo (Very Important)

Now show a practical demo.

Open the AWS console:

```
https://console.aws.amazon.com
```

Login to your account.

---

## Step 1 — Check Current Region

Look at the **top right corner**.

Example:

```
US East (N. Virginia)
```

Explain that this is your **current AWS Region**.

---

## Step 2 — Switch Region

Click the region dropdown.

Show regions like:

* US East
* Asia Pacific
* Europe

Select:

```
Asia Pacific (Singapore)
```

Explain:

Now your resources will be created in this region.

---

## Step 3 — Open EC2 Dashboard

Search for:

Amazon EC2

Click **EC2 Dashboard**.

Then click:

```
Launch Instance
```

---

## Step 4 — Check Availability Zone

Scroll to **Network Settings**.

You will see:

```
Availability Zone
```

Example:

```
ap-southeast-1a
```

Explain:

This means your server will run inside that **specific data center**.

---

## Step 5 — Launch Server (Optional Demo)

Configuration example:

Name

```
aws-demo-server
```

AMI

```
Amazon Linux
```

Instance type

```
t2.micro
```

Click:

```
Launch Instance
```

Explain:

Your server is now running inside an **AWS Availability Zone**.

---

# 7. Region Selection Best Practice

Explain how companies choose regions.

Factors:

* ✔ User location
* ✔ Compliance laws
* ✔ Latency
* ✔ Disaster recovery

Example:

If your users are in Asia → choose

```
ap-southeast-1
```

---

# 8. Real World Example

Example architecture:

Application deployed in

```
ap-south-1
```

Servers running in

```
ap-south-1a
ap-south-1b
```

If AZ-A fails → AZ-B keeps running.

This is called **High Availability Architecture**.

---

# 9. DevOps Perspective

DevOps engineers use regions and AZs for:

* ✔ High availability
* ✔ Auto scaling
* ✔ Load balancing
* ✔ Disaster recovery

Example AWS services used:

* Elastic Load Balancing
* Amazon EC2 Auto Scaling

---
