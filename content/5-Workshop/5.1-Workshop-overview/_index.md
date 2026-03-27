---
title : "Introduction"
date : 2026-03-27
weight : 1
chapter : false
pre : " <b> 4.1. </b> "
---

#### Serverless components
+ **Serverless services** are managed AWS resources that automatically scale, provide high availability, and require no infrastructure management. They allow you to focus on application logic without the operational overhead of provisioning servers.
+ In this architecture, **Amazon S3** provides secure storage, **Amazon CloudFront** acts as a global entry point and security layer, and **AWS Lambda** performs on-demand compute tasks.

#### Workshop overview
In this workshop, you will deploy a 100% serverless environment.
+ **"Frontend Layer"** consists of an **Amazon S3 bucket** hosting static web files. To ensure security, this bucket is kept private, and access is only granted through CloudFront using **Origin Access Control (OAC)**.
+ **"Backend Layer"** utilizes **AWS Lambda** to execute the security assessment logic. It is triggered via a **Lambda Function URL**, allowing the frontend to securely communicate with the backend through the CloudFront distribution. This setup simulates a real-world secure web application where the backend is shielded from direct public internet exposure.

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)
