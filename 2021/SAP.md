### SAP - 2021 
<span style="color:blue; font-family:Georgia; text-align:center; font-size:2em;">White Papers</span>
1. [Load Balancer](https://d1.awsstatic.com/whitepapers/architecture-considerations-for-migrating-load-balancers-to-aws.pdf)
2. Networking
3. Deployment
4. [VPC connectivity Options](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html)
<p>  
<p>  

> __SAP__ Areas of questioning

Element #1|Element #2|Element #3|Element #4|Element #5
------------|------------|------------|------------|------------|
1.IAM: Internal and External( Fed Identities)|6.Storage| 11.Deployment:Virtual HW & Lifecycle| 16. Migration - SMS,DMS
2.IAM: Access Limits/Controls -IAM, SCP, BP |7.Database|12.Deployment:Virtual SW & Lifecycle|17.Estimation and Cost Management|#5|
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
**LoLC**| **L**ow **L**atency and Low **C**ost|
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

## 1. IAM - 1 ( Local and External/Federated Identities - Users, Roles)
## 2. IAM - 2 (Access Control aka policy)
## 3. Networking 
* [Networking](NETWORKING.md)

## 4. Compute_EC2
* [Compute 1](Compute1_EC2.md)
## 5. Compute_Lambda 
* [Compute 2](Compute2_Lambda.md)

## 6. Storage
* [Storage](Storage.md)

## 7. Database
* [Database](Database.md)

## 8. Analytics
* [Analytics](Analytics.md)

## 9. Application Integration

## 10. Caching & CloudFront - CDN
* [Caching](Caching_CDN_CloudFront.md)

## 11.Migration
* [Migration](Migration.md)

## 12.Costing
* [Costing](Costing.md)
