# What is AWS CodeBuild?

**AWS CodeBuild** is a **fully managed CI (Continuous Integration) service** from
**Amazon Web Services**.

👉 It helps you:

* Compile code
* Run tests
* Build artifacts
* Prepare apps for deployment

---

# Key Idea

👉 Instead of building manually:

```id="cb1"
Developer → Push Code → CodeBuild → Build & Test → Output
```

---

# Why CodeBuild is Important?

* No build server needed
* Auto scaling
* Pay per build
* Works with CI/CD pipelines

---

# 🧪 Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Create Source Code

Use:
👉 AWS CodeCommit

Inside your repo, create:

### 📄 `index.html`

```html id="cb2"
<h1>Hello from CodeBuild 🚀</h1>
```

---

## 🔹 Step 2: Create `buildspec.yml`

👉 This file tells CodeBuild what to do

```yaml id="cb3"
version: 0.2

phases:
  install:
    commands:
      - echo Installing dependencies...

  build:
    commands:
      - echo Build started
      - mkdir output
      - cp index.html output/

artifacts:
  files:
    - output/**/*
```

---

## 🔹 Step 3: Create CodeBuild Project

1. Go to CodeBuild
2. Click **Create Build Project**

### Configure:

* Project name: `devops-build-demo`

### Source:

* Provider: CodeCommit
* Select your repo

### Environment:

* Managed image
* OS: Linux
* Runtime: Standard

---

## 🔹 Step 4: Configure Buildspec

* Choose: **Use buildspec.yml**

---

## 🔹 Step 5: Start Build 🚀

* Click **Start Build**

---

## 🔍 Observe:

* Build phases running:

  * INSTALL
  * BUILD
* Logs showing in real-time

👉 At end:

* Build succeeds ✅
* Artifact created

---

## 🔹 Step 6: View Output

* Go to **Artifacts**
* Download output

👉 You’ll see:

```id="cb4"
output/index.html
```

🔥 Your build pipeline is working!

---

# 🚀 Advanced Demo (Real DevOps Flow)

## 🔹 Integrate with Pipeline

Use:

* AWS CodePipeline

Flow:

```id="cbflow"
CodeCommit → CodeBuild → Deploy (S3 / EC2 / Kubernetes)
```

---

## 🔹 Example Use Case

👉 Node.js / Laravel project:

* Push code
* CodeBuild:

  * Install dependencies
  * Run tests
  * Build Docker image

🔥 This is real CI/CD

---

# 🧠 Real-World Use Cases

* Build web apps
* Run automated tests
* Create Docker images
* Prepare deployment artifacts

---
