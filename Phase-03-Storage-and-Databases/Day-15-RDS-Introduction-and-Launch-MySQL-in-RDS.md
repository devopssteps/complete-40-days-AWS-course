# Day-15: AWS RDS Tutorial | Launch MySQL Database (Hands-on)

---

# 1️⃣ Introduction 

> Managing databases manually is difficult and time-consuming. In this video, we’ll use AWS RDS to launch a fully managed MySQL database in just a few clicks with a hands-on demo.

---

# 2️⃣ What is RDS?

👉 Managed database service

 - ✔ Automated backups
 - ✔ Patching handled by AWS
 - ✔ High availability

---

# 3️⃣ Supported Databases

* MySQL
* PostgreSQL
* MariaDB
* Oracle
* SQL Server

---

# 4️⃣ Architecture Overview

```text
Application → RDS Database
```

---

# 5️⃣ Hands-on Demo – Create RDS MySQL

---

## Step 1: Go to RDS

Service:

Amazon RDS

Click:

```text id="pxtj3p"
Create Database
```

---

## Step 2: Choose Engine

```text id="puj03f"
Engine: MySQL
```

---

## Step 3: Choose Template

```text id="p15b5q"
Free tier (for beginners)
```

---

## Step 4: Configure DB

```text id="sb1l0o"
DB instance identifier: mydb
Master username: admin
Password: yourpassword
```

---

## Step 5: Instance Settings

```text id="sbmmfb"
DB class: db.t3.micro
```

---

## Step 6: Storage

```text id="ctdybr"
20 GB (default)
```

---

## Step 7: Connectivity

 - ✔ VPC: default
 - ✔ Public access: YES (for demo)

---

## Step 8: Security Group

Allow:

```text id="dn39of"
MySQL (3306) → My IP
```

---

## Step 9: Create Database

Click:

```text id="snry0j"
Create Database
```

⏱ Wait 5–10 minutes

---

# 6️⃣ Connect to RDS (Hands-on)

---

## Step 1: Get Endpoint

```text id="s2h5am"
mydb.xxxxxx.ap-south-1.rds.amazonaws.com
```

---

## Step 2: Connect via MySQL Client

```bash id="8khjbn"
mysql -h ENDPOINT -u admin -p
```

---

## Step 3: Enter Password

👉 Connected successfully ✅

---

# 7️⃣ Run SQL Commands (Demo)

```sql id="c8sb6g"
CREATE DATABASE devopsdb;
USE devopsdb;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(50)
);

INSERT INTO users (name) VALUES ('Rajiv');

SELECT * FROM users;
```

---

# 8️⃣ Test from EC2 (Real Scenario)

---

## Step 1: Launch EC2

Service:

Amazon EC2

---

## Step 2: Install MySQL Client

```bash id="a0mp0q"
sudo yum install mysql -y
```

---

## Step 3: Connect to RDS

```bash id="9rjz3q"
mysql -h ENDPOINT -u admin -p
```

👉 Works ✅

---

# 9️⃣ Real DevOps Use Case

 - ✔ Store application data
 - ✔ Backend database
 - ✔ Production systems

---

# 🔟 Common Mistakes

 - ❌ Public access disabled → cannot connect
 - ❌ Security group blocking port 3306
 - ❌ Wrong endpoint

---

# 1️⃣1️⃣ Summary

* RDS = managed database
* MySQL = engine
* Easy to deploy & scale

---

# 1️⃣2️⃣ Homework

 - 1️⃣ Create RDS MySQL
 - 2️⃣ Connect using CLI
 - 3️⃣ Create table
 - 4️⃣ Insert data
