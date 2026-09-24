# AWS S3 Static Portfolio Website

A small static portfolio website hosted using **Amazon S3** as part of my AWS cloud engineering learning journey.

The goal of this project was not only to host a website, but to understand how S3 storage, encryption, IAM permissions, and public access controls work together.

## What I Built

I created a simple HTML/CSS portfolio website and deployed it to an Amazon S3 bucket using S3 Static Website Hosting.

The website contains:

* About section
* AWS/cloud skills I'm currently learning
* Current cloud project information
* Basic responsive styling

## AWS Services Used

* **Amazon S3** — website hosting and object storage
* **AWS IAM** — identity and permission management

## Architecture

```text
Internet
   │
   ▼
S3 Static Website
   │
   ▼
cloud-portfolio-2026
   ├── index.html
   └── style.css
```

## S3 Configuration

### Bucket

Bucket name:

```text
cloud-portfolio-2026
```

The bucket stores the website files as S3 objects.

### Encryption

The bucket uses:

**SSE-S3 (Server-Side Encryption with Amazon S3 managed keys)**

This means S3 automatically encrypts objects stored in the bucket.

### Static Website Hosting

S3 Static Website Hosting was enabled with:

```text
Index document: index.html
```

The website was then accessed through the S3 website endpoint.

## IAM and Least Privilege

I created and used an IAM user called `ssshai` instead of using the root account for normal AWS operations.

The IAM user was given:

**AmazonS3ReadOnlyAccess**

I tested the permission by attempting to upload another object.

The result was:

```text
Upload failed / Access Denied
```

This confirmed that the IAM user could read S3 resources but did not have permission to upload objects.

This helped me understand the principle of **least privilege** — users should receive only the permissions they need.

## Public Access and Bucket Policy

Initially, **Block Public Access** was enabled.

When I tried to access the website, S3 returned:

```text
403 Forbidden
```

This demonstrated that enabling static website hosting does not automatically make the objects publicly accessible.

For this learning project, I disabled Block Public Access and added a bucket policy allowing public `s3:GetObject` access to the website objects.

The policy allowed:

```text
s3:GetObject
```

but did not grant the public permission to:

* Upload objects
* Delete objects
* Modify objects

## What I Learned

Through this project I practiced:

* Creating an S3 bucket
* Understanding buckets and objects
* Uploading objects to S3
* S3 server-side encryption
* Block Public Access
* IAM users and permissions
* Least-privilege access
* S3 bucket policies
* Static website hosting
* Troubleshooting `AccessDenied` and `403 Forbidden` errors
* Understanding the difference between storage configuration and access permissions

## Security Note

This project uses the traditional S3 static website hosting approach for learning purposes.

For a production website, I would consider keeping the S3 bucket private and using **Amazon CloudFront with Origin Access Control (OAC)** so that users access the website through CloudFront rather than directly accessing the S3 bucket.

## Project Status

**Completed ✅**

Next step in my AWS learning roadmap:

**Amazon VPC — networking, subnets, route tables and network ACLs.**
