# Deploying a Static Website on Amazon S3

## Overview
This project demonstrates how to deploy a static HTML website using Amazon S3. The guide includes steps to configure an S3 bucket for static website hosting, modify permissions for public access, and test the website's accessibility via the internet.

## Prerequisites
- An AWS account with appropriate permissions to create and manage S3 buckets.
- Basic knowledge of AWS S3 and IAM policies.

## Steps to Deploy the Static Website

### 1. Create an S3 Bucket
- Navigate to the **S3 service** in the AWS console.
- Click **Create bucket**.
- Provide a unique name for your bucket.

 ![Alt text](createbucket.png)
 
- Choose the region where the bucket should be created.
- Disable **Block all public access** (This will be addressed in later steps).
- Click **Create bucket**.

 ![Alt text](bucket-created.png)
  

### 2. Enable Static Website Hosting
- Select the created S3 bucket.
- Navigate to the **Properties** tab.
  
![Alt text](properties.png)
  
- Scroll down to **Static website hosting**.

  ![Alt text](endpoint.png)
  
- Enable **Use this bucket to host a website**.

![Alt text](enble-staticwebsite.png)
  
- Set the **index document** to `index.html`.
  
![Alt text](index-html.png)
  
- Click **Save changes**.

### 3. Modify Public Access Settings
- Navigate to the **Permissions** tab.
- Click **Edit** under "Block public access".

![Alt text](public-access.png)
  
- Uncheck **Block all public access**.
- Confirm the changes and click **Save**.

![Alt text](confirm-publicaccess.png)

### 4. Apply a Bucket Policy
- In the **Permissions** tab, scroll down to **Bucket policy**.
- Add the following policy to allow public read access to the objects:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
        }
    ]
}
```

- Replace `YOUR_BUCKET_NAME` with the actual name of your S3 bucket.

![Alt text](bucket-policy.png)
  
- Click **Save**.

### 5. Upload Website Files
- Create an `index.html` file with the following content:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My First Website</title>
</head>
<body>
    <h1>Hello world!</h1>
    <p>I'm hosted on Amazon S3!</p>
    <img src="puzzle_cat.jpg">
</body>    
</html>
```

- Upload both `index.html` and `puzzle_cat.jpg` to the root of your S3 bucket.
  
![Alt text](uploadfile.png)

![Alt text](uploaded.png)

### 6. Test the Website
- Navigate to the **Properties** tab in your bucket.
- Click on the **Bucket website endpoint**.

![Alt text](endpoint.png)
  
- If everything is configured correctly, your website should be accessible.
- 
![Alt text](static-website.png)
  
- If you see a `403 Forbidden` error, double-check your bucket policy and public access settings.

![Alt text](error.png)

