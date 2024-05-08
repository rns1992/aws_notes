# EBS

### What is full form of EBS?
- Elastic Block Store

### What is use case of EBS volumes?
- It is storage volumes that you can attach to your EC2 instances.
- So they are storage volumes or like disks that we are attaching to our laptops or local computer.
- When we first launch our EC2 instance by default it commes with one attached EBS volume which contains our operating system data.
- We can add more volumes depending on the use of our applciation.
- **It is designed for production workloads**.
- **It is highly available**. It gets automaticaly replicated within a single Availability Zone to protect against hardware failures.
- **It is scalable**. It dynamically increase capacity and change the type volume with no downtime or performance impact to your live systems.


### What are different type of EBS volumes?
1. General Purpose SSD (gp2)
2. General Purpose SSD (gp3) (latest)
3. Provisioned IOPS SSD (io1)
4. Provisioned IOPS SSD (io2) (latest)
5. Provisioned IOPS SSD io2 Block Express
6. Throughput Optimized HDD (st1)
7. Cold HDD (sc1)
8. Magnetic

### What is General Purpose SSD (gp2) in EBS?
- It is a balance of price and performance.
- We can get 3 IOPS per GiB, i.e 3 input output operations per second per GB, up to max 16,000 I/O per volume.
- gp2 volumes smaller than 1 TB can burst up to 3000 IOPS.
- It is good for boot volumes or development and test applications which are not latency sensitive.

### What is General Purpose SSD (gp3) in EBS?
- It is latest generation of EBS.
- It has a capacity of 3000 IOPS for any volume size (1GB - 16TB).
- Delivering upto 16,000 IOPS
- It is 20% cheaper than gp2
- It is like gp2, they are good for boot volumes or development and test applications which are not latency sensitive.

### What is Provisioned IOPS SSD (io1) in EBS?
- It supports upto 64,000 IOPS per volume, 50 IOPS per Gib.
- In case if we need more than 16,000 IOPS then we need to upgrade to this.
- It is designed for I/O intensive applciations, large databases and latency-sensitive workloads.

### What is Provisional OPS SSD (io2) in EBS?
- It is latest generation.
- It has higher durability and more IOPS.
- It also supports same 64,000 IOPS as io1
- It is of same price as io1.
- We get 500 IOPS per GiB and max of up to 64,000 IOPS per volume.
- It is used for I/O intensive apps large database, and latency-sensitive workloads. Applications which need high levels of durability. 

### What is Provisional OPS SSD io2 Block Express in EBS?
- It is a SAN (Storage Area Network) in the cloud. It has highest performance, sub-millisecons latency.
- It uses EBS Block Express architecture.
- It has 4x throughput, IOS and capacity of regular io2 volumes.
- It supports up to 64 TB, 2,56,000 IOPS per volume.
- It has 99.999% durability.
- It is great for largest, most critical, high-performance aplciations like SAP HANA, Oracle, Microsoft SQL Server and IBM DB2.

### What is Throughput Optimized HDD (st1) in EBS?
- It is Low cost HDD volume.
- Its baseline throughput is of 40 MB/s per TB.
- It has the ability to burst upto 250 MB/s per TB.
- Maximum throughput of 500 MB/s per volume.
- It is used when data is frequently accessed, and has throughput-intensive workloads.
- It is used for Big Data, data warehouse, ETL and log precoessing.
- It is a cost effective way to store mountains of data.
- It cannot be a boot volume. AWS does not allow to select this as boot volume.

### What is COLD HDD (SC1) in EBS?
- It is Lowest Cost Option.
- Its baseline throughput is of 12 MB/s per TB.
- It has the ability tp burst upto 80 MB/s per TB.
- It has Max throughput of 250 MB/s per volume.
- It is not where near to st1 performance, but it is really good choice for colder data requiring fewer scans per day.
- It is good for the applications that need the lowest cost and performance is not a factor.
- If we require a job which runs at night and requires a lot of data but performance is not a problem then we can use this option.
- It also can not be a boot volume, AWS does not allows it.

