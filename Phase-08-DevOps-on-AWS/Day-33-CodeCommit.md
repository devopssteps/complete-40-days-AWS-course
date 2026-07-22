# What is AWS CodeCommit?

**AWS CodeCommit** is a **fully managed Git repository service** from
**Amazon Web Services**.

👉 It is similar to:

* GitHub
* GitLab

---

# Key Idea

👉 Store your code securely in AWS

👉 Developers can:

* Push code
* Pull code
* Collaborate

---

# Why CodeCommit is Important?

* Private Git repos (secure)
* Integrated with AWS services
* No need external tools
* Perfect for CI/CD pipelines

---

# Hands-On Demo (Step-by-Step)

## 🔹 Step 1: Create Repository

1. Go to CodeCommit
2. Click **Create Repository**

### Fill:

* Name: `devops-repo`
* Description: DevOps demo repo

---

## 🔹 Step 2: Setup Git Credentials

👉 Go to IAM → Users → Security Credentials

* Generate HTTPS Git credentials

---

## 🔹 Step 3: Clone Repository

On your local machine:

```bash id="cc1"
git clone https://git-codecommit.ap-south-1.amazonaws.com/v1/repos/devops-repo
cd devops-repo
```

---

## 🔹 Step 4: Add Code

Create file:

```bash id="cc2"
echo "Hello from CodeCommit" > index.html
```

---

## 🔹 Step 5: Commit & Push

```bash id="cc3"
git add .
git commit -m "Initial commit"
git push
```

👉 Now code is stored in CodeCommit

---

## 🔹 Step 6: Verify in Console

* Go back to CodeCommit
* Open repo

👉 You’ll see your file 🎉

---

# 🚀 Advanced Demo (DevOps Flow)

## 🔹 Integrate with CI/CD

Use:

* AWS CodePipeline
* AWS CodeBuild

---

## 🔹 Real Flow:

```id="ccflow"
Developer → CodeCommit → CodePipeline → Build → Deploy
```

---

## 🔹 Example Use Case

👉 Laravel / Node.js project:

* Push code → CodeCommit
* Pipeline triggers → Deploy automatically

🔥 This is real DevOps automation

---

# 🧠 Real-World Use Cases

* Store application code
* CI/CD pipelines
* Team collaboration
* Infrastructure as Code (Terraform)

---

# Configure the git commit by doing the following setps

```bash
aws configure
```

Then:

```bash
aws sts get-caller-identity
```

Configure Git:

```bash
git config --global credential.helper '!aws codecommit credential-helper $@'
```

```bash
git config --global credential.UseHttpPath true
```

Clone:

```bash
git clone https://git-codecommit.us-east-2.amazonaws.com/v1/repos/cloudops
```

Go inside:

```bash
cd cloudops
```

Check remote:

```bash
git remote -v
```

Check branch:

```bash
git branch --show-current
```

Create a file:

```bash
echo "Hello AWS CodeCommit" > index.html
```

Check status:

```bash
git status
```

Add:

```bash
git add .
```

Commit:

```bash
git commit -m "Add index HTML file"
```

Push:

```bash
git push origin main
```

---

## ⚠️ Important: Don't Run `git init`
