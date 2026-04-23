# Day-14: AWS S3 Static Website Hosting (Full Hands-on)

---

# 1️⃣ Introduction 

> Did you know you can host a website for almost free using AWS S3? In this video, I’ll show you step-by-step how to deploy a static website using S3 with full hands-on demo.

---

# 2️⃣ What is Static Website?

👉 Static website = HTML, CSS, JS only

 - ✔ No backend
 - ✔ Fast & cheap
 - ✔ Easy to deploy

---

# 3️⃣ Architecture

```text
User → S3 → Website
```

---

# 4️⃣ Hands-on Demo – Create Website Files

---

## Step 1: Create index.html

```html
<!DOCTYPE html>
<html>
<head>
  <title>DevOps Steps</title>
</head>
<body>
  <h1>Hello from S3 Static Website 🚀</h1>
</body>
</html>
```

---

## Step 2: Optional error.html

```html
<h1>Error: Page not found</h1>
```

---

# 5️⃣ Hands-on – Create S3 Bucket

---

## Step 1: Go to S3

Service:

Amazon S3

---

## Step 2: Create Bucket

```text
Bucket Name: devopssteps-static-site
```

⚠️ IMPORTANT:

 - ✔ Bucket name must be **globally unique**
 - ✔ Use lowercase

---

## Step 3: Disable Block Public Access

👉 Very important step

```text
Uncheck: Block all public access
```

---

# 6️⃣ Upload Website Files

---

## Step 1: Upload

Upload:

```text
index.html
error.html
```

---

# 7️⃣ Enable Static Website Hosting

---

## Step 1: Go to Properties

```text
Enable Static Website Hosting
```

---

## Step 2: Configure

```text
Index document: index.html
Error document: error.html
```

---

## Step 3: Save

---

# 8️⃣ Set Bucket Policy (VERY IMPORTANT)

Without this → site won’t open ❌

---

## Step 1: Go to Permissions → Bucket Policy

Paste this:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::devopssteps-static-site/*"
    }
  ]
}
```

---

# 9️⃣ Access Website

---

## Step 1: Get Endpoint

```text
http://bucket-name.s3-website-region.amazonaws.com
```

---

👉 Open in browser:

 - ✔ Website live 🎉

---

# 🔟 Test

 - ✔ Refresh page
 - ✔ Test error page

---

# 1️⃣1️⃣ Real DevOps Use Case

 - ✔ Portfolio website
 - ✔ Documentation site
 - ✔ Landing page

---

# 1️⃣2️⃣ Common Mistakes

 - ❌ Forget public access
 - ❌ Wrong bucket policy
 - ❌ Wrong file name (index.html)

---

# 1️⃣3️⃣ Pro Tip

👉 For production:

 - ✔ Use CloudFront (CDN)
 - ✔ Use HTTPS
 - ✔ Custom domain

---

# 1️⃣4️⃣ Summary

👉 Say clearly:

* S3 = static hosting
* Cheap & scalable
* Easy deployment

---

# 1️⃣5️⃣ Homework

 - 1️⃣ Create HTML file
 - 2️⃣ Upload to S3
 - 3️⃣ Enable hosting
 - 4️⃣ Access website
