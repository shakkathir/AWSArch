# Caching

![AWS Cache Options!](SAP.CACHE.DIAG.001.JPG "AWS Cache Options")
_ref_: Stephane PDF

> #cloudfront,  #logging, #kms,
   
* In this case CloudFront delivers the logs to AWS Logs Delivery account. Then *AWS Logs Delivery account* delivers the logs to S3. __ref__: [Exam topics Page 69](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/69/#:~:text=in%20this%20case%20cloudfront%20delivers%20the%20logs%20to%20aws%20logs%20delivery%20account.%20then%20aws%20logs%20delivery%20account%20delivers%20the%20logs%20to%20s3)
* If you enabled server-side encryption for your Amazon S3 bucket using AWS KMS-managed keys (SSE-KMS) with a customer-managed Customer Master Key (CMK), you must add the following to the key policy for your CMK to enable writing log files to the bucket. You cannot use the default CMK because CloudFront won't be able to upload the log files to the bucket. __ref__: [aws docs](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/AccessLogs.html#:~:text=for%20the%20bucket-,When%20you%20create%20or,files%20to%20the%20bucket,-.%20If%20your%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%09%09%09%09%09%09account)
