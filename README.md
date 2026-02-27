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

  <img src="Documents/Images/webfiles.png" width="600" height="400">
  
# Step 2: Distribute your content globally with Cloudfront
* ## Create a CloudFront Distribution
Amazon CloudFront is a Content Delivery Network (CDN) Which means it speeds up the distribution of your static and dynamic web content, such as html, css, js and image files. Amazon CloudFront distribution is a configuration that controls how CloudFront delivers your content to users. It defines the location of your website files (known as the origin), determines how content is cached, and sets other delivery options such as security settings and performance rules.
* Head to CloudFront Console

<img src="Documents/Images/Createdistribution.png" width="600" height="400">  

* In the distribution Options panel, enter a name to match your S3 bucket in the Distribution name.
* Now for the Distribution type, select the Single website or app option.
* Select `Next`
* In the `Origin` panel, select the Browse S3 button
<img src="Documents/Images/S3origin.png" width="600" height="400"> 

* Select your bucket name and click Choose
* Keep the default in the Settings panel and select Next at the bottom.
* For Web Application firewall (WAF), select `Do not enable security protections`
* Let's review the configuration. Select `Create distribution` if everything looks good.

  Congratulation! You've just set up a CloudFront distribution.

## Update your S3 bucket's settings 
* In your CloudFront distribution's settings page, select Copy policy.
* Next, select the shortcut under the popup message. It lets go straight to your S3 bucket's Permissions tab
* Select `Edit`
* Past the Policy that you copied into the policy editor.
<img src="Documents/Images/policy.png" width="600" height="400"> 

ClICK `Save Changes`
