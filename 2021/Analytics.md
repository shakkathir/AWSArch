>#kinesis, firehose

_ref_: [ExamTopics Page Q698 Page 70](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-professional/view/70/#:~:text=kinesis%20does%20not%20provide%20a%20native%20auto-scaling%20solution)
* Q: What is Amazon Kinesis Data Firehose?  
**Firehose automatically scales to match the throughput of your data** and requires no ongoing administration.

* **Unlike some other AWS services, Kinesis does not provide a native auto-scaling solution like DynamoDB On-Demand or EC2 Auto Scaling.** Therefore, there is a need for the right number of shards to be calculated for every stream based on the expected number of records and/or the size of the records. This can lead to over/under-provisioning of shards within a stream resulting in higher costs and/or data ingestion being throttled.

> #kinesis  
 * [What are the limits of Amazon Kinesis Data Streams](https://aws.amazon.com/kinesis/data-streams/faqs/#:~:text=limits%20of%20amazon%20kinesis%20data%20streams )
 * [Auto scaling Amazon Kinesis Data Streams](https://aws.amazon.com/blogs/big-data/auto-scaling-amazon-kinesis-data-streams-using-amazon-cloudwatch-and-aws-lambda/#:~:text=auto%20scaling%20amazon%20kinesis%20data%20streams)
   * [What is Application Auto Scaling](https://docs.aws.amazon.com/autoscaling/application/userguide/what-is-application-auto-scaling.html#:~:text=who%20need%20a%20solution%20for%20automatically%20scaling%20their%20scalable%20resources%20for%20individual%20aws%20services%20beyond%20amazon%20ec2)
   * [Scale Amazon Kinesis Data Streams with AWS Application Auto Scaling](https://aws.amazon.com/blogs/big-data/scaling-amazon-kinesis-data-streams-with-aws-application-auto-scaling/#:~:text=scale%20amazon%20kinesis%20data%20streams%20with%20aws%20application%20auto%20scaling)