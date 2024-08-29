# AWS Lambda and SNS Email Notification System

## Description
This project creates an AWS Lambda function that sends an email notification whenever a new file is uploaded to an S3 bucket. The email is sent via Amazon SNS (Simple Notification Service).

## Steps

### 1. Create the S3 Bucket

1. Go to the [Amazon S3 console](https://s3.console.aws.amazon.com/s3/home).
2. Click on **Create bucket**.
3. Enter a unique name for the bucket (e.g., `my-notification-bucket`).
4. Choose the region closest to you.
5. Leave the default settings and click **Create bucket**.

### 2. Set Up SNS (Simple Notification Service)

1. Go to the [Amazon SNS console](https://console.aws.amazon.com/sns/home).
2. Click on **Create topic**.
3. Select **Standard** as the type of topic.
4. Enter a name for the topic (e.g., `my-notification-topic`).
5. Click **Create topic**.
6. After creating the topic, click on it and go to the **Subscriptions** section.
7. Click **Create subscription**.
8. Under **Protocol**, select **Email**.
9. In the **Endpoint** field, enter your email address.
10. Click **Create subscription**.
11. Check your email and confirm the subscription.

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
