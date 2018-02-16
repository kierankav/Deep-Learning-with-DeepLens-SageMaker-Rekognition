# 4 - Approval Verification Website

## 1. Create Cognito Identity Pool

_Cognito will be used to assign temporary credentials for securely accessing AWS resources used in this workshop. (For more information: https://aws.amazon.com/cognito/)_

1.	In the AWS Console, click on “Services” in the top, left-hand corner of the screen, and click on “Cognito” (you can find it by typing _cog_ into the search field at the top of the screen).
2.	Click “Manage Federated Identities”, and then click “Create new identity pool”.
3.	For “Identity pool name”, enter _ML_ID_Pool_
4.	Select “Enable access to unauthenticated identities” from the “Unauthenticated identities” collapsible section.
5.	Click “Create Pool”.
6.	In the screen that appears, click “Allow” (in the bottom, right-hand corner of the screen).
7.	Note the identity pool ID that is displayed in the center of the screen (please see the following example screenshot).

![](Lab4-Images/Cognito_ID_Pool_ID.png)

8.	Copy that into a text file because you will use it in a later step.

## 2. Update the Cognito IAM Role to Allow Access to AWS Resources

1.	In the AWS Console, click on “Services” in the top, left-hand corner of the screen, and click on “IAM” (you can find it by typing _iam_ into the search field at the top of the screen).
2.	On the left-hand side of the screen, click "Roles".
3.	In your list of roles, click on “Cognito_ML_ID_PoolUnauth_Role”, and click “Attach policy”.
4.	In the Search field, type _s3_, and then select “AmazonS3FullAccess” (i.e. click the checkbox to the left of “AmazonS3FullAccess”).
5.	In the Search field, type _step_, and then select “AWSStepFunctionsFullAccess”.
6.	In the Search field, type _rek_, and then select “AmazonRekognitionFullAccess”.
7.	In the Search field, type _dyn_, and then select “AmazonDynamoDBFullAccess”.
8.	In the Search field, type _ses_, and then select “AmazonSESFullAccess”.
9.	In the Search field, type _api_, and then select “AmazonAPIGatewayInvokeFullAccess”.
10.	Click “Attach policy” (at the bottom, right-hand corner of the screen).
11.	Repeat steps 1 to 10 for the “Cognito_ML_ID_PoolAuth_Role”.


## Create a Bucket for Uploading Images of Faces (This section to be moved to Lab 1 or 2)

_This is the bucket to which DeepLens will upload images._

1.	In the AWS Console, click on “Services” in the top, left-hand corner of the screen, and click on “S3” (you can find it by typing _s3_ into the search field at the top of the screen).
2.	Click "Create bucket", and enter the following details:
*	Bucket name: _[Your name or username]-ml-bucket_
*	Region: US East (N. Virginia)
3.	Click "Create".

![](Lab4-Images/ML_Bucket.png)

## 3. Create S3 Bucket for Static Website Hosting

_We will use a static website to host a web-page that will be used for approving unrecognized faces to be added to our Rekognition collection._

1. In the AWS Console, click on “Services” in the top, left-hand corner of the screen, and click on “S3” (you can find it by typing _s3_ into the search field at the top of the screen).
2. Click "Create bucket", and enter the following details:
*	Bucket name: [Your name or username]-web
*	Region: US West (Oregon)
2.	Click "Create".
3.	Now, in your list of S3 buckets, click on the bucket you just created (i.e. [Your name or username]-web).
4.	Click on the "Properties" tab and click on "Static website hosting".
5.	Select the "Use this bucket to host a website" option.
6.	In the "Index document" textbox, type index.html
7.	Click "Save".


## 4. Create the Approval Static Web Page

