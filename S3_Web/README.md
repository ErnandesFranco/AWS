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
     <img width="828" alt="Screenshot 2024-08-25 at 12 07 22 AM" src="https://github.com/user-attachments/assets/8e158e17-3576-45b8-bfde-125e49d734bb">
   - Enter a unique bucket name (e.g., `my-static-website-bucket`).
   - Select a region close to your audience.
     <img width="807" alt="Screenshot 2024-08-25 at 12 09 09 AM" src="https://github.com/user-attachments/assets/e9b68018-7405-4e52-a8fa-5aede837e3c1">
   - Uncheck **"Block all public access"**.
     <img width="807" alt="Screenshot 2024-08-25 at 12 09 59 AM" src="https://github.com/user-attachments/assets/8fb84c67-de0f-450f-a19d-56af96123642">
   - Click **"Create bucket"**.
     <img width="147" alt="Screenshot 2024-08-25 at 12 10 37 AM" src="https://github.com/user-attachments/assets/7090f735-4fd9-4546-8b58-5e1834e575dc">

3. **Configure the Bucket for Website Hosting**:
   - Go to the bucket and click the **"Properties"** tab.
     <img width="665" alt="Screenshot 2024-08-25 at 12 13 01 AM" src="https://github.com/user-attachments/assets/1cb53a84-fe6c-45ab-812f-ea8832708f58">
   - Under **"Static website hosting"**, click **"Edit"**.
   - Enable static website hosting and enter `index.html` as the Index document.
     <img width="665" alt="Screenshot 2024-08-25 at 12 14 17 AM" src="https://github.com/user-attachments/assets/bcf1b16b-882c-40f6-ad81-eb711a7af110">
   - Optionally, enter `error.html` for the Error document.
   - Click **"Save changes"**.
     <img width="139" alt="Screenshot 2024-08-25 at 12 14 43 AM" src="https://github.com/user-attachments/assets/b8caef68-6670-48ab-b0eb-f49c1f279575">


### 2. Upload Your Website Files

1. **Prepare your website files**:
   - Create an `index.html` file with basic HTML content.
   - Include any CSS and JavaScript files as needed.

2. **Upload files to the S3 bucket**:
   - Go to the **"Objects"** tab of your bucket.
   - Click **"Upload"**.
   - Drag and drop your files into the upload area and click **"Upload"**.
     <img width="665" alt="Screenshot 2024-08-25 at 12 16 24 AM" src="https://github.com/user-attachments/assets/68f26702-1232-4c5a-b476-71fd37bed3d2">


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

