# ElastiCache

### What is ElastiCache?
- Its a In Memory Cache (Key Value)
	- Elastic Cache makes it easy to deploy, operate and scale an in memory cache in the cloud.
- Improves Database Performance
	- It allows you to retrieve information from fast, in-memory cache instead of slower disk based storage.
- Great for Read Heavy database Workloads
	- Caching the results of I/O intensive database queries. Also for storing session data for distributed applications.

### How many types of ElastCache is available?
1) **Memcached**
	- Great for basic object caching.
	- Scales horizontally, but there is no persistence, Multi-AZ or failover.
	- A good choice if we just want basic caching and our caching model needs to be as simple as possible.
2) **Redis**
	- A more sophisticated solution with enterprise features like persistence, replication, Multi-AZ and failover.
	- It supports sorting and ranking data (eg. for gaming leaderboards) and complex data types like lists and hashes.


### When ElastiCache can help?
- Database is under stress for read-heavy workloads.

### When ElasticCache can't help?
- Database is having write heavy workloads.
- If we are performing Online ANalytical Processing (use RedShift instead).


### ExamTips
1) MemCached
	- In Memory, key-value data store.
	- Object caching is your primary goal.
	- You want to keep things as simple as possible.
	- You don't need persistence or Multi-AZ.
	- You don't need to support advanced data types or sorting.
2) Redis
	- In-memory, key-value data store.
	- You are performing data sorting, ranking, such as gaming leaderboards.
	- You have advanced data types, such as lists and hashes
	- You need data persistence
	- You need Multi-AZ