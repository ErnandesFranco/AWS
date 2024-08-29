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
3. Enter a name for the topic (e.g., `my-notification-topic`).
4. Click **Create topic**.
   <img width="907" alt="Screenshot 2024-08-29 at 2 50 02 PM" src="https://github.com/user-attachments/assets/72ae7825-a2ff-46a6-9d94-4ba89ac0561f">
5. Select **Standard** as the type of topic.
   <img width="1090" alt="Screenshot 2024-08-29 at 2 52 08 PM" src="https://github.com/user-attachments/assets/e780ca4c-2d0c-4d35-987a-53767a534db8">
6. Create the topic

   <img width="130" alt="Screenshot 2024-08-29 at 2 53 21 PM" src="https://github.com/user-attachments/assets/de93ca01-40e1-4fce-9370-4807f400f6d1">
7. After creating the topic, click on it and go to the **Subscriptions** section.
    <img width="1058" alt="Screenshot 2024-08-29 at 2 54 34 PM" src="https://github.com/user-attachments/assets/8f1f3350-b7d9-4771-9858-f578cb56d908">
8. Click **Create subscription**.

    <img width="1058" alt="Screenshot 2024-08-29 at 2 57 01 PM" src="https://github.com/user-attachments/assets/eba3acd8-bf72-4d4c-90d7-d0469c7e91bd">
9. Under **Protocol**, select **Email**.
10. In the **Endpoint** field, enter your email address.
    <img width="1093" alt="Screenshot 2024-08-29 at 2 58 51 PM" src="https://github.com/user-attachments/assets/0be6901c-f6e2-4204-bef5-160cbfd58570">
11. Click **Create subscription**.

    <img width="182" alt="Screenshot 2024-08-29 at 3 00 03 PM" src="https://github.com/user-attachments/assets/43a64030-a837-49d7-a6db-bcc1b08db3d2">
12. Check your email and confirm the subscription.
    <img width="1090" alt="Screenshot 2024-08-29 at 3 01 14 PM" src="https://github.com/user-attachments/assets/ae9ecff6-f5db-4aff-8be4-24190c347b8e">

### 3. Create the Lambda Function

1. Go to the [AWS Lambda console](https://console.aws.amazon.com/lambda/home).
2. Click on **Create function**.

   <img width="781" alt="Screenshot 2024-08-29 at 3 10 03 PM" src="https://github.com/user-attachments/assets/e96d73e5-eb11-410e-8cc2-7466c1a24a65">
   
3. Select **Author from scratch**.
4. Enter a name for your function (e.g., `S3FileUploadNotifier`).
5. Choose the runtime (e.g., `Python 3.8`).
   <img width="815" alt="Screenshot 2024-08-29 at 3 11 00 PM" src="https://github.com/user-attachments/assets/ea25d592-6621-47c0-ad18-3aab2af7d750">
6. Under **Permissions**, choose an existing role if you have one or let Lambda create a new role with basic Lambda permissions.
7. Click **Create function**.

   <img width="152" alt="Screenshot 2024-08-29 at 3 11 46 PM" src="https://github.com/user-attachments/assets/bcc1db7a-1314-47e8-8f8b-1eca4e823101">


### 4. Add Code to the Lambda Function

For this example, use Python:

# Copy and edit the code below: (Don't copy this line.)
<code>
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
</code>
# This is the end of the code. (Don't copy this line.)
**Replace your-region and your-account-id with the appropriate values from your SNS topic's ARN.**

### 5. Set Up S3 Trigger for Lambda
1. In the Lambda function page, go to the Designer section and click Add trigger.
   <img width="644" alt="Screenshot 2024-08-29 at 3 28 15 PM" src="https://github.com/user-attachments/assets/78196eeb-0bc2-423c-acd8-b293cca8ab66">
2. Choose S3 as the trigger.
3. Select the S3 bucket you created earlier.
4. Set Event type to All object create events.
   <img width="811" alt="Screenshot 2024-08-29 at 3 30 13 PM" src="https://github.com/user-attachments/assets/1d49918d-a017-40ef-8377-d2ddceda3832">
5. Click Add.
   <img width="811" alt="Screenshot 2024-08-29 at 3 30 56 PM" src="https://github.com/user-attachments/assets/0b649238-12d1-490b-b09e-1c9f1396c6ce">

### 5. Set Up the SNS Topic as a Destination
1. Configure the destination like this:
   <img width="809" alt="Screenshot 2024-08-29 at 3 46 42 PM" src="https://github.com/user-attachments/assets/00e8bdbc-a350-4529-a1fa-e84a61fcaa96">
2. Click on Save.

   <img width="80" alt="Screenshot 2024-08-29 at 3 47 36 PM" src="https://github.com/user-attachments/assets/268341c4-6d93-4198-8b56-b56877397bc8">

### 6. Testing the Setup
1. Upload a file to your S3 bucket.
   ![image](https://github.com/user-attachments/assets/fa410d25-6824-400a-942e-d8164dfb9692)

   <img width="1307" alt="Screenshot 2024-08-29 at 3 33 52 PM" src="https://github.com/user-attachments/assets/8b972d00-2a26-4cb5-93ec-0437348a5464">
2. Check your email for the notification sent by SNS.
   <img width="1093" alt="Screenshot 2024-08-29 at 3 50 22 PM" src="https://github.com/user-attachments/assets/3608a752-2183-4b7b-b0d8-93c957d9ad41">
   
3. Free Tier Resources Used
4. AWS Lambda: 1 million free requests per month.
5. Amazon S3: 5 GB of free storage and 20,000 GET requests per month.
6. Amazon SNS: 1 million free publishes or deliveries per month.

### Summary
Amazon S3: Used for storing and triggering notifications on file uploads.
Amazon SNS: Used for sending email notifications.
AWS Lambda: Used for processing S3 events and sending notifications.
This project leverages the AWS Free Tier to demonstrate basic email notification capabilities. You can expand it by integrating additional AWS services as needed.

### License
This project is not licensed. Feel free to use it and learn from it.

### Contact
For any questions or feedback, please contact me at [LinkedIn](https://www.linkedin.com/in/ernandesfranco/).
