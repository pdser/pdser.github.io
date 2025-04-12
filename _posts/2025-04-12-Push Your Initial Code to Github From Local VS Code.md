---
layout: post
title: "Build your own CMS Part2: Push Your Initial Code to Github From Local VS Code"
date: 2025-04-12 10:00:00 +0800
# categories: [SilverStripe]
# tags: [SilverStripe, CMS]
---


# 🚀 Push Local Project to GitHub (VS Code + Command Line)

This is a step-by-step guide for developers to push an existing local project to a GitHub repository using **VS Code** and its built-in terminal. Perfect for blog posts or internal documentation.

---

## 📦 Project Context

- Local project path: `D:\code\nzta`
- Tools: VS Code + Git + GitHub
- Goal: Upload code to GitHub repository at https://github.com/yourname/nzta

---

## 🧰 Prerequisites

Make sure the following tools are installed and configured:

- [x] Visual Studio Code
- [x] Git (with username and email configured)
- [x] A GitHub account with an empty repository created (without initializing with a README)

---

## 🧭 Step 1: Open the Project in VS Code

1. Launch VS Code
2. Go to `File > Open Folder...`
3. Select your project folder `D:\code\nzta`
4. Ensure you can see your project files in the Explorer panel

---

## 🧱 Step 2: Initialize Git and Push to GitHub

Open the terminal in VS Code:

```bash
# Open terminal
Terminal > New Terminal
```

Then run the following commands:

```bash
# Initialize the Git repository
git init

# Link to your remote GitHub repository
git remote add origin https://github.com/yourname/nzta.git

# Stage all files
git add .

# Make the first commit
git commit -m "Initial commit"

# Set the main branch to 'main' (recommended)
git branch -M main

# Push the code to GitHub
git push -u origin main
```

> ✅ Note: On first push, you might be prompted to authenticate with GitHub. Use GitHub CLI or a Personal Access Token (PAT) for best results.

---

## 🔄 Step 3: Keep Updating the Repository

For every code update, simply run:

```bash
git add .
git commit -m "Your update message"
git push
```

This will sync your local changes to GitHub.

---

## 📌 Common Issues

- **Error: refusing to merge unrelated histories**:
  ```bash
  fatal: refusing to merge unrelated histories
  ```
  Solution:
  ```bash
  git push -f origin main
  ```

---

## 🧪 Verification

Open your GitHub repository in a browser. If you see your code there — congrats, you did it ✅

---

## 🧑‍💻 Use Cases

- Initializing version control for local projects
- Preparing codebase for team collaboration
- Perfect for blog tutorials or onboarding documentation

---

Happy coding 🚀
