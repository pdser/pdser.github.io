---
layout: post
title: "Build your own CMS Part1: Setting Up a Silverstripe Development Environment on Windows (XAMPP)"
date: 2025-04-12 10:00:00 +0800
# categories: [SilverStripe]
# tags: [SilverStripe, CMS]
---


# 🛠️ Setting Up a Silverstripe Development Environment on Windows (XAMPP)

This guide walks you through setting up a **Silverstripe CMS development environment** on **Windows using XAMPP**, with Composer and Apache virtual hosts. It also includes real-world error messages and solutions encountered during setup.

---

## 📋 Prerequisites

Make sure the following tools are installed:

| Tool              | Purpose                    | Notes                          |
|-------------------|----------------------------|--------------------------------|
| **XAMPP**         | PHP, Apache & MySQL stack | PHP ≥ 7.4 required             |
| **Composer**      | PHP dependency manager     | Latest version                 |
| **Git** *(optional)*     | Version control             | Helpful for source control     |
| **VS Code** *(optional)* | Code editor                 | Recommended for `.env` editing |

---

## 🚀 Installation Steps

### 1. Install XAMPP and Start Services

- Download and install XAMPP.
- Launch **XAMPP Control Panel**.
- Start the following services:
  - ✅ Apache
  - ✅ MySQL
- Verify: Visit [http://localhost/phpmyadmin](http://localhost/phpmyadmin) to access MySQL.

---

### 2. Install Composer

- Download Composer from [getcomposer.org](https://getcomposer.org)
- During setup, set PHP path to:

```
C:\xampp\php\php.exe
```

- After installation, open **Command Prompt (CMD)** and verify:

```bash
composer -V
```

---

### 3. Create a Silverstripe Project

In your development directory (e.g., `C:\xampp\htdocs`):

```bash
cd C:\xampp\htdocs
composer create-project silverstripe/installer my-blog
cd my-blog
```

---

### 4. Create a Database & Configure `.env`

1. Open [http://localhost/phpmyadmin](http://localhost/phpmyadmin)
2. Create a new database named:

```
myblog
```

3. In your project root, create a `.env` file with the following content:

```env
SS_DATABASE_CLASS="MySQLDatabase"
SS_DATABASE_SERVER="localhost"
SS_DATABASE_NAME="myblog"
SS_DATABASE_USERNAME="root"
SS_DATABASE_PASSWORD=""
SS_ENVIRONMENT_TYPE="dev"
```

> ⚠️ Ensure the file is named exactly `.env` — not `.env.txt`.

---

### 5. Enable the `intl` PHP Extension

Edit this file:

```
C:\xampp\php\php.ini
```

Find this line:

```ini
;extension=intl
```

Change it to:

```ini
extension=intl
```

Then save and **restart Apache** from the XAMPP Control Panel.

---

### 6. (Optional but Recommended) Set Up Apache Virtual Host

1. Edit the virtual host configuration file:

```
C:\xampp\apache\conf\extra\httpd-vhosts.conf
```

Add the following:

```apache
<VirtualHost *:80>
    DocumentRoot "D:/Projects/my-blog/public"
    ServerName myblog.local

    <Directory "D:/Projects/my-blog/public">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

2. Edit your system `hosts` file:

```
C:\Windows\System32\drivers\etc\hosts
```

Add:

```
127.0.0.1   myblog.local
```

> 🛡️ Use **Notepad or VS Code as Administrator** to save the file.

3. Restart Apache.

---

### 7. Initialize the Database

On **Windows**, **do not** use the `sake` command — it’s a Unix shell script.

Instead, open your browser and visit:

- If using virtual host:

```
http://myblog.local/dev/build?flush=1
```

- Or without virtual host:

```
http://localhost/my-blog/public/dev/build?flush=1
```

You should see output like:

```
Creating database tables
Rebuilding manifest
Building ...
```

---

## ✅ Access Your Site

- With virtual host:

```
http://myblog.local/
```

- Without virtual host:

```
http://localhost/my-blog/public/
```

You should now see the **Silverstripe welcome screen** 🎉

---

## 💡 Common Issues & Fixes

| Error | Cause | Solution |
|-------|-------|----------|
| **This backend requires the php-intl extension** | PHP `intl` extension not enabled | Edit `php.ini`, enable `extension=intl` |
| **Silverstripe requires a "database" key...** | `.env` file missing or invalid | Ensure `SS_DATABASE_NAME` is set and DB exists |
| **.env ignored** | Misnamed or misplaced file | Must be named `.env` and located in project root |
| **sake doesn't work** | Windows doesn't support Unix shell scripts | Use browser `/dev/build?flush=1` instead |
| **Stylesheets or JS not loading** | Accessing wrong path | Always access via `/public/` |
| **404 errors after folder changes** | Apache `DocumentRoot` misconfigured | Use Virtual Hosts to point to `public/` folder |

---

## ✅ You're Ready to Build

Now that your environment is up and running, you can:

- Create your first `BlogPost` model
- Build custom templates and controllers
- Add admin CMS fields
- Use SCSS and JS for styling
- Deploy to a server or cloud service when ready

Happy Silverstriping! 🚀
