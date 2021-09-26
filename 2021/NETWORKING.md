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