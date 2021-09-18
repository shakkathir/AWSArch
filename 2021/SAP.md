### SAP - 2021 
* Braincert Exam 1 
  * [Review #1  Week of Mar 1 -5](http://htmlpreview.github.io/?BrainCert.Exam2.Attemp1.Review_Answers_(3_9_2021_11_56_47_PM).html) 
* Braincert Exam 2 
  * [Review #1  Week of Mar 8- 12](http://htmlpreview.github.io/?BrainCert.Exam2.Attemp1.Review_Answers_(3_9_2021_11_56_47_PM).html)

### SAP 2021 | whitepaper | [Load Balancer](https://d1.awsstatic.com/whitepapers/architecture-considerations-for-migrating-load-balancers-to-aws.pdf)
## Networking
> #alb, #global_accelerator
* Alternatively, when using ALBs, the underlying IP addresses of the compute nodes
    supporting the ALB are subject to change, for example, in response to scaling events.
    *Because an ALB is not supported by a static compute node, or static group of compute
    nodes, it does not support direct integration with Elastic IP addresses. Static IP
    addresses can still be provided to consumers of ALB-based applications via AWS
    Global Accelerator, a service that provides fixed entry points to your application* 

## Storage 
> #ebs 
> Neal  Storage Section - Q3  2021-09-18 13:04:28
* The volume should be configured with 1-TB as gp2 volumes provide *3 IOPS per GB, 3000 IOPS / TB* which will allow the full 3,000 IOPS to be achieved.  
* This HDD volume type supports a maximum of 500 IOPS per volume.  

[aws link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)
>Between a minimum of 100 IOPS (at 33.33 GiB and below) and a maximum of 16,000 IOPS (at 5,334 GiB and above), baseline performance scales linearly at 3 IOPS per GiB of volume size. AWS designs gp2 volumes to deliver their provisioned performance 99% of the time. A gp2 volume can range in size from 1 GiB to 16 TiB.  
* EFS will be much more expensive than using a gp2 volume
___
> #s3 #s3-acls #s3-public-access
> Neal Storage Section Q4 2021-09-18 15:10:56
* [stackoverflow example for full understanding](https://stackoverflow.com/questions/64303953/what-does-these-settings-mean-for-block-public-access-settings-in-s3#:~:text=for%20example%2C%20aws%20s3%20api%20has%20a%20call%20such%20as%20put-object%20have%20option%20--acl.%20with%20this%20you%20can%20not%20only%20upload%20object%2C%20but%20also%20make%20it%20publicly)
* [S3 predefined groups](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#:~:text=amazon%20s3%20predefined%20groups)
* [canned acl](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#:~:text=amazon%20s3%20supports%20a%20set%20of%20predefined%20grants%2C)
