# Memory DB For Redis


### What is Memory DB for Redis?
- It is massively scalable from GB up to 100 TB.
- It is highly Available. It can be available in Multi AZ and has transaction logs for recovery and durability.
- It can be used as Primary Database instead of database + cache.
- It has Ultra Fast Performance. *It supports >160 million request per second. Microsecond read and single-digit millisecond write latency.*

### What is microsecond?
- It is one millionth of a second.

### What are suitable use cases for Redis?
- It is great for workloads requiring an ultra-fast, Redis compatible primary database.
- High Performance applications that needs an in-memory database to handle millions of request per second.
- Application that are data-intensive, low-latency and also requires high scalability.
- High scalable microservice based architectures.


### What is difference between ElastiCache for redis and MemoryDB for Redis?
1) **ElastiCache**
	- Its a database cache an in-memory database cache service. It sits in front of a database like RDS.
	- Its fast but not ultra-fast. It has millisecond read latency.
	- Its use case is a website that needs to store session data for its customers.
2) **MemoryDB**
	- It can be used as primary database by reducing complexity for a database + cache.
	- It has ultra fast performance in microsecond read and single millisecond write.
	- Its use case is of online gaming company with millions of users sharing digital assets.