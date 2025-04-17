---
layout: post
title: "Build your own CMS Part4: NZTA Road Condition Reporting Platform – Product Requirements (MVP)"
date: 2025-04-16 13:00:00 +0800
# categories: [SilverStripe]
# tags: [SilverStripe, CMS]
---



# 🚧 NZTA Road Condition Reporting Platform – Product Requirements (MVP)

This document outlines the core functional requirements and implementation plan for a citizen-facing road condition reporting platform, built with Silverstripe CMS.

---

## ✅ Core Features Overview

1. **User Registration**
2. **User Login / Logout**
3. **Road Condition Report Submission**
4. **User Report History Query**

---

## 🧱 Feature 1: User Registration

### 🎯 Goal
Allow citizens to create accounts in order to report road conditions and track their submissions.

### 🔧 Functional Breakdown

| Feature           | Description                            |
|------------------|----------------------------------------|
| Form Fields       | Full Name, Email, Password, Confirm Password |
| Validation        | Email must be unique                  |
| Password Policy   | Minimum 6 characters (can be extended)|
| Data Storage      | Stored in Silverstripe's `Member` table |
| Auto-login Option | Optional login after successful registration |
| Error Feedback    | Real-time and server-side validation messages |

---

## 🧱 Feature 2: User Login / Logout

### 🎯 Goal
Allow registered users to log in and securely manage their reporting actions.

### 🔧 Functional Breakdown

| Feature        | Description                            |
|----------------|----------------------------------------|
| Login Fields   | Email, Password                        |
| Auth System    | Based on `MemberAuthenticator`         |
| Session Handling | Maintain session after login          |
| Logout         | Log out and redirect to homepage       |
| Access Control | Only logged-in users can access submission and query features |
| Feedback       | Login success/failure messages         |

---

## 🧱 Feature 3: Road Report Submission

### 🎯 Goal
Allow users to report road issues via a structured form, optionally with images and location details.

### 🔧 Functional Breakdown

| Feature         | Description                            |
|----------------|----------------------------------------|
| Form Fields     | Description, Location, Time, Image(s)  |
| User Binding    | Reports are linked to logged-in `Member` |
| Media Upload    | Supports multiple image uploads        |
| Status Field    | New reports start with "Pending" or "Unprocessed" |
| Validation      | Required fields with validation hints |
| Backend Model   | Custom `RoadReport` DataObject         |
| Admin Management| Manage reports via `ModelAdmin`        |
| Post-Submit UX  | Confirmation message + redirect to "My Reports" |

---

## 🧱 Feature 4: User Report Query

### 🎯 Goal
Enable users to track the status of their previously submitted reports.

### 🔧 Functional Breakdown

| Feature         | Description                            |
|----------------|----------------------------------------|
| Data Source     | Filter reports by current logged-in user |
| Display Fields  | Description, Time, Location, Status, Thumbnail |
| Sorting         | Sorted by submission time (newest first) |
| Pagination      | Paginate with 10 reports per page      |
| Permissions     | Users can only see their own reports   |

---

## 🌐 Common Features (Cross Module)

| Area            | Description                            |
|----------------|----------------------------------------|
| CMS Management  | `ModelAdmin` enables admin view and edit |
| Security        | Auth control using `Member` login status |
| Routing         | Use `routes.yml` to define endpoints (e.g. `/register`, `/submit`) |
| Template System | Each frontend page needs a corresponding `.ss` template |
| Form Handling   | Form API for validation + submission   |

---

## 🚀 Optional Future Enhancements

- Geolocation support for map-based submissions
- Admin report processing and state transitions
- Category tagging (e.g. pothole, broken light)
- Email notification system
- Dashboard and visual analytics

---

## ✅ Suggested Development Flow

1. Implement **User Registration + Login**
2. Build **Report Submission Form + Backend Model**
3. Create **User Report History View**

---

*This markdown planning document is intended to guide structured Silverstripe CMS feature development.*
