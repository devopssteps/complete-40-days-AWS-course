# AWS Route 53 Tutorial with Hands-On Demo

## What is AWS Route 53?

Amazon Route 53 is AWS's highly available and scalable **DNS (Domain Name System)** service.

Think of Route 53 as the internet's phonebook:

```text id="g2s5zc"
www.google.com  →  142.250.xxx.xxx
www.amazon.com  →  54.xxx.xxx.xxx
```

Instead of remembering IP addresses, users type domain names, and Route 53 translates them to the correct IP address.

---

## What Can Route 53 Do?

### 1. Domain Registration

Buy domains such as:

```text id="xyn66g"
devopssteps.com
mycompany.com
```

---

### 2. DNS Management

Map a domain to:

* EC2 Instance
* Load Balancer
* S3 Static Website
* CloudFront Distribution
* App Runner
* API Gateway

---

### 3. Health Checks

Monitor application health.

Example:

```text id="tx8wqo"
Website Down
↓
Route 53 Detects Failure
↓
Redirect Traffic to Backup Site
```

---

### 4. Traffic Routing

Different routing policies:

* Simple Routing
* Weighted Routing
* Latency Routing
* Failover Routing
* Geolocation Routing

---

# Route 53 Components

## Hosted Zone

A container for DNS records.

Example:

```text id="nzov8v"
devopssteps.com
```

Hosted Zone contains:

```text id="ytlkvg"
A Record
CNAME Record
MX Record
TXT Record
```

---

## DNS Records

### A Record

Maps:

```text id="f6uv4i"
Domain → IP Address
```

Example:

```text id="0s6h44"
devopssteps.com → 54.210.10.20
```

---

### CNAME

Maps:

```text id="1v9p4v"
www.devopssteps.com
→
devopssteps.com
```

---

### MX

Mail records.

Used by:

```text id="4cw89n"
Google Workspace
Microsoft 365
```

---

### TXT

Verification records.

Used by:

```text id="2r8tt9"
Google Search Console
SSL Validation
SPF/DKIM
```

---

# Hands-On Demo 1

## Point a Domain to an EC2 Website

### Architecture

```text id="ttuzjv"
Route 53
      |
      v
devopssteps.com
      |
      v
EC2 Instance
      |
      v
Apache Website
```

---

## Step 1: Launch EC2

Install Apache:

```bash id="n4jsgq"
sudo yum update -y
sudo yum install httpd -y

sudo systemctl start httpd
sudo systemctl enable httpd
```

Create webpage:

```bash id="s66i24"
echo "<h1>Welcome to DevOps Steps</h1>" | sudo tee /var/www/html/index.html
```

Open browser:

```text id="l9z8rt"
http://EC2-PUBLIC-IP
```

Example:

```text id="d70j1e"
http://54.210.10.20
```

Website should load.

---

## Step 2: Purchase a Domain

Go to:

### Route 53

```text id="h9o73u"
AWS Console
→ Route 53
→ Registered Domains
→ Register Domain
```

Example:

```text id="m6jqzh"
devopsstepsdemo.com
```

---

## Step 3: Create Hosted Zone

```text id="qjlwmg"
Route 53
→ Hosted Zones
→ Create Hosted Zone
```

Domain:

```text id="bx6qvi"
devopsstepsdemo.com
```

Type:

```text id="ovrq8v"
Public Hosted Zone
```

---

## Step 4: Create A Record

Inside Hosted Zone:

```text id="wjj7ot"
Create Record
```

Configure:

```text id="7y7n1x"
Record Type:
A

Value:
54.210.10.20
```

Save.

---

## Step 5: Test

Open:

```text id="7ksrjv"
http://devopsstepsdemo.com
```

Route 53 resolves:

```text id="vwmbg8"
devopsstepsdemo.com
↓
54.210.10.20
↓
Apache Website
```

---

# Hands-On Demo 2

## Route 53 + Load Balancer

### Architecture

```text id="s9hwmz"
Domain
   |
Route53
   |
ALB
 / \
EC2 EC2
```

Benefits:

* High Availability
* Auto Scaling
* Production Architecture

---

### Create ALB

Go to:

```text id="vjlwmc"
EC2
→ Load Balancer
→ Application Load Balancer
```

Copy DNS Name:

Example:

```text id="b42n8i"
myalb-123456.us-east-1.elb.amazonaws.com
```

---

### Create Alias Record

In Route 53:

```text id="7h1pdu"
Create Record
```

Type:

```text id="o2dxmw"
A Record
```

Enable:

```text id="g7z0u2"
Alias = Yes
```

Select:

```text id="0wb8hl"
Application Load Balancer
```

Save.

---

### Test

Open:

```text id="vt5sb7"
http://devopsstepsdemo.com
```

Traffic flow:

```text id="svfqqw"
Domain
↓
Route53
↓
ALB
↓
EC2
```

---

# Common Routing Policies

## Simple Routing

One destination.

```text id="lhmwwq"
Domain
↓
One Server
```

---

## Weighted Routing

Split traffic.

Example:

```text id="9r4v4j"
Server A = 80%
Server B = 20%
```

Useful for:

```text id="fjjbgn"
Blue-Green Deployment
```

---

## Latency Routing

User routed to nearest region.

Example:

```text id="8bw5pt"
USA User → Virginia

Asia User → Singapore
```

---

## Failover Routing

Primary site fails.

```text id="9q5b4r"
Primary Website
↓
Down
↓
Backup Website
```

---

# Route 53 Interview Questions

### What is Route 53?

AWS DNS service used for domain registration, DNS management, health checks, and traffic routing.

### What is a Hosted Zone?

A container that stores DNS records for a domain.

### What is an A Record?

Maps a domain name to an IPv4 address.

### What is an Alias Record?

AWS-specific record that points to AWS resources such as:

* Load Balancer
* CloudFront
* S3 Static Website

without requiring an IP address.

### What is Failover Routing?

Automatically routes traffic to a secondary resource if the primary resource becomes unhealthy.

---
