> #eventbridge
* Eventbridge (CW Events rule) can be configured with a rule that checks all AWS CloudTrail API calls 

> #SQS FIFO
* A FIFO queue is not necessary and may not support the rate of messages (up to 3,000 messages per second

> #SQS 
* The Lambda function can then be configured to poll the SQS queue for messages (event-source mapping)
