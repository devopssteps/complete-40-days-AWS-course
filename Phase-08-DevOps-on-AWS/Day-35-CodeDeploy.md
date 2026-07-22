# 🚀 What is AWS CodeDeploy?

**AWS CodeDeploy** is a service from
**Amazon Web Services** that helps you:

👉 Automatically **deploy applications** to:

* EC2
* On-prem servers
* Lambda

---

# 🎯 Key Idea

```id="cd1"
CodeBuild → CodeDeploy → EC2 (Application Updated)
```

👉 Instead of manual deployment:

* CodeDeploy handles everything automatically ⚡

---

# 🔥 Why CodeDeploy is Important?

* Zero downtime deployments
* Automated rollbacks
* Easy integration with CI/CD
* Supports Blue/Green deployment

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Launch EC2 Instance

Use:
👉 Amazon EC2

### Configure:

* Amazon Linux 2
* t2.micro
* Allow HTTP (80) & SSH (22)

---

## 🔹 Step 2: Install CodeDeploy Agent

SSH into EC2:

```bash id="cd2"
sudo yum update -y
sudo yum install ruby -y
sudo yum install wget -y

cd /home/ec2-user
wget https://aws-codedeploy-ap-south-1.s3.ap-south-1.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto

sudo service codedeploy-agent start
```

👉 Verify:

```bash id="cd3"
sudo service codedeploy-agent status
```

---

## 🔹 Step 3: Create Application in CodeDeploy

* Go to CodeDeploy
* Click **Create Application**

### Configure:

* Name: `devops-app`
* Compute platform: EC2

---

## 🔹 Step 4: Create Deployment Group

* Select EC2 instances
* Use tag or manually select instance

👉 Set:

* Deployment type: In-place

---

## 🔹 Step 5: Prepare Application Code

Use:
👉 AWS CodeCommit

### Create files:

### 📄 `index.html`

```html id="cd4"
<h1>Welcome to CodeDeploy 🚀</h1>
```

---

### 📄 `appspec.yml`

```yaml id="cd5"
version: 0.0
os: linux

files:
  - source: /
    destination: /var/www/html

hooks:
  ApplicationStart:
    - location: scripts/start.sh
      timeout: 300
      runas: root
```

---

### 📄 `scripts/start.sh`

```bash id="cd6"
#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
```

👉 Make executable:

```bash id="cd7"
chmod +x scripts/start.sh
```

---

## 🔹 Step 6: Create Deployment

* Go to CodeDeploy → Create Deployment
* Select:

  * Application
  * Deployment group
  * Source: CodeCommit

---

## 🔍 Observe:

* Deployment starts 🚀
* Files copied to EC2
* Script runs
* Apache starts

---

## 🔹 Step 7: Test Application 🌐

* Open EC2 Public IP

👉 Output:

```id="cd8"
Welcome to CodeDeploy 🚀
```

🔥 Your deployment is successful!

---

# 🚀 Advanced Demo (Real DevOps Flow)

## 🔹 Full CI/CD Pipeline

Use:

* AWS CodeBuild
* AWS CodePipeline

---

## 🔹 Flow:

```id="cdflow"
CodeCommit → CodeBuild → CodeDeploy → EC2
```

---

## 🔹 Blue/Green Deployment (Important)

👉 Benefits:

* Zero downtime
* Safe rollback

---

# 🧠 Real-World Use Cases

* Deploy web apps automatically
* Zero downtime deployments
* Production release automation
* Microservices deployment

---
