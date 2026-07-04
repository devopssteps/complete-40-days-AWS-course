# 🚀 What is Infrastructure as Code (IaC)?

👉 **Infrastructure as Code (IaC)** means:

* Instead of manually creating resources
* You **define everything in code (YAML/JSON)**

---

# ☁️ What is CloudFormation?

**AWS CloudFormation** is a service from
**Amazon Web Services** that lets you:

👉 Create and manage AWS resources using templates

---

# 🎯 Key Idea

```id="cf1"
Template (YAML/JSON) → CloudFormation → AWS Resources Created Automatically
```

---

# 🔥 Why CloudFormation is Important?

* Automation
* Consistency
* Version control
* Easy to replicate environments

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Create CloudFormation Template

Create a file:

### 📄 `template.yaml`

```yaml id="cf2"
AWSTemplateFormatVersion: '2010-09-09'
Description: Simple EC2 instance using CloudFormation

Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0f58b397bc5c1f2e8  # (Update for your region)
      SecurityGroups:
        - default
```

---

## 🔹 Step 2: Create Stack

1. Go to CloudFormation
2. Click **Create Stack**
3. Upload your `template.yaml`

---

## 🔹 Step 3: Configure Stack

* Stack name: `devops-stack`
* Leave default options

👉 Click **Create**

---

## 🔍 Observe:

* Stack creation starts
* Resources are created automatically

---

## 🔹 Step 4: Verify EC2 Instance

Go to:
👉 Amazon EC2

👉 You’ll see EC2 instance created 🎉

---

## 🔹 Step 5: Update Stack (Important)

Modify template:

```yaml id="cf3"
InstanceType: t2.small
```

👉 Update stack

---

## 🔥 Result:

* Instance updated automatically
* No manual change needed

---

## 🔹 Step 6: Delete Stack

👉 Click **Delete Stack**

🔥 All resources are deleted automatically

---

# 🚀 Advanced Demo (Real DevOps Use)

## 🔹 Create Full Infrastructure

Using CloudFormation:

* VPC
* Subnets
* EC2
* Load Balancer

---

## 🔹 Real Architecture

```id="cf4"
CloudFormation Template →
    VPC + EC2 + Load Balancer →
        Production Environment
```

---

# 🧠 Real-World Use Cases

* Dev/Test/Prod environment setup
* CI/CD infrastructure
* Disaster recovery
* Multi-region deployment

---
