---
layout: post
title: "A Minimal and Developer-Friendly Project Structure"
date: 2025-04-15 10:00:00 +0800
# categories: [SilverStripe]
# tags: [SilverStripe, CMS]
---



# 🧱 Getting Started with Silverstripe: A Minimal and Developer-Friendly Project Structure

If you're new to Silverstripe or want to create a clean, maintainable project from scratch, this guide walks you through a simple and standard-compliant setup.

---

## ✅ Step 1: Install Silverstripe via Composer

First, create a new Silverstripe project using Composer:

```bash
composer create-project silverstripe/installer mysite
cd mysite
```

---

## ✅ Step 2: Create Your Custom Template Directory

Instead of using the default `themes/` structure, we'll keep things simpler.

Create a `templates/` folder inside the `app/` directory:

```bash
mkdir -p app/templates/Layout
mkdir -p app/templates/Includes
```

This will be your primary template location.

---

## ✅ Step 3: Enable the Template Path

Tell Silverstripe to use your custom templates by editing or creating the following file:

```yaml
# app/_config/theme.yml

---
Name: myapptheme
---
SilverStripe\View\SSViewer:
  themes:
    - '$app'
    - '$public'
    - '$default'
```

Run:

```bash
?flush
```

in your browser to apply the configuration.

---

## ✅ Step 4: Add a PSR-4 Autoloading Structure

To keep your PHP code organized and IDE-friendly, add a standard Composer autoload section.

Create a `src/` folder for your PHP classes:

```bash
mkdir -p src/Controllers
```

Then update `composer.json`:

```json
"autoload": {
  "psr-4": {
    "SilverStripe\\Lessons\\": "src/"
  }
}
```

Run:

```bash
composer dump-autoload
```

Now you can place controllers like this:

```php
// src/Controllers/HomeController.php

namespace SilverStripe\Lessons\Controllers;

use SilverStripe\Control\Controller;

class HomeController extends Controller {
    public function index() {
        return [];
    }
}
```

---

## ✅ Step 5: Set Up a Route

Define a route in `app/_config/routes.yml`:

```yaml
---
Name: customroutes
---
SilverStripe\Control\Director:
  rules:
    'home': SilverStripe\Lessons\Controllers\HomeController
```

Visit `/home` to see your new controller in action!

---

## 🎉 You're Ready!

You now have:

- A clean `app/templates/` structure for templates
- A `src/` directory with namespaced PHP classes
- A custom theme and routing setup
- PSR-4 autoloading for future-proof development

This lightweight setup is perfect for small to medium projects where you want **clarity, flexibility, and standard compliance**.

Happy Silverstriping!
