# AWS Project: **S3 Upload → Lambda → SNS Notification** 

### Here's the complete flow explained:
 * ① User → S3 — User uploads an image (via app, CLI, or SDK) to an S3 bucket.
 * ② S3 Event → Lambda — S3 automatically fires an s3:ObjectCreated event notification which invokes your Lambda function, passing the bucket name and file key.
 * ③ Lambda → SNS Topic — Lambda processes the event (extracts file info, optionally runs logic) then publishes a message to an SNS Topic.
 * ④ SNS → Email — SNS delivers the notification to all subscribers — in this case an email address — with details like filename, size, and timestamp.

# Demo Architecture
```text
User
  |
Upload Image
  |
Amazon S3
  |
S3 Event
  |
AWS Lambda
  |
SNS Topic
  |
Email Notification
```

### What Happens?

1. User uploads an image to S3.
2. S3 triggers Lambda.
3. Lambda reads image details.
4. Lambda sends message to SNS.
5. SNS sends email notification.

This demonstrates:

* S3 Events
* Lambda
* SNS
* IAM Roles
* CloudWatch Logs

---

# Lab 1: Create S3 Bucket

Navigate to:

```text
AWS Console
→ S3
→ Create Bucket
```

Example:

```text
devopssteps-image-demo-12345
```

Keep defaults and create.

---

# Lab 2: Create SNS Topic

Navigate:

```text
SNS
→ Topics
→ Create Topic
```

Choose:

```text
Standard
```

Topic Name:

```text
image-upload-topic
```

Create Topic.

---

# Lab 3: Create Email Subscription

Inside topic:

```text
Create Subscription
```

Protocol:

```text
Email
```

Endpoint:

```text
your-email@gmail.com
```

Click Create.

Check email and confirm subscription.

---

# Lab 4: Create Lambda Role

Navigate:

```text
IAM
→ Roles
→ Create Role
```

Trusted Entity:

```text
Lambda
```

Attach:

* AWSLambdaBasicExecutionRole

Create role:

```text
lambda-s3-sns-role
```

---

# Add SNS Permission

Attach inline policy:

```json
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Effect":"Allow",
      "Action":[
        "sns:Publish"
      ],
      "Resource":"*"
    }
  ]
}
```

---

# Lab 5: Create Lambda Function

Navigate:

```text
Lambda
→ Create Function
```

Settings:

```text
Function Name:
image-upload-handler

Runtime:
Python 3.13
```

Role:

```text
lambda-s3-sns-role
```

Create.

---

# Lambda Code

Replace code with:

```python
import json
import boto3

sns = boto3.client('sns')

TOPIC_ARN = "YOUR-SNS-TOPIC-ARN"

def lambda_handler(event, context):

    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']

    message = f"""
New File Uploaded

Bucket: {bucket}
File: {key}
"""

    sns.publish(
        TopicArn=TOPIC_ARN,
        Subject="New S3 Upload",
        Message=message
    )

    return {
        'statusCode':200,
        'body':'Notification Sent'
    }
```

Deploy.

---

# Get SNS ARN

Example:

```text
arn:aws:sns:us-east-1:123456789012:image-upload-topic
```

Update Lambda code.

Deploy again.

---

# Lab 6: Configure S3 Trigger

Open Lambda:

```text
Configuration
→ Triggers
→ Add Trigger
```

Choose:

```text
S3
```

Bucket:

```text
devopssteps-image-demo-12345
```

Event:

```text
PUT
```

Enable.

Save.

---

# Lab 7: Test Workflow

Upload:

```text
cat.jpg
```

to S3 bucket.

Immediately:

```text
S3
→ Lambda Trigger
→ Lambda Executes
→ SNS Sends Email
```

Email received:

```text
Subject:
New S3 Upload

Bucket:
devopssteps-image-demo-12345

File:
cat.jpg
```

---

# Verify Logs

Navigate:

```text
CloudWatch
→ Log Groups
```

Open Lambda log group.

You will see execution logs.

---

# Enhanced Version (Image Metadata)
### First crete a role which allsow access s3 metadata and use this way 
```sh
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect":"Allow",
      "Action":"s3:*",
      "Resource":"*"
    }
  ]
}
```
OR, Advance level s3 idea
```sh
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::devopssteps-image-demo-12345/*"
    }
  ]
}
```

### Edit the lamda code
Replace code:

```python
import boto3

s3 = boto3.client('s3')
sns = boto3.client('sns')

TOPIC_ARN = "YOUR-TOPIC-ARN"

def lambda_handler(event, context):

    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']

    obj = s3.head_object(
        Bucket=bucket,
        Key=key
    )

    size = obj['ContentLength']

    message = f"""
Image Uploaded

Bucket: {bucket}
File: {key}
Size: {size} bytes
"""

    sns.publish(
        TopicArn=TOPIC_ARN,
        Subject="Image Upload Notification",
        Message=message
    )
```

Now email contains file size.

---

# Production-Level Demo

```text
S3 Upload
    |
Lambda
    |
Resize Image
    |
Store Thumbnail
    |
SNS Notification
```

Common real-world use cases:

* Profile pictures
* E-commerce images
* Product catalogs
* Social media uploads

---