### What is IOS Vs Throughput?

- `IOPS`
	- Measures the number of read and write per second.
	- Important metric for quick transactions, low latency apps and transactional workloads.
	- The ability to read and write very quickly
	- Choose Provisioned IOPS SSD (io1 or io2)
- `Throughput`
	- Measures the number of bits read or written per second (MB/s)
	- Important metric for large datasets, large I/O sizes, complex queries.
	- The ability to deal with large datasets.
	- Choose Throughout Optimized HDD (st1)

### How encryption works for EBS volume?
1. `Default Encryption`
	- If encryption by default is set on your account by your account admin, you cannot create unencrypted EBS volumes.
	- If your account is enabled for encryption by default, you can't create an unencrypted volume.
2. `Encrypted Snapshots`
	- If you can create an EBS volume from an encrypted snapshot, then you will get an encrypted volume.
	- If you selected an encrypted snapshot, you can't create an unencrypted volume.
3. `Unencrypted Snapshots`
	- If you create an EBS volume from an unencrypted snapshot, then encryption is only optional if default encryption has not been set at account level by your account admin. 
	- If your account is not enabled for encryption by default, and you did not select a snapshot or you selected an unencrypted snapshot, encryption is optional.

### What is snapshot in EBS?
- The snapshot from which to create the volume. When you create a new volume from a snapshot, it's an exact copy of the original volume at the time the snapshot was taken.
- EBS volumes that are created from encrypted snapshots are automatically encrypted. You can also encrypt the volume on-the-fly while restoring it from an unencrypted snapshot by selecting  **Encrypt this volume**. If you choose to encrypt the volume on-the-fly, you must choose the KMS key with which to encrypt the volume.
- Encrypted volumes can only be attached to instance types that support EBS encryption.

### What is throughput in EBS?
- The throughput performance that the volume can support. This is a performance measure in MiB/s. It is applicable to Throughput Optimized HDD (st1), Cold HDD (sc1), and General Purpose SSD (gp3) volumes only.
- Throughput Optimized HDD (st1) volumes have a baseline performance of 40 MiB/s per TiB, while Cold HDD (sc1) volumes have a baseline performance of 12 MiB/s per TiB.
- General Purpose SSD (gp3) volumes have a baseline performance of 125 MiB/s. You can provision additional throughput of 0.25 MiB/s per provisioned IOPS up to a maximum of 1,000 MiB/s (at 4,000 IOPS or higher).
- For General Purpose SSD (gp2) and Provisioned IOPS SSD (io1 and io2) volumes, performance is measured in IOPS.

### What is IOPS in EBS?
- The requested number of I/O operations per second that the volume can support. It is applicable to Provisioned IOPS SSD (io1) and General Purpose SSD (gp2 and gp3) volumes only.
- Provisioned IOPS SSD (io1) volumes support between 100 and 64,000 IOPS depending on the volume size. For io1 volumes, you can provision up to 50 IOPS per GiB.
- Provisioned IOPS SSD (io2) volumes support between 100 and 256,000, IOPS with an IOPS:GiB ratio of 1,000:1.
- For General Purpose SSD (gp2) volumes, baseline performance scales linearly at 3 IOPS per GiB from a minimum of 100 IOPS (at 33.33 GiB and below) to a maximum of 16,000 IOPS (at 5,334 GiB and above). General Purpose SSD (gp3) volumes support a baseline of 3,000 IOPS. Additionally, you can provision up to 500 IOPS per GiB up to a maximum of 16,000 IOPS.
- Magnetic (standard) volumes deliver approximately 100 IOPS on average, with a burst capability of up to hundreds of IOPS.
- For Throughput Optimized HDD (st1) and Cold HDD (sc1) volumes, performance is measured in throughput (MiB/s).



- https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html