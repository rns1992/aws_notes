# ELB

### What is full form of ELB?
- Elastic Load Balancer

### What are different types of Elastic Load Balancer?
- Application Load Balancer (HTTP and HTTPS)
- Network Load Balancer (TCP and high Performance)
- Classic Load Balancer (Legacy)
- Gateway Load Balancer

### What are 7 Layers of OSI model?
- It is a conceptual framework which describes the function of a network.
- Beginning with the applciation layer, which directly serves the end user, down to the physical layer.
- Layer 7 (Application Layer)
	- It is the layer which end users sees.
	- HTTP operates in this layer and webbrowser.
- Layer 6 (Presentational Layer)
	- It ensures that the data is in the usable format.
	- It operates on Encryption and SSH protocol.
- Layer 5 (Session Layer)
	- It is about maintaining connections and sessions.
- Layer 4 (Transport Layer)
	- It is about transmitting data using TCP and UDP. 
- Layer 3 (Network Layer)
	- It is responsible for routing packets based on IP addresses.
- Layer 2 (DataLink Layer)
	- It is responsible for physically transmitting data based on MAC adresses.
- Layer 1 (Physical Layer)
	- It is responsible for transmiting bits and bytes over physical devices like Cables and Hub.

### What is Applciation Load Balancer? 
- It is used for load balancing HTTP/HTTPS traffic. They operate at Layer 7 of OSI model and are application-aware.
- They support advanced request routing to specific web servers based on the HTTP header.

### Network Load Balancer
- Used to load balancing TCP traffic where extreme performance is required.
- Operates on Layer 4 (Transport Layer).
- It is capable ofhandling millions of requests per second while maintaining ultra-low latencies.
- As it provides high performance it is the most expensive option,

### Classic Load Balancer
- It is legacy option but may appear in the exam.
- It support Layer 7 specific features, such as *X-Forwarded-For* headers and sticky sessions.
- Support Layer 4 load balancing for applciations that rely purely on the TCP protocol.

### What is X-Forwarded-For-Header?
- This is HTTP header which helps identifying IP Address of a client connecting through a load balancer.

### What are common Load Balancer Errors?
- 504
	- It is most common error. It means that tagret application has failed to respond.

### Exam Tips
- Application Load Balancers
	- HTTP/HTTPS
	- Intelligent Load Balancing
	- Routes requests to a specific web server based on the type of request.
- Network Load Balancers
	- Provides high-performance load balancing for TCP traffic.
- Classic Load Balancers
	- The legacy option that supports both HTTP/HTTPS and TCP.
	- May still appear in the exam.
- Gateway load Balancers
	- Provides load balancing for third-party virtual aplications, like firewalls, Intrusion Detection and Preventions Systems
- X-Forwarded-For
	- If you need the IPv4 address of your end user, look for the X-Forwarded-For header.


### What does vertical scalability means in AWS?
- Vertical scalability means increasing the size of the instance.
- Vertical scalability is very common for non distributed systems, such as database.
- RDS, ElasticCache are services that can scale vertically.
- There's usually a limit to how much you can vertically scale (hardware limit).
- For eg. scaling from t2.micro to t2.large.

### What does horizontally scalability means in AWS?
- Horizontally scaling means increasing number of instances/system for your application
- Horizontally scaling implies distributed systems.
- This is very common for web applications/mordern applications.
- It's easy to horizontally scale thanks the cloud offerings such as Amazon EC2.

### What is high availability?
- High availablity means you are running your application/system in at least 2 data centers(== Availability Zones)
- The goal of High availability is to survice a data center loss.
- High availability can be passive (for RDS multi AZ for example)
- The high availability can be active (for horizontal scaling)

### What is activepassive and active-active type in high availability?
- Active-Passive
	- In an active-passive configuration, one node is active and other nodes are inactive and on standby. The backup server takes over if the active node is disconnected or unable to serve. The client machines connect to the main server, which handles the full workload. The backup server only activates in the event of a failure.
- Active-Active
	 - In an active-active configuration, all equivalent members are active and none are on standby. The multiple active nodes are simultaneously active and operational. If one node goes down, traffic intended for it is reassigned to another, online node.

### What is high Availability and scalability for EC2?
- Vertical Scaling: Increase instance size (= scale up/down)
	- from: t2.nano = 0.5 GB of Ram, 1 vCPU
	- to: u-12tbl.metal = 12.3 TB of RAM, 448 vCPUs
- Horizontal scaling: ncreate number of Instance (= scale out/in)
	- Auto Scaling Group
	- Load Balancer
- High Availability: Run instances for the same applciation accross multi AZ
	- Auto Scaling Group multi AZ
	- Load Balancer multi AZ

### What is Load balancing?
- Load Balancers are servers that forward traffic to multiple servers (eg. EC2 instances) downstream.

### Why use a load balancer?
- Spread load across multiple downstream instances.
- Expose a single point of excess(DNS) to your application.
- Seamlessly handle failures of downstream instances
- Do regular health checks to your instances
- Provide SSL terminations(HTTPS) for your websites.
- Enforce stickiness with cookies
- High availability across zones
- Seperate public traffic from private traffic

### Why use Elastic Load Balancer?
- An Elastic Load Balancer is a managed load balancer
	- AWS gurantees that it will be working
	- AWS takes care of upgrades, maintenance, high availability
	- AWS provides only a few configuration knobs to tweak the behavior  of load balancer.
- It costs less to setup our own load balancer but it will be a lot more effort on our end. Also it would be a nightmare to manage our own load balancer in point of scalability.
- It is integrated with many AWS offerings/services
	- EC2, ECS Auto Acaling Groups, Amazon ECS
	- AWS Certificate Manager (ACM), CLoudWatch
	- Route 53, AWS WAF, AWS Global Accelerator

### What are health checks in Load Balancer?
- They are a way to check is the instance is currently active or not.
- Health checks are crucial for Load Balancers.
- They enable the load balancer to know if instances it forwards traffic to are available to reply to requests.
- The health check is done ona port and a route (/health is common)
- If the response is not 200 OK, then the instance is unhealthy.

### How many tyoes of Load Balancers are there?
1) Classic Load Balancer (v1 - old generation) -2009 - `CLB`
	- Supports HTTP, HTTPs, TCP, SSL (secure TCP)
	- It is depricated and AWS does not wants us to use it but still available to use.
2) Application Load Balancer (v2 - new generation) - 2016 - `ALB`
	- It supports HTTP, HTTPs, WebSocket
	- Its new generation load balancer
3) Network Load Balancer (v2 - new generation) - 2017 - `NLB`
	-	It supports TCP, TLS (secure TCP), UDP
4) Gateway Load Balancer - 2020 - GWLB
	-	Operates at layer 3 (Network layer) - IP Protocol
- Overall it is recomended to use the newer generation load balancers as they provide more features.
- Some load balancers can be setup as *internal* (private) or *external* (public) ELBs for example websites or public applications.