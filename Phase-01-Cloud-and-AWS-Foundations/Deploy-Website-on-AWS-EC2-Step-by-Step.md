# Deploy Website on AWS EC2 Step-by-Step

“Todays video we will deploy our website on AWS in just 10 minutes.”

---

## 🪜 Step 1 — Launch EC2

* Go to AWS Console → EC2
* Click **Launch Instance**
* Choose:

  * AMI: Ubuntu
  * Instance: t2.micro
* Create key pair
* Allow:

  * Port 22 (SSH)
  * Port 80 (HTTP)
* Launch instance

---

## 🔐 Step 2 — Connect to EC2

```bash
ssh -i your-key.pem ubuntu@your-public-ip
```

---

## ⚙️ Step 3 — Update Server

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 🌐 Step 4 — Install Nginx

```bash
sudo apt install nginx -y
```

Start service:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

👉 Open browser:

```
http://your-public-ip
```

---

## 📂 Step 5 — Deploy Your Website

Go to web directory:

```bash
cd /var/www/html
```

Replace default page:

```bash
sudo rm index.nginx-debian.html
sudo nano index.html
```

Add simple HTML:

```html
<h1>Hello from AWS EC2</h1>
```

---

## 🔄 Step 6 — Reload Nginx

```bash
sudo systemctl restart nginx
```

👉 Refresh browser → Your site is LIVE 🎉

---

# ⚠️ Important

“Don’t forget to stop your EC2 instance when not using it — or AWS will charge you 💸”

---
