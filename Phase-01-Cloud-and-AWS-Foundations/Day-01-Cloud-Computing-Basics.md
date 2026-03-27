# Complete 40 days AWS Course (day 1)


### Todays class topics:
 - What is Cloud Computing?
 - Cloud Computing Concept
 - Key Characteristics of Cloud
 - Hands-on Demo (Create First Cloud Server)
 - IaaS vs PaaS vs SaaS
 - Public vs Private vs Hybrid Cloud
 - Real World Example
 - DevOps Perspective
---

# 1. What is Cloud Computing?

### Simple Definition

Cloud computing means:

> **Using computing resources (servers, storage, networking, databases) over the internet instead of owning physical hardware.**

Instead of buying a server, you **rent it from a cloud provider**.

### Traditional Infrastructure (Before Cloud)

Company needed to buy:

* Physical Servers
* Storage
* Networking devices
* Data center space
* Cooling & electricity
* IT engineers

Problems:

* Very expensive
* Slow to scale
* Maintenance required

---

# 2. Cloud Computing Concept

Cloud providers like:

* Amazon Web Services
* Microsoft Azure
* Google Cloud Platform

provide infrastructure **on demand**.

Advantages:

  - ✔ Pay only for what you use
  - ✔ Launch servers in minutes
  - ✔ Global infrastructure
  - ✔ High availability
  - ✔ Auto scaling

Example:

Instead of buying a $10,000 server you can launch one in AWS for **$0.01/hour**.

---

# 3. Key Characteristics of Cloud

These 5 are very important for interviews:

1️⃣ **On-Demand Self Service**
Create servers anytime.

2️⃣ **Broad Network Access**
Access from anywhere.

3️⃣ **Resource Pooling**
Cloud provider shares infrastructure.

4️⃣ **Rapid Elasticity**
Scale up/down instantly.

5️⃣ **Pay As You Go**

---

# 4. Hands-on Demo (Create First Cloud Server)

A simple AWS demo.

Platform:
Amazon Web Services

Service:
Amazon EC2

### Step 1

Login to AWS

```
https://console.aws.amazon.com
```

---

### Step 2

Search

```
EC2
```

Open **EC2 Dashboard**

---

### Step 3

Click

```
Launch Instance
```

---

### Step 4

Configure

Name:

```
my-first-cloud-server
```

AMI

```
Amazon Linux
```

Instance type

```
t2.micro (Free tier)
```

---

### Step 5

Create Key Pair

```
aws-demo-key
```

Download `.pem`

---

### Step 6

Security Group

Allow

```
SSH (22)
HTTP (80)
```

---

### Step 7

Launch Instance

Wait 30 seconds.

---

### Step 8

Connect to server

```
ssh -i aws-demo-key.pem ec2-user@PUBLIC-IP
```

Now show command:

```
hostname
uptime
df -h
```

> This server is running in **AWS cloud data center**, not on your laptop.

---

# 5. IaaS vs PaaS vs SaaS

These are **three cloud service models**.

---

# IaaS (Infrastructure as a Service)

Definition:

Provider gives **virtual machines, storage, networking**.

You manage:

* OS
* Applications
* Security
* Runtime

Examples:

* Amazon EC2
* Amazon EBS
* DigitalOcean

Diagram explanation for video:

```
You manage
Application
Runtime
OS
----------------
Provider manages
Network
Storage
Server
```

---

# PaaS (Platform as a Service)

Provider manages **infrastructure + OS + runtime**.

You only deploy code.

Examples:

* AWS Elastic Beanstalk
* Heroku
* Google App Engine

Example demo explanation:

Deploy application without managing server.

---

# SaaS (Software as a Service)

Users access **ready-made software via browser**.

No infrastructure management.

Examples:

* Google Workspace
* Salesforce
* Dropbox

Example:

```
Gmail
Google Docs
Zoom
```

---

# 6. Comparison Table

| Feature        | IaaS           | PaaS              | SaaS           |
| -------------- | -------------- | ----------------- | -------------- |
| Infrastructure | Cloud provider | Cloud provider    | Cloud provider |
| OS             | You manage     | Provider          | Provider       |
| Runtime        | You manage     | Provider          | Provider       |
| Application    | You            | You               | Provider       |
| Example        | EC2            | Elastic Beanstalk | Gmail          |

---

# 7. Public vs Private vs Hybrid Cloud

---

# Public Cloud

Infrastructure shared by many companies.

Example:

* Amazon Web Services
* Microsoft Azure
* Google Cloud Platform

Advantages:

 - ✔ Cheap
 - ✔ Highly scalable
 - ✔ No maintenance

---

# Private Cloud

Cloud dedicated to **one organization**.

Example:

Bank running cloud in their own data center.

Technologies:

* OpenStack
* VMware vSphere

Advantages:

 - ✔ High security
 - ✔ Full control

Disadvantages:

❌ Expensive

---

# Hybrid Cloud

Combination of **public + private cloud**.

Example:

Bank data in private cloud
Website in AWS.

Example technologies:

* VMware Cloud
* AWS Outposts

Advantages:

 - ✔ Flexibility
 - ✔ Security
 - ✔ Cost optimization

---

# 8. Real World Example

Netflix architecture.

Runs on:

Netflix using Amazon Web Services

Millions of users watch movies without owning servers.

---

# 9. DevOps Perspective

Why cloud is important for DevOps:

 - ✔ Infrastructure automation
 - ✔ CI/CD pipelines
 - ✔ Kubernetes clusters
 - ✔ Monitoring
 - ✔ Scalability

Tools you will later use:

* Terraform
* Kubernetes
* Docker
* Jenkins

---
