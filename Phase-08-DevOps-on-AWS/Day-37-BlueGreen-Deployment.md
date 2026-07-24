
# 🚀 AWS Blue/Green Deployment — Complete Hands-On Demo
## 1. What is Blue/Green Deployment?

Blue/Green Deployment is a deployment strategy where we maintain **two environments**:

### 🔵 Blue Environment

The current version of the application serving production traffic.

### 🟢 Green Environment

The new version of the application that we want to deploy and test.

### An AWS Blue-Green Deployment is a release strategy that cuts downtime and risk by running two identical production environments: Blue (the current live version) and Green (the new version).Once testing passes on Green, production traffic is instantly routed away from Blue. If something goes wrong, you can instantly roll back to Blue with zero downtime.

![AWS BlueGreen Deployment](https://github.com/devopssteps/complete-40-days-AWS-course/blob/main/Phase-08-DevOps-on-AWS/aws_blue_green_deployment_thumbnail.png) 
---
The basic workflow is:

```text
                 Users
                   |
                   v
          Application Load Balancer
                   |
          Current Production Traffic
                   |
                   v
          🔵 BLUE ENVIRONMENT
          Application v1.0
                   
                   |
                   | Deploy New Version
                   v
          🟢 GREEN ENVIRONMENT
          Application v2.0
                   
                   |
              Test & Verify
                   |
                   v
             Shift Traffic
                   |
                   v
          🟢 GREEN = LIVE
```

If something goes wrong:

```text
🟢 GREEN ❌
     |
     | Rollback
     v
🔵 BLUE ✅
```

The major benefit is that we can deploy a new version **without taking down the existing production environment**.

---

# 2. What We Will Build

Our hands-on architecture will look like this:

```text
                         Internet
                             |
                             v
                  Application Load Balancer
                             |
                    Target Group / Traffic
                             |
               +-------------+-------------+
               |                           |
               v                           v
       🔵 Blue Environment         🟢 Green Environment
          EC2 Instance                EC2 Instance
          App Version 1               App Version 2
               |                           |
               +-------------+-------------+
                             |
                       AWS CodeDeploy
                             |
                       Deployment
```

We will use:

* Amazon EC2
* Application Load Balancer
* Target Groups
* AWS CodeDeploy
* IAM
* S3
* AWS CLI
* Linux
* Shell Script
* `appspec.yml`

---

# 3. What We Will Learn

By the end of this demo, we should understand:

* What Blue/Green Deployment is
* Why companies use it
* Blue vs Green environments
* How traffic is shifted
* How rollback works
* How AWS CodeDeploy supports Blue/Green Deployment
* How ALB works with deployment environments
* How to deploy a new application version
* How to test the new environment before production traffic is shifted

---
