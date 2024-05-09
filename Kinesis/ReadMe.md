# AWS Kinesis

## What is AWS Kinesis?

- AWS Kinesis is a suite of services provided by Amazon Web Services (AWS) that enables real-time processing of streaming data at scale.
- It makes easy to collect, process and analyze streaming data in real-time.
- Ingest real-time data such as: Application logs, Metrics, Website clickstreams, IOT telemetry data etc.

## How many components are there with AWS Kinesis?

1. **Amazon Kinesis Data Streams**
   - Amazon Kinesis Data Streams is the core service that enables you to build custom applications for processing and analyzing streaming data in real time. It allows you to ingest large amounts of data continuously and scale the processing capacity as needed by adding or removing shards.
   - It helps to capture, process and store data streams.
2. **Amazon Kinesis Data Firehose**
   - Amazon Kinesis Data Firehose is a fully managed service that simplifies the process of loading streaming data into AWS data stores and analytics services. 
   - It can automatically scale to handle varying data throughput and can deliver data to destinations such as Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk.
   - It helps to load data streams into AWS data stores.
3. **Amazon Kinesis Data Analytics**
   - Amazon Kinesis Data Analytics enables you to analyze streaming data using SQL queries without having to manage servers or infrastructure. It provides a simple way to perform real-time analytics on streaming data, allowing you to gain insights and take immediate actions based on the analysis.
   - It helps to analyze data streams with SQL or Apache Flink.
4. **Amazon Kinesis Video Streams**
   - Amazon Kinesis Video Streams is a service for ingesting, processing, and storing video streams for analytics and playback applications. It allows you to securely stream video from devices such as cameras and IoT devices to the cloud, where you can analyze the video data in real time or store it for later analysis.
   - It helps to capture, process and store video streams.

## What are four core services in Kinesis?

- **Kinesis Streams**
  - Stream data and video to allow you to build custom applications that process data in real time.
  - There ae 2 services
    1. Data Streams
    2. Video Streams
- **Kinesis Data Firehose**
  - **Capture**, **transform** and **load** data streams into AWS data stores to enable near real-time analytics with BI tools.
- **Kinesis Data Analytics**
  - Analyze, **query** and **transform** streamed data in real time using **standard SQL**. Store the results in an AWS data store.

## What is difference between Kinesis Streams, Fiehose and Analytics?

- Refer to diagram attached

## Explain Shards in Kinesis?

## Exam Tips on Kinesis Shards.

- The Kinesis Client Library running on your consumers creates a record processor for each shard that is being consumed by your instance.
- If you increase the number of shards, the KCL will add more record processors on your consumers.
- CPU utilization is what should drive the quantity of consumer instances you have, NOT the number of shards in your Kinesis stream.
- Use an Auto Scaling group, and base scaling decisions on CPU load on your consumers.