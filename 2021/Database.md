
## Database 
_ref_ : <a href="https://aws.amazon.com/blogs/database/aws-database-migration-service-and-aws-schema-conversion-tool-now-support-ibm-db2-as-a-source/">AWS Database Migration Service and AWS Schema Conversion Tool now support IBM Db2 LUW as a source | AWS Database Blog</a>

Services like the [AWS Database Migration Service (AWS DMS)](https://aws.amazon.com/dms/) and the [AWS Schema Conversion Tool (AWS SCT)](https://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.GettingStarted.html) help with migrating commercial to open-source databases in AWS with minimal downtime

Migrations from commercial to open-source databases typically take multiple steps, but we discuss two important parts following:

*   Using AWS SCT to convert objects (tables, indexes, constraints, functions, and so on) from the source commercial engine to the open-source engine.
*   Using AWS DMS to move data into the appropriate converted objects and keep the target database in complete sync with the source. Doing this takes care of the production workload while the migration is ongoing.  

> #aurora serverless
*  Aurora Data API "enables the SQL HTTP endpoint, a connectionless Web Service API for running SQL queries against this database. When the SQL HTTP endpoint is enabled, you can also query your database from inside the RDS console (these features are free to use).