# AWS Lambda and SNS Email Notification System

## Description
This project creates an AWS Lambda function that sends an email notification whenever a new file is uploaded to an S3 bucket. The email is sent via Amazon SNS (Simple Notification Service).

## Steps

### 1. Create the S3 Bucket

1. Go to the [Amazon S3 console](https://s3.console.aws.amazon.com/s3/home).
3. Click on **Create bucket**.
   <img width="1016" alt="Screenshot 2024-08-29 at 2 44 34 PM" src="https://github.com/user-attachments/assets/f42e7d92-0acb-4835-aae3-c641fefa19f6">
5. Enter a unique name for the bucket (e.g., `my-notification-bucket`).
6. Choose the region closest to you.
   <img width="806" alt="Screenshot 2024-08-29 at 2 45 36 PM" src="https://github.com/user-attachments/assets/e59c5645-ed12-4e1c-bf71-3d25d772d08a">
8. Leave the default settings and click **Create bucket**.
   <img width="147" alt="Screenshot 2024-08-29 at 2 47 06 PM" src="https://github.com/user-attachments/assets/e72aef18-83d3-4b42-8f32-9ab059d78e89">

### 2. Set Up SNS (Simple Notification Service)

1. Go to the [Amazon SNS console](https://console.aws.amazon.com/sns/home).
2. Click on **Create topic**.
4. Enter a name for the topic (e.g., `my-notification-topic`).
5. Click **Create topic**.
   <img width="907" alt="Screenshot 2024-08-29 at 2 50 02 PM" src="https://github.com/user-attachments/assets/72ae7825-a2ff-46a6-9d94-4ba89ac0561f">
5. Select **Standard** as the type of topic.
   <img width="1090" alt="Screenshot 2024-08-29 at 2 52 08 PM" src="https://github.com/user-attachments/assets/e780ca4c-2d0c-4d35-987a-53767a534db8">
7. Create the topic
   <img width="130" alt="Screenshot 2024-08-29 at 2 53 21 PM" src="https://github.com/user-attachments/assets/de93ca01-40e1-4fce-9370-4807f400f6d1">
9. After creating the topic, click on it and go to the **Subscriptions** section.
    <img width="1058" alt="Screenshot 2024-08-29 at 2 54 34 PM" src="https://github.com/user-attachments/assets/8f1f3350-b7d9-4771-9858-f578cb56d908">
10. Click **Create subscription**.
    <img width="1058" alt="Screenshot 2024-08-29 at 2 57 01 PM" src="https://github.com/user-attachments/assets/eba3acd8-bf72-4d4c-90d7-d0469c7e91bd">
11. Under **Protocol**, select **Email**.
12. In the **Endpoint** field, enter your email address.
    <img width="1093" alt="Screenshot 2024-08-29 at 2 58 51 PM" src="https://github.com/user-attachments/assets/0be6901c-f6e2-4204-bef5-160cbfd58570">
13. Click **Create subscription**.
    <img width="182" alt="Screenshot 2024-08-29 at 3 00 03 PM" src="https://github.com/user-attachments/assets/43a64030-a837-49d7-a6db-bcc1b08db3d2">
14. Check your email and confirm the subscription.
    <img width="1090" alt="Screenshot 2024-08-29 at 3 01 14 PM" src="https://github.com/user-attachments/assets/ae9ecff6-f5db-4aff-8be4-24190c347b8e">

### 3. Create the Lambda Function

1. Go to the [AWS Lambda console](https://console.aws.amazon.com/lambda/home).
2. Click on **Create function**.
3. Select **Author from scratch**.
4. Enter a name for your function (e.g., `S3FileUploadNotifier`).
5. Choose the runtime (e.g., `Python 3.8` or `Node.js 14.x`).
6. Under **Permissions**, choose an existing role if you have one or let Lambda create a new role with basic Lambda permissions.
7. Click **Create function**.

### 4. Add Code to the Lambda Function

For this example, use Python:

```python
import json
import boto3

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    sns = boto3.client('sns')
    
    # Get bucket and file name from the event
    bucket_name = event['Records'][0]['s3']['bucket']['name']
    file_name = event['Records'][0]['s3']['object']['key']
    
    # Compose the message
    message = f"A new file {file_name} was uploaded to the bucket {bucket_name}."
    
    # Publish the message to the SNS topic
    sns.publish(
        TopicArn='arn:aws:sns:your-region:your-account-id:my-notification-topic',
        Message=message,
        Subject='S3 File Upload Notification'
    )
    
    return {
        'statusCode': 200,
        'body': json.dumps('Notification sent successfully!')
    }
