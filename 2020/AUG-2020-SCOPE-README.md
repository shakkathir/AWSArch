## Resource metering and throttling Feature: Scope of Work

### Last Updated : 2020/Aug/18

Work Item # | Work Item  | Component
------------ | -------------|-------------
1| Globally uniq trace id (GUTID) | Client App
2| Extract, instrument, augment | Server App - API GW
3| Message format Design & update life cycle  | Server App - Lambda based Data Extractor
4| Ship the extracted & instrumented message package  | Server App - Lambda Data Shipper
5| Centralized message aggregation   + loading | Server App - Data Store - DynamoDb
6| Reporting (Non-real time )  | Server App - Athena Table, Glue Crawler, S3 Datasets, Athena Query 
7| Dynamic API Throttling config  | Server App - DynamoDB Streams, Kinesis Data Streams + AWS Lambda Trigger



### On the client side 
#### Work Item #1: Globally uniq trace id (GUTID)
 - Establish of globally uniq trace id  with the **namespace tenenet.sub tenent**
 - Enable the client apps to embed the globally uniq trace id  in every client request

### On the server side 

#### Work Item #2 :  Extract, instrument, augment:
- for every __application account__ = 1..n  : do {
    - for every __application gateway or extraction point__ = 1..m  : do {
        - intercept every inbound API call from any client
          - extract the GUTID
          - timestamp it. 
          - cull relevant attributes from client request from the inbound message that are needed for metrics calculation by the downstream systems
          - package/create message payload containing 
            - GUTID
            - request attributes - app name, app id, tenet, sub tenent etc.,  
            - w/ timestamp  
          in a standardized message format (JSON or plain text)
       - intercept every outbound API call from any client
           - extract the GUTID 
            - timestamp it. 
            - cull relevant attributes in client response from from the outbound message that are needed for metrics calculation by the downstream systems
            - package/create message payload containing 
              - GUTID, 
              - request attributes - app name, app id, tenet, sub tenent etc., , 
              - w/ timestamp 
            - in a standardized message format (JSON or plain text)    
  \*}
\*}
  
___
#### Work Item #3 :  Message format Design & update life cycle 
- Design the message format with the attributes, types and nested structures if needed.
- Version message format ( The format evolves over time  and backwards compatiblity )
- when the message format changes: do  {
  - update the message attributes, types 
  - Version the new format
  - Publish the message format to all down stream systems & components that consumes the message.
}            
___
#### Work Item #4 : Ship the extracted & instrumented message package 
for every application account = 1..n : do  {
  - for every every application gateway or extraction point = 1..m : do {
    - set up required cross account permissions between application account & metering account. 
    - establish a block non blocking channel between a) the application gateway or extraction point and b) centralized data aggregation component to the metering account
    - publish the payload through a non-blocking channel from the application gateway or extraction point to the metering account 
  \*}
\*}
___
#### Work Item #5 :  Centralized message aggregation   + loading      
- Create a DynamoDB datastore (a Key Value datastore)  to store inbound and outbound message payloads. 
- Develop message reader + data loader to read the payload from non-blocking channel and to load it into key value DynamoDB datastore. 
___
#### Work Item #6 : Reporting (Non-real time ) 
- Crawl usage data from in DynamoDB tables to S3 bucket using AWS Glue to create ETL code 
- Create Datasets in S3 by configure the scheduler to run Glue creaeted ETL code on the incremental data that is generated on daily basis
- Create a AWS Athena instance 
- Develop a Table Model in AWS Athena and point to the datasets created in step 3 
- Develop Athena queries to calculate dollar metrics of API usage by tenet/sub tenent by combining the information from Cost Allocation Tool
___        
#### Work Item #7 : Real time API usage Throttling
- Enable DynamoDb datastreams that stores inbound and outbound message payloads. . 
- Process the Dyanamo Db stream records using a stream processing implementation to calculate per tenet/sub tenet Throttling thresholds metrics.
  - Stream Processing Implementation options
    - Kinesis Data Streams 
    - Dynamo DB streams + AWS Triggers.
    - Invoke API Gateway API to Update the API Throttling limits on a dynamic basis based on the tenet/sub tenet Throttling thresholds metrics calcuated by the stream processing implementation.
___
