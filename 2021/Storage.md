# Storage 
> #ebs  
> Neal  Storage Section - Q3  2021-09-18 13:04:28  
* The volume should be configured with 1-TB as gp2 volumes provide *3 IOPS per GB, 3000 IOPS / TB* which will allow the full 3,000 IOPS to be achieved.  
* This HDD volume type supports a maximum of 500 IOPS per volume.  

> #ebs   
* Between a minimum of 100 IOPS (at 33.33 GiB and below) and a maximum of 16,000 IOPS (at 5,334 GiB and above), baseline performance scales linearly at 3 IOPS per GiB of volume size. AWS designs gp2 volumes to deliver their provisioned performance 99% of the time. A gp2 volume can range in size from 1 GiB to 16 TiB.  [aws link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)
* EFS will be much more expensive than using a gp2 volume

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
*  **Authenticated Users group**   
    * Represented by `http://acs.amazonaws.com/groups/global/AuthenticatedUsers`.

    * This group represents all AWS accounts. **Access permission to this group allows any AWS account to access the resource.** However, all requests must be signed (authenticated).

    * When you grant access to the Authenticated Users group any AWS authenticated user in the world can access your resource.
* **All Users group** – Represented by `http://acs.amazonaws.com/groups/global/AllUsers`.

  * **Access permission to this group allows anyone in the world access to the resource.** The requests can be signed (authenticated) or unsigned (anonymous). Unsigned requests omit the Authentication header in the request.
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
> #s3 access points  
* If you use AWS Organizations, you can add a Service Control Policy (SCP) requiring all S3 access points are restricted to a VPC
* If you use AWS Organizations, you can add a Service Control Policy (SCP) requiring all S3 access points are restricted to a VPC
