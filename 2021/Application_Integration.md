> #eventbridge
* Eventbridge (CW Events rule) can be configured with a rule that checks all AWS CloudTrail API calls 

> #SQS FIFO
* A FIFO queue is not necessary and may not support the rate of messages (up to 3,000 messages per second

> #SQS 
* The Lambda function can then be configured to poll the SQS queue for messages (event-source mapping)

> #apigw
_ref_: [Neil Davis](https://digitalcloud.training/certification-training/aws-certified-solutions-architect-professional/aws-networking-content-delivery/#:~:text=for%20a%20lambda%20function)
*   *For a Lambda function, you can have the Lambda proxy*integration, or the Lambda custom integration.
*   *For an HTTP endpoint, you can have the HTTP proxy integration*or the HTTP custom integration.
*   *For an AWS service action, you have the AWS integration of the non-proxy type only*

