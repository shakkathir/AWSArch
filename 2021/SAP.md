### SAP - 2021 
<span style="color:blue; font-family:Georgia; text-align:center; font-size:2em;">White Papers</span>
1. [Load Balancer](https://d1.awsstatic.com/whitepapers/architecture-considerations-for-migrating-load-balancers-to-aws.pdf)
2. Networking
3. Deployment
<p>  
<p>  

> __SAP__ Areas of questioning

Element #1|Element #2|Element #3|Element #4|Element #5
------------|------------|------------|------------|------------|
1.IAM: Internal and External( Fed Identities)|6.Storage| 11.Deployment:Virtual HW & Lifecycle| 16. Migration - SMS,DMS
2.IAM: Access Limits/Controls -IAM, SCP, BP |7.Database|12.Deployment:Virtual SW & Lifecycle|17.Esimation and Cost Management|#5|
3.Networking|8.Analytics|13.Deployment:Application & Lifecycle|Disaster Recovery |#5|
4.Compute #1:EC2+AMI+ASS |9.App Integration SQS, Kinesis|14.All 3 Layers Logging & Monitoring|#4|#5|
5.Compute #2:ECS, Lambda|10.Caching & CloudFront-CDN|15.Security|#4|#5|
#1|#2|#3|#4|#5|
___

> __WAF__ - Well Architected Framework  

#1|#2
--|--|
__HAS__| **H**igh Avail. & **S**caling|
**HAD**| **H**igh Avail. & **D**urability|
**LaC**| **L**ow **L**atency and Low **C**ost|
**RR**| **R**eliability and **R**esiliency
**OPS** | **O**perations (Efficient and/or less overhead), **P**erformance (high) and **S**ecurity




  * >__PTSD Environments__ (Prod, Testing, Staging and Dev)

    * >__WACD Layering__ ( Web, App  Data Caching Database)


Element #1|Element #2|Element #3|Element #4|
------------|------------|------------|------------|
Production| Staging | Testing| Development
Web Layer|#2|#3|#4|
App Layer|#2|#3|#4|
DB Cache Layer|#2|#3|#4|
Database Layer|#2|#3|#4|
#1|#2|#3|#4|

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
## Storage 
> #ebs  
> Neal  Storage Section - Q3  2021-09-18 13:04:28  
* The volume should be configured with 1-TB as gp2 volumes provide *3 IOPS per GB, 3000 IOPS / TB* which will allow the full 3,000 IOPS to be achieved.  
* This HDD volume type supports a maximum of 500 IOPS per volume.  

> #ebs Between a minimum of 100 IOPS (at 33.33 GiB and below) and a maximum of 16,000 IOPS (at 5,334 GiB and above), baseline performance scales linearly at 3 IOPS per GiB of volume size. AWS designs gp2 volumes to deliver their provisioned performance 99% of the time. A gp2 volume can range in size from 1 GiB to 16 TiB.  [aws link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)
* EFS will be much more expensive than using a gp2 volume
___
> #s3 #s3-acls #s3-public-access  
> Neal Storage Section Q4 2021-09-18 15:10:56  

### [stackoverflow example for full understanding](https://stackoverflow.com/questions/64303953/what-does-these-settings-mean-for-block-public-access-settings-in-s3#:~:text=for%20example%2C%20aws%20s3%20api%20has%20a%20call%20such%20as%20put-object%20have%20option%20--acl.%20with%20this%20you%20can%20not%20only%20upload%20object%2C%20but%20also%20make%20it%20publicly)


I can see this can be confusing, however the below should help to illustrate the usage of these.

*   `BlockPublicAcls` - This prevents any **new** ACLs to be created or **existing** ACLs being modified which enable public access to the object. With this alone existing ACLs will not be affected.
*   `IgnorePublicAcls` - Any ACLs actions that exist with public access will be ignored, this does not prevent them being created but prevents their effects.
*   `BlockPublicPolicy` - This prevents a bucket policy containing public actions from being created or modified on an S3 bucket, the bucket itself will still allow the existing policy.
*   `RestrictPublicBuckets` - This will prevent non AWS services or authorized users (such as an IAM user or role) from being able to publicly access objects in the bucket.

<ul>


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

> How does BlockPublicPolicy and RestrictPublicBuckets work differently?

Similarly, you can use [put-bucket-policy](https://docs.aws.amazon.com/cli/latest/reference/s3api/put-bucket-policy.html) to apply public bucket policies, e.g.:

```
{
   "Statement": [
      {
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::MyBucket/*"
      }
   ]
}

```

with

```
aws s3api put-bucket-policy --bucket MyBucket --policy file://policy.json 
```

Now, if you enable:

*   `BlockPublicPolicy` the above **API will fail**, because the policy allows for public API.

*   `RestrictPublicBuckets` the above **API will succeed**, and the bucket policy will be applied. However, the policy will be **ignored**, and objects will be private. Disabling `RestrictPublicBuckets` will make the policy to work, and the objects will be publicly available.
</ul>

### [4 settings to block public access](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html#:~:text=settings-,s3%20block%20public%20access%20provides%20four%20settings,-.)

### [S3 predefined groups](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#:~:text=amazon%20s3%20predefined%20groups)  

### [canned acl](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#:~:text=amazon%20s3%20supports%20a%20set%20of%20predefined%20grants%2C)

* [put-object — AWS CLI 1.20.44 Command Reference](https://docs.aws.amazon.com/cli/latest/reference/s3api/put-object.html)
<ul>

*\--acl* *(string)*

> *The canned ACL to apply to the object. For more information, see* [*Canned ACL*](https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#CannedACL) *.*
>
> *This action is not supported by Amazon S3 on Outposts.*
>

> *Possible values:*
>
> *   *private*
> *   *public-read*
> *   *public-read-write*JJ
> *   *authenticated-read*
> *   *aws-exec-read*
> *   *bucket-owner-read*
> *   *bucket-owner-full-control*
</ul>
 
 
> #s3
  1. The maximum object size in S3 is 5TB  
  2. For Amazon S3 you can enable cross-Region replication which requires versioning is enabled. This provides synchronization of changes and also versioning history in case of data corruption. 

> #kds
  1. You cannot store records in a Kinesis data stream for 90 days, the maximum is 7 days  

> #dynamodb
   1. DynamoDB continuous backups can be enabled. This provides per-second granularity and restore to any single second from the time PITR was enabled up to the prior 35 days. This protects against data corruption  
   2. Adaptive capacity is enabled automatically for every DynamoDB table, at no additional cost. You don’t need to explicitly enable or disable it.

> #ebs
1. You cannot create snapshots of an instance in one Region directly into another Region as the wording suggests. You must create the snapshot in the same Region and then copy it across Regions

> #efs
1. There’s no such thing as EFS cross-Region replication so the shared files cannot be synchronized that way.
2. [AWS DataSync](https://aws.amazon.com/datasync/) makes it easy for customers to replicate data from one Amazon EFS file system to another without traversing a public network. [AWS Blog link](https://aws.amazon.com/blogs/storage/transferring-file-data-across-aws-regions-and-accounts-using-aws-datasync/)
____


## Database 
_ref_ : <a href="https://aws.amazon.com/blogs/database/aws-database-migration-service-and-aws-schema-conversion-tool-now-support-ibm-db2-as-a-source/">AWS Database Migration Service and AWS Schema Conversion Tool now support IBM Db2 LUW as a source | AWS Database Blog</a>

Services like the [AWS Database Migration Service (AWS DMS)](https://aws.amazon.com/dms/) and the [AWS Schema Conversion Tool (AWS SCT)](https://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.GettingStarted.html) help with migrating commercial to open-source databases in AWS with minimal downtime

Migrations from commercial to open-source databases typically take multiple steps, but we discuss two important parts following:

*   Using AWS SCT to convert objects (tables, indexes, constraints, functions, and so on) from the source commercial engine to the open-source engine.
*   Using AWS DMS to move data into the appropriate converted objects and keep the target database in complete sync with the source. Doing this takes care of the production workload while the migration is ongoing.  

___
## Migration  
 _ref_: [Neal Davis](https://digitalcloud.training/certification-training/aws-certified-solutions-architect-professional/aws-migration-transfer/#:~:text=aws%20migration%20hub%20provides%20a%20single%20location%20to%20track%20the%20progress)
* SMS
* DMS + SCT
* App Discovery
* Migration Hub   

__Data Migration Tools__  
  * Snow Ball, Snow Cone, Snow Mobile
  * Data Sync
  * Data Transfer Family (sFTP, FTPS)  

## Costing
_ref_: [Neal Davis](https://digitalcloud.training/certification-training/aws-certified-solutions-architect-professional/aws-cost-management/#:~:text=Management-,aws%20cost%20management,-AWS)  

__AWS Budgets,__  
__AWS Cost Explorer,  and   
AWS Cost and Usage Report (CUR)__ 
<p>  

* __AWS Budgets__ to track your service costs and usage  
  * AWS Budgets helps Monitoring EC2 reserved instance (RI) usage  
  * AWS Budgets allows customers to monitor how much of their Amazon EC2 instance usage is covered by reservations and to receive alerts when coverage falls below a specified threshold  
<p>

*  __AWS Cost Explorer__ has an easy-to-use interface that lets you visualize, understand, and manage your AWS costs and usage over time.

<p>

* *The __AWS Cost & Usage Report__ itemizes usage at the account or Organization level by product code, usage type and operation*

  * These costs can be further organized by enabling 
    * __Cost Allocation tags__ and 
    *  __Cost Categories__
<p>

* __Cost allocation tags__ to organize your resource costs on your cost allocation report, to make it easier for you to categorize and track your AWS costs

* __You can create custom categories__ and map your cost and usage information into these categories based on the rules defined by you using various dimensions such as account, tag, service, charge type, and even other cost categories

# Caching
