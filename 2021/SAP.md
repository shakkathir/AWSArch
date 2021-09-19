### SAP - 2021 

### SAP 2021 | whitepaper | [Load Balancer](https://d1.awsstatic.com/whitepapers/architecture-considerations-for-migrating-load-balancers-to-aws.pdf)
## IAM - 1 ( Non Federated)
## IAM - 2 ( Federated)
## Compute

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

>[aws link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)Between a minimum of 100 IOPS (at 33.33 GiB and below) and a maximum of 16,000 IOPS (at 5,334 GiB and above), baseline performance scales linearly at 3 IOPS per GiB of volume size. AWS designs gp2 volumes to deliver their provisioned performance 99% of the time. A gp2 volume can range in size from 1 GiB to 16 TiB.  
* EFS will be much more expensive than using a gp2 volume
___
> #s3 #s3-acls #s3-public-access  
> Neal Storage Section Q4 2021-09-18 15:10:56  
* [4 settings to block public access](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html#:~:text=settings-,s3%20block%20public%20access%20provides%20four%20settings,-.)
* [stackoverflow example for full understanding](https://stackoverflow.com/questions/64303953/what-does-these-settings-mean-for-block-public-access-settings-in-s3#:~:text=for%20example%2C%20aws%20s3%20api%20has%20a%20call%20such%20as%20put-object%20have%20option%20--acl.%20with%20this%20you%20can%20not%20only%20upload%20object%2C%20but%20also%20make%20it%20publicly)
* [S3 predefined groups](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#:~:text=amazon%20s3%20predefined%20groups)
* [canned acl](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#:~:text=amazon%20s3%20supports%20a%20set%20of%20predefined%20grants%2C)

[put-object — AWS CLI 1.20.44 Command Reference](https://docs.aws.amazon.com/cli/latest/reference/s3api/put-object.html)
*\--acl* *(string)*

> *The canned ACL to apply to the object. For more information, see* [*Canned ACL*](https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#CannedACL) *.*
>
> *This action is not supported by Amazon S3 on Outposts.*
>
> *Possible values:*
>
> *   *private*
> *   *public-read*
> *   *public-read-write*
> *   *authenticated-read*
> *   *aws-exec-read*
> *   *bucket-owner-read*
> *   *bucket-owner-full-control*

[stackoverflow](https://stackoverflow.com/posts/64304415/timeline)

&nbsp;&nbsp;&nbsp;&nbsp;Show activity on this post.

<div style="padding-left: 30px;">
My text

> How does BlockPublicAcls and IgnorePublicAcls work differently?

*For example, AWS S3 api has a call such as* [*put-object*](https://docs.aws.amazon.com/cli/latest/reference/s3api/put-object.html) *have option* `*--acl*`*. With this you can not only upload object, but also make it publicly available.*

When `Block Public Access` is off, call

```
aws s3api put-object --bucket some-bucket --acl public-read --key test.file

```

successes, and `test.file` will be not only uploaded, but also publicly available.

Now, if you enable:

*   `BlockPublicAcls`: the above **API will fail**. Any API which allows `*--acl public-read*`will be rejected. So `test.file` won't be uploaded.
*   `IgnorePublicAcls`: **API call succeeds**. The file is uploaded, but option `*--acl public-read*`is **ignored** and the file is private.

> *How does BlockPublicPolicy and RestrictPublicBuckets work differently?*
</div>