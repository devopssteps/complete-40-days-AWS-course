# Deploy Docker App to ECS Fargate with ALB + Auto Scaling

### 🛠 Hands-on Demo Project: Deploy Docker App to ECS Fargate with ALB + Auto Scaling
We’ll deploy a Dockerized Node.js App on ECS (Fargate) behind an Application Load Balancer (ALB) with Auto Scaling enabled.

![aws-project](https://github.com/devopssteps/complete-40-days-AWS-course/blob/main/Phase-07-Containers_and_Kubernetes/ecs-proejct.jpg) 
![aws-project](https://github.com/devopssteps/complete-40-days-AWS-course/blob/main/Phase-07-Containers_and_Kubernetes/ecs-proejct-diagram.png) 

Notes: 
- ECR → ECS: the cluster pulls the container image from ECR when a task starts, so it always runs the exact image you pushed.
- ALB → tasks: the load balancer spreads incoming requests across whichever tasks are currently running, so no single container gets overwhelmed.
- Auto Scaling → tasks: this is the "hands-off" piece — it monitors metrics like CPU/request count and scales the task count up or down without you touching anything manually.


### 📌 Step 1: Create a Simple Dockerized App
```app.js``` (Node.js example)
```sh
const express = require('express');
const os = require('os');
const app = express();
const PORT = process.env.PORT || 3000;

app.get('/', (req, res) => {
  res.send(`Hello from ECS Fargate 🚀 | Served by: ${os.hostname()}`);
});

app.listen(PORT, () => {
  console.log(`App running on port ${PORT}`);
});
```
Dockerfile
```sh
FROM node:18-alpine
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```
```package.json```
```sh
{
  "name": "ecs-demo",
  "version": "1.0.0",
  "main": "app.js",
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

### 📌 Step 2: Build & Push Docker Image to ECR
```sh
# Authenticate Docker to AWS ECR
aws ecr create-repository --repository-name ecs-demo
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com

# Build & Push
docker build -t ecs-demo .
docker tag ecs-demo:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/ecs-demo:latest
docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/ecs-demo:latest
```

### 📌 Step 3: Create ECS Cluster (Fargate)
 1. Go to ECS Console → Create Cluster → Select Networking only (Fargate).
 2. Name: ```ecs-fargate-demo```.

### 📌 Step 4: Create Task Definition
 1. ECS → Task Definitions → Create New.
 2. Launch Type: Fargate.
 3. Container Definition:
     - Image: ```<AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/ecs-demo:latest```
     - Port Mappings: ```3000```


### 📌 Step 5: Create ALB + Service
 1. ECS → Services → Create Service.
 2. Launch Type: Fargate.
 3. Cluster: ```ecs-fargate-demo```.
 4. Task Definition: Select above.
 5. Desired Tasks: ```2```.
 6. Load Balancing: Application Load Balancer.
    - Create ALB (Internet-facing).
    - Listener: HTTP 80 → Target Group → ECS tasks.

### 📌 Step 6: Enable Auto Scaling
 1. While creating the Service → Enable Service Auto Scaling.
 2. Configure:
    - Min tasks: 2
    - Max tasks: 5
    - Scaling policy: CPU utilization > 60% → Scale out, < 30% → Scale in.


### 📌 Step 7: Test
 1. Get ALB DNS from EC2 → Load Balancer.
 2. Open in browser:
```sh
http://<ALB-DNS-NAME>
```
### You should see: Hello from ECS Fargate 🚀
 3. Run load test with ApacheBench:
```sh
ab -n 10000 -c 200 http://<ALB-DNS-NAME>/
```
→ New tasks will launch automatically.
