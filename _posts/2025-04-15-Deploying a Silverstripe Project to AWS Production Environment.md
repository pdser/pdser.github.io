---
layout: post
title: "Build your own CMS Part5: Deploying a Silverstripe Project to AWS Production Environment"
date: 2025-04-17 13:00:00 +0800
# categories: [SilverStripe]
# tags: [SilverStripe, CMS]
---



# 🚀 Deploying a Silverstripe Project to AWS Production Environment

Silverstripe is a powerful PHP-based CMS and framework. This guide walks you through deploying a Silverstripe 5 project to an AWS EC2 instance using Apache and MySQL, with production-ready configurations.

---

## 📦 Prerequisites

- A working Silverstripe project (created via `composer create-project`)
- An AWS EC2 instance (Ubuntu 20.04 recommended)
- Domain name (optional)
- SSH access to your server
- Basic knowledge of Linux commands

---

## 1. 🔧 Launch and Prepare Your EC2 Instance

### Step 1.1 — Create an EC2 instance

- Use Ubuntu Server 20.04 LTS
- Allow ports: `22`, `80`, `443` in the security group

### Step 1.2 — SSH into your server

```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

---

## 2. 🧱 Install Apache, PHP, and MySQL

```bash
sudo apt update
sudo apt install apache2 mysql-server
sudo apt install php php-mysql php-xml php-mbstring php-curl php-intl php-gd php-zip unzip
```

Install Composer:

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

---

## 3. 📁 Upload Your Silverstripe Project

You can upload via `scp` or pull from Git:

```bash
# Example: Cloning from GitHub
git clone https://github.com/your/repo.git /var/www/nzta
cd /var/www/nzta
composer install
```

---

## 4. ⚙️ Configure Environment Variables

Create a `.env` file in your Silverstripe root:

```dotenv
SS_ENVIRONMENT_TYPE="live"
SS_DATABASE_CLASS="MySQLDatabase"
SS_DATABASE_NAME="silverstripe_db"
SS_DATABASE_USERNAME="user"
SS_DATABASE_PASSWORD="your_password"
SS_DATABASE_SERVER="localhost"
```

---

## 5. 🏗️ Set Up MySQL Database

```bash
sudo mysql -u root -p

CREATE DATABASE silverstripe_db DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
CREATE USER 'ss_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON silverstripe_db.* TO 'ss_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

---

## 6. 🌐 Configure Apache Virtual Host

Create a virtual host file:

```bash
sudo nano /etc/apache2/sites-available/nzta.conf
```

Paste the following configuration:

```apache
<VirtualHost *:80>
    ServerName yourdomain.com
    DocumentRoot /var/www/nzta/public

    <Directory /var/www/nzta/public>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Enable the site and `mod_rewrite`:

```bash
sudo a2ensite nzta.conf
sudo a2enmod rewrite
sudo systemctl restart apache2
```

---

## 7. 🔐 Fix Permissions

```bash
sudo chown -R www-data:www-data /var/www/nzta
sudo find /var/www/nzta -type d -exec chmod 755 {} \;
sudo find /var/www/nzta -type f -exec chmod 644 {} \;
```

Make sure `public/assets/` is writable:

```bash
sudo chown -R www-data:www-data /var/www/nzta/public/assets
```

---

## 8. 🛠️ Run Database Build

Visit:

```
http://yourdomain.com/dev/build?flush=all
```

If `SS_ENVIRONMENT_TYPE` is set to `live`, temporarily change it to `dev` to run the build.

---

## 9. 🚀 (Optional) Configure HTTPS

Install Certbot:

```bash
sudo apt install certbot python3-certbot-apache
sudo certbot --apache
```

---

## ✅ Done!

Your Silverstripe site is now live and running on AWS!

---

## 🧪 Troubleshooting Tips

- **Permission denied on uploads**: Check ownership of `public/assets/` → `www-data`
- **CSS/JS not loading**: Run `dev/build?flush=all`, check Apache root points to `public/`
- **Site shows Apache default page**: Ensure your virtual host is correctly enabled and `000-default.conf` is disabled if needed

---

## 🛠️ Bonus: Use GitHub Actions for CI/CD (optional)

Want to automate deployment? Set up a GitHub Actions workflow to push changes directly to your EC2 via SSH.

---

Happy coding with Silverstripe! 🧁