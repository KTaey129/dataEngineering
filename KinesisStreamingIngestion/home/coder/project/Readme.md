Kinesis Streaming Ingestion Project
Welcome to the Kinesis Streaming Ingestion project! This repository demonstrates how to build a streaming data ingestion pipeline using Amazon Kinesis. The main goal is to provide a practical, end-to-end example of capturing and processing real-time data streams.

Table of Contents
Introduction

Architecture Overview

Project Structure

Setup & Installation

Configuration

Usage

Data Flow

Monitoring & Logging

Future Improvements

Contributing

License

Introduction
This project showcases how to ingest and process streaming data using AWS Kinesis. It includes the following components:

Data Producers: Simulated or real-time data sources pushing data into a Kinesis Data Stream.

Kinesis Data Stream: A highly scalable channel for streaming data ingestion.

Consumer Application: Consumes data from Kinesis, processes it (e.g., filtering, transformation), and then forwards it to a destination (database, data lake, etc.).

With this setup, you can handle continuous, real-time data flows and build analytics/insights on top of them.

Architecture Overview
Below is a conceptual diagram of the pipeline:


+------------------+        +----------------------+         +--------------------+
|   Data Producer  |  -->   | Kinesis Data Stream  |  -->    | Consumer Application|
| (IoT, logs, etc.)|        | (Shards, Streams)    |         |  (Processing Script)|
+------------------+        +---------+------------+         +---------+----------+
                                      |                              |
                                      |------------------------------|
                                                (Real-time Processing)
Data Producer: Sends data records to Amazon Kinesis.

Kinesis Stream: Collects and stores data for short-term processing.

Consumer (Processing): Reads from the stream, transforms data, and stores it in a target system.

Project Structure

KinesisStreamingIngestion/
└── home/
    └── coder/
        └── project/
            ├── README.md             <- You are here!
            ├── requirements.txt      <- Python dependencies
            ├── config/               <- Configuration files (AWS credentials, environment variables)
            ├── producer/             <- Scripts or apps simulating the data producer
            │    └── data_producer.py
            ├── consumer/             <- Scripts or apps consuming and processing data
            │    └── data_consumer.py
            └── logs/                 <- Log files generated during runtime
producer/data_producer.py: Simulates or reads from a source and pushes data to Kinesis.

consumer/data_consumer.py: Consumes records from Kinesis, applies transformations, and writes data to a target (database, file, etc.).

Setup & Installation
Clone the Repository:


git clone https://github.com/KTaey129/dataEngineering.git
cd dataEngineering/KinesisStreamingIngestion/home/coder/project
Create & Activate a Virtual Environment (optional but recommended):


# For macOS / Linux
python3 -m venv venv
source venv/bin/activate

# For Windows
python -m venv venv
venv\Scripts\activate
Install Dependencies:


pip install -r requirements.txt
AWS Account Setup:

You must have an AWS account with the correct permissions to create and interact with Kinesis streams.

Install and configure the AWS CLI with your credentials:


aws configure
Configuration
Kinesis Stream:

Create a Kinesis Data Stream (e.g., my-data-stream) using the AWS Console or CLI.

Make sure your AWS credentials and permissions are set up so your producer and consumer can access this stream.

Environment Variables / Config Files:

You can store your AWS credentials (Access Key, Secret Key, Region) in:

~/.aws/credentials, or

.env file, or

config/credentials.json (not recommended for production).

Update your stream name and region in a config file or environment variable (e.g., KINESIS_STREAM_NAME=my-data-stream).

IAM Permissions:

Both the producer and consumer require IAM policies that allow kinesis:PutRecord and kinesis:GetRecords/kinesis:GetShardIterator.

Usage
1. Data Producer
Update producer/data_producer.py with your Kinesis Stream name and AWS region.

Run the producer to push messages into the stream:


python producer/data_producer.py
This script may randomly generate or source data records, then send them to the configured Kinesis stream in near real-time.

2. Data Consumer
Update consumer/data_consumer.py with the same Kinesis Stream name and AWS region.

Run the consumer to start reading and processing data:


python consumer/data_consumer.py
The script listens to the stream, retrieves records, and performs transformations (e.g., parsing JSON, filtering, cleaning).

Results can be logged, pushed to a database, or stored in CSV/Parquet files locally (configure as you see fit).

Data Flow
Producer: Sends continuous data records to my-data-stream.

Kinesis: Stores these records in shards.

Consumer: Reads from shards, processes records, and writes to a target.

You can monitor throughput, shard usage, and record counts via the AWS Console or AWS CLI.

Monitoring & Logging
AWS CloudWatch: Monitor the Kinesis Data Stream’s metrics (PutRecord latency, GetRecords success, etc.).

Logs Directory: Both producer and consumer scripts can be configured to log events and errors to logs/.

Exception Handling: In case of failures, ensure that logs capture relevant error messages for troubleshooting.

Future Improvements
Auto-scaling: Configure dynamic shard scaling based on data volume.

Enhanced Consumer Processing: Use AWS Lambda or Kinesis Data Analytics for serverless processing.

Security: Implement encryption at rest (KMS) or in transit (HTTPS endpoints).

Orchestration: Integrate with workflow orchestration tools like Apache Airflow or AWS Step Functions.

Contributing
Contributions are welcome! To propose changes or improvements:

Fork this repository.

Create a new branch: git checkout -b feature/someFeature.

Commit your changes: git commit -m "Add someFeature".

Push to the branch: git push origin feature/someFeature.

Open a Pull Request describing your changes.

License
This project is licensed under the MIT License. You are free to use, modify, and distribute this software.
