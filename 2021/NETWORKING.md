## Networking
> #alb, #global_accelerator
* Alternatively, when using ALBs, the underlying IP addresses of the compute nodes
    supporting the ALB are subject to change, for example, in response to scaling events.
    *Because an ALB is not supported by a static compute node, or static group of compute
    nodes, it does not support direct integration with Elastic IP addresses. Static IP
    addresses can still be provided to consumers of ALB-based applications via AWS
    Global Accelerator, a service that provides fixed entry points to your application* 

* A 404 HTTP status code indicates that the object has not been found    
> #nlb
* There is no security group associated with an NLB
* Note that NLBs do not have security groups configured and pass connections straight to EC2 instances with the source IP of the client preserved (when registered by instance-id).
* With NLBs, when you register EC2 instances as targets, you must ensure that the security groups for these instances allow traffic on both the listener port and the health check port
> #waf
* WAF cannot be configured to directly trigger a Lambda function
> #endpoints  

There are 
* VPC Gateway Endpoint
* VPC Interface Endpoint
* VPC Service Endpoint

> accelerator

There are
 * S3 Transfer accelerator
 * Global accelerator

> #route53
* In Route 53 you are limited (by default) to five requests per second per AWS account. If you submit more than five requests per second, Amazon Route 53 returns an HTTP 400 error (Bad request)  

> #s3 transfer accelator  
_ref_: SAP.Neal.Practice Exam 2 (exam mode) - Digital Cloud Training (9_27_2021 12_08_07 AM).html Q10
* Amazon S3 Transfer Acceleration enables fast, easy, and secure **uploads** of files over long distances between a client and an S3 bucket. Transfer Acceleration takes advantage of Amazon CloudFront’s globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path   
* Multipart upload transfers parts of the file in parallel and can speed up performance. This should definitely be built into the application code. Multipart upload also handles the failure of any parts gracefully, allowing for those parts to be retransmitted.

* **Transfer Acceleration in combination with multipart upload will offer significant speed improvements when uploading data**

* **CloudFront can offer performance improvements for downloading data** but to improve **upload transfer times, Transfer Acceleration should be used**