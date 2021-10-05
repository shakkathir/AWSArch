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
* VPC Gateway Endpoint (Caller side )
* VPC Interface Endpoint (Caller side)
* VPC Endpoint Service (Server side URL/Endpoint)

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

* [Transfer Acceleration over a fully available 1 Gbps can theoretically move around 10TB/Day.](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/55/#:~:text=1%20gbps%20%3D%20(1024%2F8)%20mbps%20%3D%20128%20mbps)

_ref_: [ExamTopics : Q696 : Page 70](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/70/#:~:text=https%20between%20viewers%20and%20cloudfront)  
* **HTTPS between viewers and CloudFront** – You can use a certificate that was issued by a trusted certificate authority (CA) such as Comodo, DigiCert, or Symantec, or you can use a certificate provided by AWS Certificate Manager (ACM). 

* **HTTPS between CloudFront and a custom origin** – If the origin is not an Elastic Load Balancing (ELB) load balancer, such as Amazon EC2, the certificate must be issued by a trusted CA such as Comodo, DigiCert, or Symantec. If your origin is an ELB load balancer, you can also use a certificate provided by ACM. 

* **For SSL Between ELB and EC2:** Amazon-issued certificates can’t be installed on an EC2 instance. To enable end-to-end encryption, you must use a third-party SSL certificate. Install the third-party certificate on an EC2 instance. Then, associate the third-party certificate with a load balancer by importing it into AWS Certificate Manager (ACM) (https://aws.amazon.com/premiumsupport/knowledge-center/acm-ssl-certificate-ec2-elb/) The requirement of 3rd party cert between ELB and EC2 makes Option A is invalid.

> #transit gw  
* Transit Gateway doesn’t support routing between Amazon VPCs with overlapping CIDRs
* Transit Gateway is a regional service

> route#53 #dns

[Active-active and active-passive failover:](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover-types.html#:~:text=configure%20active-active%20and%20active-passive%20failover)

   * [Choosing a routing policy:](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html#:~:text=responds%20to%20queries%3A-,simple%20routing%20policy,-%E2%80%93%20Use%20for%20a)


> [VPC Connectivity Options - ET 548]  
    
* [ref:](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html#:~:text=a%20direct%20connect%20gateway%20is%20a%20globally%20available)  
* [ref:](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/55/#:~:text=we%20can%20associate%20a%20vpg%20with%20multiple%20dx.)



> #VPN even if it is redundant does not allow high bandwidth where it has a limit of 1.25Gbps. ET 404

* [ref:](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/41/#:~:text=it%20has%20a-,limit%20of%201.25gbps,-.%20https%3A%2F%2Faws.amazon)
* [ref:](https://aws.amazon.com/vpn/faqs/#:~:text=maximum%20throughput%20of%20up%20to%201.25%20gbps)
* [ref:](https://aws.amazon.com/vpn/faqs/#:~:text=aggregate%20throughput%20limit%20from%20aws%20to%20on-premises%20of%20up%20to%201.25%20gbps)

> #networking

[Transfer Acceleration over a fully available 1 Gbps can theoretically move around 10TB/Day.](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/55/#:~:text=1%20gbps%20%3D%20(1024%2F8)%20mbps%20%3D%20128%20mbps)

> VPC Connectivity Options #vpc #dc  

* [ET 548 + aws blog:](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html#:~:text=a%20direct%20connect%20gateway%20is%20a%20globally%20available)
    * [ET 548 + aws blog:](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/55/#:~:text=we%20can%20associate%20a%20vpg%20with%20multiple%20dx.) 



[ET 550 :](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/55/#:~:text=A%2C%20now-,amazon%20route%2053%20supports%20dnssec%20for%20domain%20registration%20as%20well%20as%20dnssec,-signing)
* [ET 550](https://aws.amazon.com/about-aws/whats-new/2020/12/announcing-amazon-route-53-support-dnssec/#:~:text=you%20can%20now%20enable%20dnssec%20signing)

   * Amazon’s domain name registrar, Route 53 Domains, already supports DNSSEC. 
        * Customers can now register domains and host their DNS on Route 53 with DNSSEC signing enabled
             * You can now enable DNSSEC signing for all existing and new public hosted zones, 
          * When you enable DNSSEC signing on a hosted zone, Route 53 cryptographically signs each record in that hosted zone.
          * Amazon Route 53 DNSSEC provides data origin authentication and data integrity verification for DNS.
     * When you enable DNSSEC validation on the Route 53 Resolver in your VPC, it ensures that DNS responses have not been tampered with in transit.