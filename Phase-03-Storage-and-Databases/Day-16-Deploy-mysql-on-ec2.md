# Day 16: Install MySQL on AWS EC2 (Hands-On Tutorial)

👉 Topics Covered:

* Install MySQL on EC2
* Configure MySQL
* Connect from Local PC
* Open Security Group Port
* RDS vs EC2 MySQL Cost Comparison
* Reduce Database Cost

---

# 🧠 1. Introduction

👉 Usually databases are hosted using:

* Amazon RDS
* Self-managed MySQL on EC2

---

> “RDS is easier to manage, but running MySQL on EC2 can significantly reduce database cost for learning, development, or small production workloads.”

---

# 📊 Architecture

```text id="mysqlarch"
Local PC
    ↓
AWS EC2
    ↓
MySQL Database
```

---

# 💻 🧪 2. Launch EC2 Instance

Go to
[AWS Management Console](https://aws.amazon.com/console/?utm_source=chatgpt.com)

Launch:

* Ubuntu EC2
* t2.micro or t3.micro

---

# 🔐 Security Group Rules

Add inbound rules:

| Type         | Port |
| ------------ | ---- |
| SSH          | 22   |
| MySQL/Aurora | 3306 |

---

# ⚠️ Important

For testing:

```text id="mysqlsg"
0.0.0.0/0
```

For production:
 - ✔ Use your IP only

---

> “Port 3306 is required for MySQL remote access.”

---

# 🔗 3. Connect to EC2

---

## SSH Command

```bash id="sshmysql"
ssh -i mykey.pem ubuntu@<public-ip>
```

---

# 📦 4. Install MySQL on Ubuntu EC2

---

## Update Server

```bash id="updateec2"
sudo apt update
```

---

## Install MySQL

```bash id="installmysql"
sudo apt install mysql-server -y
```

---

# 🔍 Verify MySQL

```bash id="mysqlstatus"
sudo systemctl status mysql
```

---

# 🎉 MySQL installed successfully

---

# 🔐 5. Configure MySQL for Remote Access

---

# Open MySQL Config

```bash id="mysqledit"
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

---

# Find:

```text id="bindaddress"
bind-address = 127.0.0.1
```

Replace with:

```text id="bindall"
bind-address = 0.0.0.0
```

---

# Restart MySQL

```bash id="restartmysql"
sudo systemctl restart mysql
```

---

> “By default MySQL only accepts local connections. We must allow remote connections.”

---

# 👤 6. Create MySQL User for Remote Access

---

# Login to MySQL

```bash id="mysqlroot"
sudo mysql
```

---

# Create User

```sql id="createuser"
CREATE USER 'devops'@'%' IDENTIFIED BY 'password123';
```

---

# Grant Privileges

```sql id="grantpriv"
GRANT ALL PRIVILEGES ON *.* TO 'devops'@'%';
FLUSH PRIVILEGES;
```

---

# Exit

```sql id="exitmysql"
exit;
```

---

# 💻 7. Connect from Local PC

Use:

* MySQL Workbench
* DBeaver
* Azure Data Studio

---

# Connection Details

| Item     | Value         |
| -------- | ------------- |
| Hostname | EC2 Public IP |
| Port     | 3306          |
| Username | devops        |
| Password | password123   |

---

# 🎉 Database connected successfully

---

# 🧪 8. Create Database Demo

---

# Create Database

```sql id="createdb"
CREATE DATABASE company;
```

---

# Use Database

```sql id="usedb"
USE company;
```

---

# Create Table

```sql id="createtablemysql"
CREATE TABLE employees (
  id INT,
  name VARCHAR(50)
);
```

---

# Insert Data

```sql id="insertmysql"
INSERT INTO employees VALUES (1, 'Rajiv');
```

---

# Query Data

```sql id="querymysql"
SELECT * FROM employees;
```

---

> “Now MySQL is fully running on AWS EC2.”

---

# 💸 9. RDS vs MySQL on EC2 (VERY IMPORTANT)

| Feature     | RDS         | MySQL on EC2          |
| ----------- | ----------- | --------------------- |
| Setup       | Easy        | Manual                |
| Maintenance | AWS Managed | Self Managed          |
| Backup      | Automatic   | Manual                |
| Scaling     | Easy        | Manual                |
| Cost        | Higher      | Lower                 |
| Best For    | Production  | Learning / Small Apps |

---

# 💰 Cost Comparison Example

Example monthly:

| Service            | Approx Cost |
| ------------------ | ----------- |
| RDS MySQL          | $15–30+     |
| EC2 MySQL t2.micro | $5–10       |

---

> “For learning and small projects, MySQL on EC2 can reduce database cost significantly.”

---

# ⚠️ Production Warning

For real production:
 - ✔ RDS preferred
 - ✔ Automated backup
 - ✔ High availability
 - ✔ Easier maintenance

---

# 🧠 10. Real DevOps Use Cases

 - ✔ Laravel/MySQL
 - ✔ WordPress hosting
 - ✔ Kubernetes backend DB
 - ✔ CI/CD testing databases

---

# 🔐 11. Security Best Practices

 - ✔ Restrict port 3306
 - ✔ Use strong password
 - ✔ Backup database
 - ✔ Use private subnet in production

---

# 🧠 Summary

 - ✔ Installed MySQL on EC2
 - ✔ Connected remotely from local PC
 - ✔ Compared RDS vs EC2 cost
 - ✔ Learned database cost optimization

---

# 🎬 Final Line

> “Self-managed MySQL on EC2 is an excellent way to learn database administration and reduce cloud costs.”

---
