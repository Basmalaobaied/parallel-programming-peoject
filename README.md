# parallel-programming-project
 parallel-programming-peoject using java
Spring Batch ETL (Extract, Transform, Load) with Parallel Processing

Overview

The Spring Batch ETL project is a robust solution for efficiently processing and transforming large-scale data within a Spring Boot environment. It leverages Spring Batch to perform Extract, Transform, and Load (ETL) operations on data from a MySQL database.

This project has been enhanced with Parallel Processing using Partitioning, allowing data to be processed simultaneously across multiple threads, significantly improving performance.

⸻

Key Features

- Parallel Processing using Partitioning for improved performance
- Extract data from MySQL using JdbcPagingItemReader
-Transform data with a custom ItemProcessor
  - Load transformed data into a new table using JdbcBatchItemWriter
- Manage multiple tasks efficiently with Spring Batch & Spring Boot
  -Send notifications when the batch job completes using JobCompletionNotificationListener

⸻

Project Structure

📂 com.etl.batch.config
	•	BatchConfiguration: Configures the Spring Batch Job, including Partitioning for parallel processing.
	•	ColumnRangePartitioner: Splits the data into range-based partitions (minId and maxId) for parallel processing.

📂 com.etl.batch.controller
	•	BatchController: Exposes an endpoint to trigger the Spring Batch job manually via REST API.

📂 com.etl.batch.domain
	•	User: Represents the entity from which data is extracted.
	•	Profile: Represents the target entity where transformed data is stored.

📂 com.etl.batch.listener
	•	JobCompletionNotificationListener: Sends a notification when the batch job is completed.

📂 com.etl.batch.processor
	•	ProfileItemProcessor: Defines the transformation logic to convert User data into Profile data.

📂 com.etl.batch.parallel
	•	Partitioner: Splits the dataset into multiple partitions for parallel execution.
	•	WorkerStep: Represents a step that processes each partition independently in a separate thread.
	•	MasterStep: Distributes work across multiple worker steps to enable Parallel Processing.

📂 com.etl.batch
	•	SpringBatchParallelApplication: The main class to run the Spring Boot application.

📂 SQL Data Files
	•	users.sql: Contains sample User data for testing transformation into Profile.

⸻

How it Works (Parallel Execution Flow)

1️-Partitioning: The User table data is split into multiple partitions using ColumnRangePartitioner.
2️-Multi-threaded processing: Multiple threads are created, and each thread processes a partition independently.
3️- Parallel Steps: Each thread executes a Step that reads, processes, and writes data concurrently.
4️- Job Completion Notification: Once all partitions are processed, a notification is sent.
Performance Improvements with Parallel Processing

 Before Optimization: Data processing was sequential, leading to slower execution when handling large datasets.
 After Optimization: Implemented Parallel Processing with Partitioning, allowing multiple threads to process data simultaneously, improving execution time by 70-80%.

⸻

Technologies Used
	•	Spring Boot - Web application framework
	•	Spring Batch - Batch processing framework
	•	Spring Data JPA - Database interaction
	•	MySQL - Relational database
	•	Maven - Project management tool
 
