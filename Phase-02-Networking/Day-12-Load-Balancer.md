# Day-12: AWS Load Balancer (ALB & NLB) – Full Hands-on

---

# 1️⃣ Introduction  

> What happens if your server gets too much traffic? Your app will crash. That’s why we use Load Balancers. In this video, we’ll learn Application Load Balancer and Network Load Balancer with real hands-on demo.

---

# 2️⃣ What is Load Balancer?

👉 A Load Balancer distributes traffic across multiple servers.

 - ✔ High availability
 - ✔ Fault tolerance
 - ✔ Scalability

---

# 3️⃣ Types of Load Balancer

---

## 🌐 Application Load Balancer (ALB)

 - ✔ Works at **Layer 7 (HTTP/HTTPS)**
 - ✔ Smart routing (path-based)

Example:

```text
/app → Server 1
/api → Server 2
```

---

## ⚡ Network Load Balancer (NLB)

 - ✔ Works at **Layer 4 (TCP/UDP)**
 - ✔ Ultra high performance

---

# 4️⃣ Architecture 

```text
User → Load Balancer → EC2 Instances
```

---

# 5️⃣ Hands-on Demo – Setup EC2 Servers

---

## Step 1: Launch 2 EC2 Instances

Service:

Amazon EC2

Name:

```text
web-server-1
web-server-2
```

---

## Step 2: Install Nginx on Both

```bash
sudo yum install nginx -y
sudo systemctl start nginx
```

---

## Step 3: Customize Pages

---

### Server 1

```bash
echo "Hello from Server 1" | sudo tee /usr/share/nginx/html/index.html
```

---

### Server 2

```bash
echo "Hello from Server 2" | sudo tee /usr/share/nginx/html/index.html
```

---

👉 Test individually via Public IP

---

# 6️⃣ Hands-on – Create ALB

---

## Step 1: Go to Load Balancer

Service:

Elastic Load Balancing

Click:

```text
Create Load Balancer → Application Load Balancer
```

---

## Step 2: Configure

```text
Name: my-alb
Scheme: Internet-facing
Listener: HTTP (80)
```

---

## Step 3: Select Subnets

✔ At least 2 AZs

---

## Step 4: Create Target Group

```text
Type: Instances
Protocol: HTTP
Port: 80
```

Add both EC2 instances

---

## Step 5: Create ALB

---

# 7️⃣ Test ALB 

Open:

```text
http://ALB-DNS
```

👉 Refresh multiple times:

 - ✔ Server 1
 - ✔ Server 2

👉 Traffic distributed ✅

---

# 8️⃣ Advanced ALB Feature 

---

## Path-based Routing

Example:

```text
Click ALB1 > CLick HTTP:80 > Add rule > click Add condition then select Path >
type error in path condition value > select return fixed option from Action >
type 404 in reponse code > type page not found in Response body > Next >
type a priority like 5 > Next > click Add rule 
```

### Now go to the browser and type URL : loadbalancer dns/error 
<br>
### We will get the message page not found
---

# 9️⃣ Hands-on – Create NLB

---

## Step 1: Create NLB

```text
Network Load Balancer
```

---

## Step 2: Configure

```text
Protocol: TCP
Port: 80
```

---

## Step 3: Target Group

Attach same EC2 instances

---

## Step 4: Test

👉 Use NLB DNS

 - ✔ Fast response
 - ✔ No HTTP routing

---

# 🔟 ALB vs NLB (Important Comparison)

| Feature  | ALB        | NLB       |
| -------- | ---------- | --------- |
| Layer    | 7          | 4         |
| Protocol | HTTP/HTTPS | TCP/UDP   |
| Routing  | Smart      | Simple    |
| Speed    | Medium     | Very Fast |

---

# 1️⃣1️⃣ Real DevOps Use Case

 - ✔ Microservices routing → ALB
 - ✔ High-performance apps → NLB
 - ✔ Kubernetes ingress → ALB

---

# 1️⃣2️⃣ Common Mistakes

 - ❌ Health check failing
 - ❌ Security group blocking
 - ❌ Wrong port

---

# 1️⃣3️⃣ Summary

* ALB = Smart routing (HTTP)
* NLB = High performance (TCP)

---

# 1️⃣4️⃣ Homework

 - 1️⃣ Create 2 EC2
 - 2️⃣ Install nginx
 - 3️⃣ Create ALB
 - 4️⃣ Test load balancing

---
