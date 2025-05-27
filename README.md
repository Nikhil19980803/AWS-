Step 1: Create an S3 Bucket
Go to the S3 console

Click Create Bucket

Bucket name must match your domain name (e.g., www.example.com) if you're using a custom domain

Uncheck "Block all public access"
![image](https://github.com/user-attachments/assets/56499d2a-98a9-4981-8c90-d50494370266)

Acknowledge warning → Create Bucket

Step 2: Upload Website Files to S3
Open your S3 bucket

Click Upload

Drag & drop your website files (index.html, styles.css, etc.)

Upload

Step 3: Enable Static Website Hosting

Go to Properties tab of your S3 bucket

Scroll to Static Website Hosting

Choose: Enable

Enter:

Index document: index.html

Error document: error.html (optional)

Save changes

![image](https://github.com/user-attachments/assets/9461b168-aca8-4cbe-acfe-a797d29c06eb)

Step 4: Make Files Public
To allow access to your site:

Option A: Use a Bucket Policy
Go to Permissions > Bucket Policy, and paste this (replace with your bucket name):

json
Copy
Edit
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}

Step 5: Test S3 Website URL
Go to Properties > Static website hosting
Click the Endpoint URL to see your site live (e.g., http://your-bucket.s3-website-us-east-1.amazonaws.com)

Step 6: Set Up CloudFront for CDN + HTTPS
Go to CloudFront Console

Click Create Distribution

Under Web, click Get Started

Fill in:

Origin Domain: your S3 website endpoint (copy from Step 5)

Viewer Protocol Policy: Redirect HTTP to HTTPS

Cache Policy: Use default or optimized

Create Distribution

⚠️ CloudFront takes 10–20 mins to deploy.

