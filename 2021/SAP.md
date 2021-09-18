### SAP - 2021 
* Braincert Exam 1 
  * [Review #1  Week of Mar 1 -5](http://htmlpreview.github.io/?BrainCert.Exam2.Attemp1.Review_Answers_(3_9_2021_11_56_47_PM).html) 
* Braincert Exam 2 
  * [Review #1  Week of Mar 8- 12](http://htmlpreview.github.io/?BrainCert.Exam2.Attemp1.Review_Answers_(3_9_2021_11_56_47_PM).html)

### SAP 2021 | whitepaper | [Load Balancer](https://d1.awsstatic.com/whitepapers/architecture-considerations-for-migrating-load-balancers-to-aws.pdf)
## Static IP Addresses   
* Alternatively, when using ALBs, the underlying IP addresses of the compute nodes
    supporting the ALB are subject to change, for example, in response to scaling events.
    Because an ALB is not supported by a static compute node, or static group of compute
    nodes, it does not support direct integration with Elastic IP addresses. Static IP
    addresses can still be provided to consumers of ALB-based applications via AWS
    Global Accelerator, a service that provides fixed entry points to your application in single 
    Amazon Web Services Architecture Considerations for Migrating Load Balancers to AWS
    16 or multiple AWS regions

### Storage | Neal | Storage Section - Q3  2021-09-18 13:04:28
* The volume should be configured with 1-TB as gp2 volumes provide *3 IOPS per GB, 3000 IOPS / TB* which will allow the full 3,000 IOPS to be achieved.  
* This HDD volume type supports a maximum of 500 IOPS per volume.  
( https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html]
>>Between a minimum of 100 IOPS (at 33.33 GiB and below) and a maximum of 16,000 IOPS (at 5,334 GiB and above), baseline performance scales linearly at 3 IOPS per GiB of volume size. AWS designs gp2 volumes to deliver their provisioned performance 99% of the time. A gp2 volume can range in size from 1 GiB to 16 TiB.  
* EFS will be much more expensive than using a gp2 volume
