# Basic Static Website Hosting with S3

This project demonstrates how to host a simple static website using Amazon S3, which is free under the AWS Free Tier. You’ll learn how to create an S3 bucket, upload website files, and configure the bucket for static website hosting.

## Project Overview

This project includes:

- **Amazon S3**: Used for hosting static website files.
- **(Optional) Amazon Route 53**: For managing custom domains.
- **(Optional) AWS CloudFront**: For CDN and caching.

## Getting Started

Follow these steps to set up your static website on Amazon S3:

### 1. Create an S3 Bucket

1. **Sign in to the AWS Management Console** and open the S3 service.
2. **Create a new bucket**:
   - Click **"Create bucket"**.
   - Enter a unique bucket name (e.g., `my-static-website-bucket`).
   - Select a region close to your audience.
   - Uncheck **"Block all public access"**.
   - Click **"Create bucket"**.

3. **Configure the Bucket for Website Hosting**:
   - Go to the bucket and click the **"Properties"** tab.
   - Under **"Static website hosting"**, click **"Edit"**.
   - Enable static website hosting and enter `index.html` as the Index document.
   - Optionally, enter `error.html` for the Error document.
   - Click **"Save changes"**.

### 2. Upload Your Website Files

1. **Prepare your website files**:
   - Create an `index.html` file with basic HTML content.
   - Include any CSS and JavaScript files as needed.

2. **Upload files to the S3 bucket**:
   - Go to the **"Objects"** tab of your bucket.
   - Click **"Upload"**.
   - Drag and drop your files into the upload area and click **"Upload"**.

3. **Set Permissions**:
   - Select your `index.html` file.
   - Click **"Actions"** > **"Make public"**.

### 3. Access Your Website

1. **Find the Website URL**:
   - Go to the **"Properties"** tab of your bucket.
   - Under **"Static website hosting"**, locate the **"Endpoint"** URL.
   - Use this URL to access your static website.

2. **Visit the URL** in your browser to see your website in action.

### 4. (Optional) Set Up a Custom Domain with Route 53

1. **Register a Domain**:
   - Use Route 53 to register a domain or use an existing domain.

2. **Configure Route 53**:
   - Create a hosted zone for your domain.
   - Add an **A Record** pointing to your S3 bucket’s website endpoint.

3. **Update DNS Settings**:
   - Update the DNS settings with your domain registrar to use Route 53 name servers.

### 5. (Optional) Use CloudFront for CDN

1. **Create a CloudFront Distribution**:
   - Open the CloudFront service in the AWS console.
   - Create a new distribution with your S3 bucket’s website endpoint as the origin.
   - Configure caching and other settings.

2. **Update DNS Settings**:
   - Point your domain to the CloudFront distribution URL.

## Summary

- **Amazon S3** for hosting static files.
- **Amazon Route 53** for custom domains (optional).
- **AWS CloudFront** for CDN (optional).

This project leverages the AWS Free Tier to demonstrate basic web hosting capabilities. You can expand it by integrating additional AWS services as needed.

## License

This project is not licensed, feel free to use it and learn.

## Contact

For any questions or feedback, please contact me at https://www.linkedin.com/in/ernandesfranco

---

Happy coding!

