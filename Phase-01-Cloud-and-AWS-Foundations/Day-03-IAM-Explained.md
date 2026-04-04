# Day 03-Complete AWS course -AWS IAM Explained (Users, Groups, Policies, Role) 

# Toyday's video will cover:
 * User
 * Group
 * Policies
 * Role
 * Hands on all

---

# 1️⃣ Introduction to IAM

**IAM stands for Identity and Access Management.**

It is the AWS service used to **control who can access AWS resources and what actions they can perform.**

Example:

* Who can create EC2 servers
* Who can access S3 buckets
* Who can manage databases

Without IAM, anyone with access could control your entire cloud environment.

---

# 2️⃣ Why IAM is Important

IAM helps with:

 * ✔ Security
 * ✔ Access control
 * ✔ User management
 * ✔ Least privilege principle

Example:

A company may have:

* DevOps Engineers
* Developers
* Security team

Each team gets **different permissions**.

---

# 3️⃣ IAM Core Components

### 1. IAM Users

An **IAM user** represents a person or application.

Example users:

```
dev-user
admin-user
developer-user
```

Each user gets login credentials.

---

### 2. IAM Groups

Groups help **manage multiple users together**.

Example groups:

```
Developers
Admins
ReadOnlyUsers
```

Instead of assigning permissions to each user, you assign them to the group.

---

### 3. IAM Policies

Policies define **permissions**.

Policies are written in **JSON format**.

Example policy:

```
Allow EC2 Full Access
```

Policies define actions like:

* Create instance
* Stop instance
* Delete instance

---

### 4. IAM Roles

Roles are used by **AWS services or applications**.

Example:

EC2 instance accessing S3 bucket.

---

# 4️⃣ IAM Best Practices

Explain these security rules.

* ✔ Never use root account for daily tasks
* ✔ Use IAM users instead
* ✔ Use groups to manage permissions
* ✔ Follow least privilege principle
* ✔ Enable MFA

---

# 5️⃣ Hands-on Demo

Now move to practical demo.

Login to AWS console:

```
https://console.aws.amazon.com
```

Search for:

AWS Identity and Access Management

Open the IAM dashboard.

---

# Step 1 – Create IAM User

Click:

```
Users
Create user
```

User name:

```
dev-user
```

Select:

✔ AWS Management Console access

Create password.

Click **Next**.

---

# Step 2 – Create IAM Group

Click:

```
Create group
```

Group name:

```
Developers
```

Attach policy:

```
AmazonEC2ReadOnlyAccess
```

Create the group.

---

# Step 3 – Add User to Group

Add:

```
dev-user
```

to group:

```
Developers
```

This means the user now inherits the group's permissions.

---

# Step 4 – Login with IAM User

Logout from AWS root account.

Login using:

```
https://your-account-id.signin.aws.amazon.com/console
```

Use:

```
dev-user
```

Now open:

Amazon EC2

You will notice:

User can **view EC2 instances but cannot create them**.

This demonstrates **permission control**.

---

# 6️⃣ IAM Policy Example

Show simple JSON policy example.

```
{
 "Version": "2012-10-17",
 "Statement": [
   {
     "Effect": "Allow",
     "Action": "ec2:DescribeInstances",
     "Resource": "*"
   }
 ]
}
```

Explanation:

This policy allows **viewing EC2 instances only**.

---

# 7️⃣ Real DevOps Example

Example:

DevOps team manages infrastructure.

Services they manage include:

* Amazon EC2
* Amazon S3
* Amazon RDS

They get **full access policies**.

Developers may only get **read access**.

---

# 8️⃣ Homework for You

Practice these following things:

1️⃣ Create IAM user
2️⃣ Create group
3️⃣ Attach policy
4️⃣ Login with IAM user

---
