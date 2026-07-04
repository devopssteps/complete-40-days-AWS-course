## What is Amazon Elastic Beanstalk?

Elastic Beanstalk (EB) is AWS's Platform-as-a-Service (PaaS). You give it your application code, and it automatically handles everything underneath — EC2 instances, load balancers, auto scaling, health monitoring, deployments. Think of it as the middle ground between managing your own EC2 servers and going fully serverless with Lambda.Click any component in the diagram to ask more about it. Now let's walk through the full hands-on demo.

---
![Elastic Beanstalk Architecture](https://github.com/devopssteps/complete-40-days-AWS-course/blob/main/Phase-05-Serverless-and-Modern-AWS/elastic_beanstalk_architecture.svg)
---

## 🛠️ Hands-On Demo — Deploy a Node.js App on Elastic Beanstalk

## First we will see the deployment from web console

### Step 1: Create Your Application 
Create a folder and inside that folder Create these following 2 files 
```sh
mkdir my-beanstalk-app && cd my-beanstalk-app
```
---
```app.js```
```sh
const http = require('http');

const PORT = process.env.PORT || 3000;

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/html' });
  res.end(`
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <title>Hello World</title>
      <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
          font-family: -apple-system, Segoe UI, Arial, sans-serif;
          background: #0f172a;
          display: flex;
          align-items: center;
          justify-content: center;
          height: 100vh;
        }
        .card {
          background: #1e293b;
          border: 1px solid #334155;
          border-radius: 16px;
          padding: 48px 64px;
          text-align: center;
        }
        h1 { color: #38bdf8; font-size: 48px; margin-bottom: 12px; }
        p  { color: #94a3b8; font-size: 18px; }
        .badge {
          display: inline-block;
          margin-top: 20px;
          background: #0ea5e9;
          color: #fff;
          padding: 4px 14px;
          border-radius: 20px;
          font-size: 13px;
        }
      </style>
    </head>
    <body>
      <div class="card">
        <h1>Hello, World!</h1>
        <p>Running on Node.js — no frameworks, no dependencies.</p>
        <span class="badge">Port ${PORT}</span>
      </div>
    </body>
    </html>
  `);
});

server.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`);
});
```
```package.json```
```sh
{
  "name": "hello-node",
  "version": "1.0.0",
  "description": "Simple Hello World Node.js app",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "engines": {
    "node": ">=18.0.0"
  }
}
```
---
## Step 2 : Run it locally first

You need Node.js installed. Check with `node -v` — if nothing shows, download from nodejs.org.

```bash
# 1. Enter the folder
cd hello-node

# 2. Start the server
npm start

# 3. Open your browser
# → http://localhost:3000
```

You'll see the "Hello, World!" page. Press `Ctrl + C` to stop it.

---
# Now Deploy to AWS Elastic Beanstalk from Web console
### For upload to beanstalk we need to compress this two file like ```app.zip```

### Step 1: Navigate to Elastic Beanstalk
 1. Log in to your AWS Management Console.
 2. In the top search bar, type Elastic Beanstalk and select it to open the dashboard.

### Step 2: Create an Application
 1. On the Elastic Beanstalk dashboard, click Create Application.
 2. Application Information: Enter a name for your application (e.g., my-first-app).
 3. Platform: Choose the runtime environment that matches your application's programming language or framework (e.g., Python, Node.js, Java, PHP, Docker). The console automatically selects the latest recommended version and branch.
 4. Application code: 
     - To test the service, select Sample application.
     - To deploy your own app, choose Upload your code and provide the .zip or .war bundle for your project.

### Step 3: Configure Environment Details
 1. Environment tier: Leave this set to Web server environment (this is for HTTP-based apps; the Worker environment is reserved for background tasks).
 2. Environment name: This auto-populates based on your application name. You can customize it if needed.
 3. Domain: (Optional) Enter a custom subdomain. If you leave it blank, AWS will auto-generate a unique URL (e.g., http://elasticbeanstalk.com).

### Step 4: Configure Service Access (IAM Roles)
 Elastic Beanstalk needs permission to provision AWS resources on your behalf.
  1. Service role: If you do not have one, select Create and use a new service role. AWS will attach the necessary policies (like AWSElasticBeanstalkEnhancedHealth) to manage your environment.
  2. EC2 instance profile: This grants your EC2 instances permissions to interact with other AWS services. Select Create and use a new instance profile or choose an existing role.


### Step 5: Configure Networking, Database, and Tags (Optional)
 1. Networking: Select your default VPC and enable a public IP address for your EC2 instances so your site is accessible over the internet.
 2. Database: If your application requires a database, you can choose to add an Amazon RDS database directly here. For testing purposes, you can leave this disabled.
 3. Tags: (Optional) Add key-value tags to organize and track your resources (e.g., Project: Production).

### Step 6: Review and Launch
 1. Click Next to review all your configurations.
 2. Ensure everything is correct, then click Submit.
 3. Elastic Beanstalk will redirect you to an event log page. It typically takes 3 to 5 minutes to provision the EC2 instances, security groups, and load balancer.
 4. Once the environment is ready, the dashboard health status will turn green (OK).

### Step 7: Access Your Application
 1. On the main dashboard of your created environment, locate the Domain URL located near the top.
 2. On the main dashboard of your created environment, locate the Domain URL located near the top.

---

## Delete Elastic Beanstalk from AWS Console

**Step 1** — Go to **https://console.aws.amazon.com/elasticbeanstalk**

**Step 2** — In the left sidebar click **"Applications"**

**Step 3** — Tick the checkbox next to your application (e.g. `hello-node`)

**Step 4** — Click **"Actions"** (top right) → **"Delete application"**

**Step 5** — Type the application name to confirm → click **"Delete"**

---

# Now deploy from command line

### Step 1 — Install the EB CLI

```bash
# Mac
brew install awsebcli

