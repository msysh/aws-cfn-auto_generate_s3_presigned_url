# aws-cfn-auto_generate_s3_presigned_url
This is an AWS Cloud Formation template.
Generate S3 pre-signed URL when a object is created and notify by e-mail.

## Abstract

Generate S3 pre-signed URL when a object is created (uploaded) and notify the URL by e-mail.

## Required Parameter

+ BucketName : S3 bucket name.
+ IAMUserName : IAM user name.
+ SnsDisplayName : SNS display name. It's set to an e-mail subject.
+ Mail : Notify mail address.
+ NameOfSecretsManager : Name of Secrets Manager for access key.

## Deployed AWS component

+ S3
  + Store objects. And using event notify, invoke a lambda.
+ IAM User, Policy, Role
  + Why need IAM user ? -> https://aws.amazon.com/premiumsupport/knowledge-center/presigned-url-s3-bucket-expiration
+ Lambda
  + Invoked by S3. Generate a pre-signed URL of the created object.
+ SNS
  + Using for sending an e-mail which included the generated URL.
+ Secrets Manager
  + Store IAM user's access key id and secret access key.

## Attention

**This template dose not make s3 access logging enable. You have to enable s3 access logging for more secure.**