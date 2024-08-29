Project: Email Notification System using AWS Lambda and SNS
Description:
This project creates an AWS Lambda function that sends an email notification whenever a new file is uploaded to an S3 bucket. The email is sent via Amazon SNS (Simple Notification Service).

Detailed Steps:
1. Create the S3 Bucket
Go to the Amazon S3 console.
Click on “Create bucket.”
Enter a unique name for the bucket (e.g., my-notification-bucket).
Choose the region closest to you.
Leave the default settings and click on “Create bucket.”
2. Set Up SNS (Simple Notification Service)
Go to the Amazon SNS console.
Click on “Create topic.”
Select “Standard” as the type of topic.
Enter a name for the topic (e.g., my-notification-topic).
Click “Create topic.”
After creating the topic, click on it and go to the “Subscriptions” section.
Click “Create subscription.”
Under “Protocol,” select Email.
In the “Endpoint” field, enter your email address.
Click “Create subscription.”
Check your email and confirm the subscription.
