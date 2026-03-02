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

# Step 3: Build the brains of your Application using serverless functions with Lambda
In this project, our backend logic will be a simple Lambda function that fetches user data from a DynamoDB table.
To make this functionality accessible externally, we’ll use API Gateway to receive incoming requests and route them to the appropriate Lambda function for processing
* Create a Lambda function to fetch data from a DynamoDB table
* Write the code for your Lambda function.
* Create an API Gateway REST API.
* Create a resource and method to handle GET requests.
* Deploy the API to make it accessible.
###  Create a Lambda function to fetch data from a DynamoDB table
AWS Lambda is a service that lets you run your code without creating or managing a server.
* Search Lambda on AWS Management console.
* Click Create Function.
* For Function  name, enter `RetrieveUserDataAimufua`
* For Runtime, select a runtime using `Node.js`
* For Architecture, select `x86_64`
* Select Create function
## Write Lambda Function Code
* Scroll down to the Code source panel
* Copy and paste the following code into the code editor, replacing Region Region with your actual AWS region (e.g, 'us-west-2)
```// Import individual components from the DynamoDB client package
import { DynamoDBClient } from "@aws-sdk/client-dynamodb";
import { DynamoDBDocumentClient, GetCommand } from "@aws-sdk/lib-dynamodb";

const ddbClient = new DynamoDBClient({ region: 'YOUR_REGION' });
const ddb = DynamoDBDocumentClient.from(ddbClient);

async function handler(event) {
    const userId = event.queryStringParameters.userId;
    const params = {
        TableName: 'UserData',
        Key: { userId }
    };

    try {
        const command = new GetCommand(params);
        const { Item } = await ddb.send(command);
        if (Item) {
            return {
                statusCode: 200,
                body: JSON.stringify(Item),
                headers: {'Content-Type': 'application/json'}
            };
        } else {
            return {
                statusCode: 404,
                body: JSON.stringify({ message: "No user data found" }),
                headers: {'Content-Type': 'application/json'}
            };
        }
    } catch (err) {
        console.error("Unable to retrieve data:", err);
        return {
            statusCode: 500,
            body: JSON.stringify({ message: "Failed to retrieve user data" }),
            headers: {'Content-Type': 'application/json'}
        };
    }
}

export { handler };```


  
* Check: Make sure you've updated the placeholder region YOUR REGION to your own region code.
* Select Deploy This saves your code and makes the function ready to use.
* Check for the Deployment successful in he botton righ corner of the console.
