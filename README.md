# Three-Tier-Web-Application-Architecture Project
This project demonstrates the design and deployment of a scalable three-tier web application using a structured Step-by-Step Process. The solution was built using Amazon S3 for static hosting, Amazon CloudFront for content delivery, AWS Lambda for serverless compute, Amazon API Gateway for API management, and Amazon DynamoDB for the database layer.

<img src="Documents/Images/Architecture.png" width="600" height="400">

## Architecture Guide:
1. Create a Storage bucket for your website's files with S3
2. Distribute your content globally with Cloudfront
3. Build the brains of your Application using serverless functions with Lambda
4. Create an API to handle user requests with API Gateway
5. Store and retrieve user data with DynamoDB
6. Connect all these services together seamlessly for your three-tier architecture
# Step 1: Create a Storage bucket for your website's files with S3
To get started, we need a place to store our website’s files and that’s where Amazon S3 comes in.
S3 acts like a huge, scalable hard drive in the cloud, allowing you to store and access your files securely from anywhere.

* Log in to the AWS Management Console as your IAM Admin user.
* Make sure you're the AWS region closest to you.
* Head to the S3 console. (Search S3 on AWS)
* Click Create bucket.
* Enter a unique name for the bucket

<img src="Documents/Images/Bucketname.png" width="600" height="400">

* Leave all other settings as default
* Select Create bucket.
* Click into your created bucket. 
## Upload Website files
Now that we have our storage bucket set, let's fill it up with the actual content 
of our website.
* index.html (the main file of a website)
* style.css (virtual appearance: controls everything from font sizes and colors to layout designs)
* script.js (This is a JavaScript file that adds interaction to your website)


