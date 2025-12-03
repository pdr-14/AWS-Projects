# AWS S3 Static Web Hosting

This repository contains the frontend code for a Cloud-based Credit Card Application form. This guide documents the process of hosting this static website using **Amazon Simple Storage Service (S3)**.

## 📋 Project Overview
* **Goal:** Host a responsive HTML/CSS/JS web application on AWS.
* **Service Used:** AWS S3 (Static Website Hosting).
* **Architecture:** Serverless Static Frontend.

---

## 🚀 Deployment Guide

Follow these steps to deploy this project to the cloud.

### Step 1: Create an S3 Bucket
1.  Log in to the **AWS Management Console**.
2.  Navigate to **S3** and click **Create bucket**.
3.  **Bucket Name:** Enter a globally unique name (e.g., `my-cc-app-frontend-2024`).
4.  **Region:** Select the region closest to your target audience (e.g., `us-east-1`).
5.  **Object Ownership:** Keep default (ACLs disabled).
6.  **Block Public Access settings:**
    * [ ] **Uncheck** "Block all public access".
    * [x] Check the acknowledgment box warning that objects will be public.
    * *Note: This is required for a public website.*
7.  Click **Create bucket**.

### Step 2: Enable Static Website Hosting
1.  Click on your newly created bucket name.
2.  Go to the **Properties** tab.
3.  Scroll to the bottom to **Static website hosting**.
4.  Click **Edit** -> Select **Enable**.
5.  **Index document:** Enter `index.html`.
6.  **Error document:** Enter `error.html` (or `index.html` if you don't have one).
7.  Click **Save changes**.

### Step 3: Configure Bucket Policy (Permissions)
To make the website viewable to the internet, you must add a bucket policy.

1.  Go to the **Permissions** tab.
2.  Scroll down to **Bucket policy** and click **Edit**.
3.  Paste the following JSON code (Replace `YOUR-BUCKET-NAME` with your actual bucket name):

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
        }
    ]
}