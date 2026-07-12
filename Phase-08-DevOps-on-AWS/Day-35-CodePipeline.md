# 🚀 What is AWS CodePipeline?

**AWS CodePipeline** is a service from
**Amazon Web Services** that helps you:

👉 Automate the **entire CI/CD pipeline**

---

# 🎯 Key Idea

```id="cp1"
Code → Build → Deploy → Live Application
```

👉 CodePipeline connects everything automatically

---

# 🔥 Services Used in Pipeline

* AWS CodeCommit → Source
* AWS CodeBuild → Build
* AWS CodeDeploy → Deploy

---

# 🏗️ Architecture Overview

```id="cp2"
CodeCommit → CodeBuild → CodeDeploy → EC2
```

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Prepare Code Repository

Use:
👉 AWS CodeCommit

### Add files:

📄 `index.html`

```html id="cp3"
<h1>CI/CD Pipeline Working 🚀</h1>
```

📄 `buildspec.yml`

```yaml id="cp4"
version: 0.2

phases:
  build:
    commands:
      - echo "Building project"

artifacts:
  files:
    - '**/*'
```

📄 `appspec.yml`

```yaml id="cp5"
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

📄 `scripts/start.sh`

```bash id="cp6"
#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
```

---

## 🔹 Step 2: Create CodeBuild Project

Use:
👉 AWS CodeBuild

* Source: CodeCommit
* Use `buildspec.yml`

---

## 🔹 Step 3: Setup CodeDeploy

Use:
👉 AWS CodeDeploy

* Create Application
* Create Deployment Group
* Connect EC2 instance

---

## 🔹 Step 4: Create CodePipeline 🚀

Go to CodePipeline → Create pipeline

### Configure:

### 🔹 Source Stage

* Provider: CodeCommit
* Select repo

---

### 🔹 Build Stage

* Provider: CodeBuild
* Select project

---

### 🔹 Deploy Stage

* Provider: CodeDeploy
* Select application + group

---

## 🔹 Step 5: Run Pipeline

👉 Pipeline will start automatically

---

## 🔍 Observe:

* Source → Fetch code
* Build → Run build
* Deploy → Deploy to EC2

---

## 🔹 Step 6: Test Output 🌐

Open EC2 public IP:

```id="cp7"
CI/CD Pipeline Working 🚀
```

🔥 Full pipeline working!

---

## 🔹 Step 7: Make Change (Important Demo)

Edit file:

```html id="cp8"
<h1>Pipeline Updated Automatically 🔥</h1>
```

👉 Push to CodeCommit

---

## 🔥 Observe:

* Pipeline triggers automatically
* New version deployed

👉 This is **real CI/CD automation**

---

# 🧠 Real-World Use Cases

* Automated deployments
* CI/CD pipelines
* Microservices delivery
* Continuous integration

---
