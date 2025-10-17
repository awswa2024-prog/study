Tag your AWS Resources consistently with AWS Resource Explorer and AWS CloudTrail
https://aws.amazon.com/blogs/mt/tag-your-aws-resources-consistently-with-aws-resource-explorer-and-aws-cloudtrail/

Automating tagging for resources created by AWS Service Catalog
https://aws.amazon.com/blogs/aws-cloud-financial-management/automating-tagging-for-resources-created-by-aws-service-catalog/
Deploying the Solution
If this is your first time using AWS Cloud Development Kit (CDK), you will need to install it on your system to implement the following steps:

Clone the application to your local machine.
git clone https://github.com/aws-samples/resource-autotagger.git
Change to the project directory.
cd resource-autotagger
Install node dependencies for the AWS Cloud Development Kit (AWS CDK) and Lambda functions.
npm install
Execute below step to bootstrap AWS CDK if it was never set up in your AWS account.
cdk bootstrap
Deploy the solution resources with AWS CDK.
cdk deploy
