## DynamoDB Interview Questions.


1. **How do you scale the read and writes on Dynamo DB?**
	- We can use/switch to OnDemand capacity Mode.
	- **Provisioned mode**: If we are using Provisioned Mode, then we can set Auto Scaling Group to adjust the table's provisioned capacity automatically in response to traffic changes.
	- **Auto scaling groups**: Set up CloudWatch alarms to monitor key metrics such as CPU utilization, network traffic, and read/write throughput. When these metrics exceed a certain threshold, an auto scaling group can be triggered to add more capacity for DynamoDB.
	- **Sharding**: Split your table into multiple tables to distribute the data in your table across multiple partitions. This can improve performance and scalability
	- **Increase the number of partitions**: Each partition can handle up to 1000 Write Capacity Units and up to 3000 Read Capacity Units. When a partition reaches its limit, it is split into two and the items are redistributed.

2. **How do you enforce the higher reads and writes on DynamoDB?**
	- Enforcing higher reads and writes in Amazon DynamoDB involves adjusting provisioned capacity, optimizing your data model, and utilizing features like DynamoDB Accelerator (DAX) and Global Tables.
	- **Use autoscaling**:  Set up an autoscaling policy for the DynamoDB table to modify read/write capacity based on changing traffic.
	- **Use IAM policies**:  Restrict developers and services from doing expensive Scan operations on DynamoDB tables.
	- **Design data keys**: Distribute traffic uniformly across partitions by choosing partition keys wisely.
	- **Store hot and cold data in different tables**: Separate time series data into different tables, such as data for the last two years stored separately from data older than two years.
	- **Add a cache**: Point read traffic at a cache to alleviate the load from hot partitions in DynamoDB

3. **What is the use of indexing and how to sort data in DynamoDB?**
	- Indexing in Amazon DynamoDB serves two primary purposes: improving query performance and enabling alternative query patterns.
	- **TODO**

4. **What is DynamoDB Accelerator (DAX)**:
    -   DAX is an in-memory caching service that can significantly improve read performance for DynamoDB tables. By caching frequently accessed data, DAX reduces the need to read from the underlying DynamoDB table, resulting in lower latency and higher throughput for read operations.
    -   Integrate DAX with your DynamoDB application to enforce higher read throughput and reduce the load on your DynamoDB tables.

5. What is Partition Key and Sort Key?

6. Dynamo db vs no sql vs sql 

7. Indexes on different attributes

8. What are Indexes and types of index?

9.	Global secondary index in DynamoDB

10.	Local secondary index in Dynamo DB?

11. Explain DynamoDB Projections.

12. How do you query DynamoDB data based on keys that are not the primary key or sort key?

13. In DynamoDB, how will you copy data from one table to another table?

14. How do you decide which key should be used as GSI in dynamo DB?

 15. How can we implement encryption in DynamoDB table

16. Suppose you have a User table in DynamoDB , how will you choose GSI if you have to implement an API to fetch list of all first names
 