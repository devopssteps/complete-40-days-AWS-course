# 🚀 What is CI/CD Pipeline?

👉 CI/CD = **Continuous Integration + Continuous Deployment**

* **CI** → Build & test code automatically
* **CD** → Deploy code automatically

---

# 🎯 AWS CI/CD Pipeline Overview

We will use:

* AWS CodeCommit → Store code
* AWS CodeBuild → Build
* AWS CodeDeploy → Deploy
* AWS CodePipeline → Orchestrate

---

# 🏗️ Architecture (Real DevOps Flow)

```id="cicd1"
Developer → CodeCommit → CodeBuild → CodeDeploy → EC2 → Live Website
```

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Launch EC2 Server

Use:
👉 Amazon EC2

* Amazon Linux 2
* Open ports: 22, 80

---

## 🔹 Step 2: Install CodeDeploy Agent

```bash id="cicd2"
sudo yum update -y
sudo yum install ruby -y
sudo yum install wget -y

cd /home/ec2-user
wget https://aws-codedeploy-ap-south-1.s3.ap-south-1.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto

sudo service codedeploy-agent start
```

---

## 🔹 Step 3: Prepare Code Repository

Use:
👉 AWS CodeCommit

### 📄 index.html

```html id="cicd3"
<h1>Welcome to DevOps CI/CD Pipeline 🚀</h1>
```

---

### 📄 buildspec.yml

```yaml id="cicd4"
version: 0.2

phases:
  build:
    commands:
      - echo "Building project..."

artifacts:
  files:
    - '**/*'
```

---

### 📄 appspec.yml

```yaml id="cicd5"
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

### 📄 scripts/start.sh

```bash id="cicd6"
#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
```

---

## 🔹 Step 4: Create CodeBuild Project

Use:
👉 AWS CodeBuild

* Source: CodeCommit
* Use `buildspec.yml`

---

## 🔹 Step 5: Setup CodeDeploy

Use:
👉 AWS CodeDeploy

* Create Application
* Create Deployment Group
* Select EC2 instance

---

## 🔹 Step 6: Create CodePipeline 🚀

Use:
👉 AWS CodePipeline

### Add stages:

1. **Source** → CodeCommit
2. **Build** → CodeBuild
3. **Deploy** → CodeDeploy

---

## 🔹 Step 7: Run Pipeline

👉 Pipeline triggers automatically

---

## 🔍 Observe:

* Code fetched
* Build executed
* App deployed

---

## 🔹 Step 8: Test Application 🌐

Open EC2 Public IP:

```id="cicd7"
Welcome to DevOps CI/CD Pipeline 🚀
```

---

## 🔹 Step 9: Auto Deployment Demo (🔥 MUST SHOW)

Change code:

```html id="cicd8"
<h1>Pipeline Updated Automatically 🔥</h1>
```

👉 Push to repo

---

## 🔥 Result:

* Pipeline auto triggers
* Website updates automatically

👉 This is **REAL CI/CD**

---

# 🧠 Real-World Use Cases

* Automated deployments
* Microservices pipelines
* Production release automation
* DevOps workflows

---
