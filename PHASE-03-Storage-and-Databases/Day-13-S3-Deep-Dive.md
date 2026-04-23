# Day-13: AWS S3 Deep Dive + Versioning + Lifecycle Policy

---

# 1️⃣ Introduction 

> What if you delete an important file by mistake? Or your storage cost keeps increasing every month? In todays video, I’ll show you how S3 Versioning protects your data and how Lifecycle Policies reduce your AWS cost automatically.

---

# 2️⃣ What is S3?

👉 Object storage service

 - ✔ Unlimited storage
 - ✔ Highly durable (11 9’s)
 - ✔ Used for backups, static websites, logs

---

# 3️⃣ S3 Core Concepts 

* Bucket = container
* Object = file
* Key = file name

Example:

```text id="2h4b1g"
s3://my-bucket/image.png
```

---

# 4️⃣ Hands-on Demo – Create S3 Bucket

---

## Step 1: Go to S3

Service:

Amazon S3

---

## Step 2: Create Bucket

```text id="q2q0g0"
Bucket Name: devopssteps-demo-bucket
Region: choose nearest
```

---

## Step 3: Upload File

Upload any file:

```text id="o0h4gx"
test.txt
```

---

## Step 4: Access File

👉 Open object URL

---

# 5️⃣ Hands-on – Enable Versioning

---

## What is Versioning?

👉 Keeps multiple versions of the same file

---

## Step 1: Enable Versioning

```text id="ofed6r"
Bucket → Properties → Enable Versioning
```

---

## Step 2: Upload Same File Again

Upload:

```text id="y3ib78"
test.txt (modified content)
```

---

## Step 3: Check Versions

👉 Go to:

```text id="pk02a3"
Show Versions
```

---

👉 You’ll see:

 - ✔ Version 1
 - ✔ Version 2

---

## Step 4: Delete File (Important Demo)

Delete:

```text id="4bjnp7"
test.txt
```

👉 File is NOT fully deleted ❗

 - ✔ Delete marker created
 - ✔ Old versions still exist

---

## Step 5: Restore File

👉 Delete delete-marker → file restored

---

# 6️⃣ Real Use Case of Versioning

 - ✔ Backup protection
 - ✔ Accidental delete recovery
 - ✔ DevOps rollback

---

# 7️⃣ Hands-on – Lifecycle Policy

---

## What is Lifecycle Policy?

👉 Automatically moves or deletes objects

 - ✔ Save cost 💰

---

## Step 1: Go to Lifecycle Rules

```text id="x70c6q"
Management → Lifecycle Rules → Create rule
```

---

## Step 2: Configure Rule

```text id="w52u0e"
Rule Name: move-to-glacier
```

---

## Step 3: Transition Rule

Example:

```text id="ncb9y9"
After 30 days → Move to Standard-IA
After 60 days → Move to Glacier
```

---

## Step 4: Expiration Rule

```text id="6sjjgk"
Delete after 365 days
```

---

## Step 5: Apply Rule

👉 Save rule

---

# 8️⃣ Test Lifecycle 

👉 Cannot see immediate effect

 - ✔ Works automatically over time
 - ✔ Reduces storage cost

---

# 9️⃣ Storage Classes 

* Standard → frequent access
* Standard-IA → infrequent
* Glacier → archive

---

# 🔟 Real DevOps Use Case

 - ✔ Store logs
 - ✔ Backup database
 - ✔ Archive old data

---

# 1️⃣1️⃣ Common Mistakes

 - ❌ Not enabling versioning
 - ❌ Deleting without lifecycle
 - ❌ Using wrong storage class

---

# 1️⃣2️⃣ Summary

👉 Say clearly:

* S3 = Object storage
* Versioning = data protection
* Lifecycle = cost optimization

---

# 1️⃣3️⃣ Homework

 - 1️⃣ Create bucket
 - 2️⃣ Enable versioning
 - 3️⃣ Upload multiple versions
 - 4️⃣ Create lifecycle rule