# Linux / WSL
pip install awsebcli --upgrade --user

# Verify
eb --version
```
---

### Step 2 — Initialize Elastic Beanstalk

```bash
eb init
```
You'll be prompted:

```
Select a default region: (choose your region, e.g. ap-southeast-1)
Application Name: my-beanstalk-app
Platform: Node.js
Platform branch: Node.js 20 running on 64bit Amazon Linux 2023
SSH keypair: Yes (select or create one)
```

This creates a `.elasticbeanstalk/config.yml` file.

---
### Step 3 — Create the Environment & Deploy

```bash
# Create environment + deploy in one command
eb create my-app-env \
  --instance-type t3.micro \
  --platform "Node.js 20 running on 64bit Amazon Linux 2023"
```

This takes 3–5 minutes. Elastic Beanstalk automatically:
- Creates an EC2 instance
- Sets up a security group
- Creates an Application Load Balancer
- Configures Auto Scaling
- Assigns a public URL

---
### Step 4 — Open Your App

```bash
eb open
```

This opens your browser at something like:
```
http://my-app-env.ap-southeast-1.elasticbeanstalk.com
```

You'll see your website live on the internet — no server management needed!

---

### Step 5 — Monitor Health & Logs

```bash
# Check environment health
eb health

# View live logs
eb logs

# Stream logs in real time
eb logs --all
```

In the AWS console you'll also see the health dashboard with green/yellow/red indicators per instance.

---

### Step 6 — Cleanup (Save your $200 credit!)

```bash
# Terminate the environment (stops all EC2, ALB billing)
eb terminate my-app-env

# Delete the application entirely
eb terminate --all
```

---
## 🔑 Key Concepts Summary

| Feature | What EB Does for You |
|---|---|
| Deployment | Packages & uploads your code to S3, deploys to EC2 |
| Load Balancing | Creates & manages an ALB automatically |
| Auto Scaling | Adds/removes EC2 instances based on traffic |
| Health Monitoring | Tracks instance health, restarts unhealthy ones |
| Rolling Updates | Deploys new versions with zero downtime |
| Environment Variables | Securely injects config without hardcoding |
| Logs | Aggregates all instance logs to CloudWatch |

---

## 🆚 Elastic Beanstalk vs Alternatives

| | Elastic Beanstalk | EC2 (Manual) | Lambda |
|---|---|---|---|
| Server management | AWS | You | None |
| Scaling | Automatic | Manual | Automatic |
| Long-running apps | Yes | Yes | No (15 min max) |
| Cost control | Medium | Full | Per-request |
| Best for | Web apps, APIs | Full control | Event-driven |

---
