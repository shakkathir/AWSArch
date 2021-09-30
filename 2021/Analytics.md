>#kinesis, firehose

_ref_: [ExamTopics Page Q698 Page 70](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/70/#:~:text=kinesis%20does%20not%20provide%20a%20native%20auto-scaling%20solution)
* Q: What is Amazon Kinesis Data Firehose?  
**Firehose automatically scales to match the throughput of your data** and requires no ongoing administration.

* **Unlike some other AWS services, Kinesis does not provide a native auto-scaling solution like DynamoDB On-Demand or EC2 Auto Scaling.** Therefore, there is a need for the right number of shards to be calculated for every stream based on the expected number of records and/or the size of the records. This can lead to over/under-provisioning of shards within a stream resulting in higher costs and/or data ingestion being throttled