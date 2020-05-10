Stream Processing 
What is the problem? 
Data that is generated at a very high volume as a continuous stream of events or from multiple continuous streams of events. Typically, this data is used to track patterns over time or monitor a system
Examples: 
Financial services, sensor data, log entries, user events in an application, geospatial data, telemetry from devices or instruments, social networks, ecommerce activity…
This kind of data often needs to be processed immediately, as its value decreases over time 
Generally, no need to update or delete any given data point--may need to delete or archive batches of older data
Relational Database Management Systems (RDBMSs) were not designed to efficiently process this type of data
What are the solutions? 
Batch processing
Basic idea: store the data, stop data collection, process the data in a batch
Challenges:
Aggregation over batches is problematic for pattern detection 
Storage limitations
Higher latencies
Benefits 
Good for processing bounded data, i.e. data that has a fixed size, not continuous
Jobs can be scheduled to run periodically
Stream processing 
Basic idea: process data as it is produced, either as individual data points or in sliding windows 
Challenges
Not good for data that needs to be randomly accessed or passed through multiple times for processing
Benefits
Processing is spread over time
Do not need to store all data--preserve only useful parts
Good for situations where processing can be done in a single pass or only needs to access most recent data
Sliding windows facilitate pattern detection
Very low latencies 
Hybrid
Basic idea: stream processing initially, plus storage and retrieval for batch processing
Batch processing vs. Stream processing
				Batch Processing				Stream Processing
Data scope
Queries or processing over all or most of the data in a dataset
Queries or processing over data within a rolling time window, or on just the most recent data record
Data size
Large batches of data
Individual records or micro batches consisting of a few records
Performance
Latencies in minutes to hours
Requires latency in the order of seconds or milliseconds
Analyses
Complex analytics
Simple response functions, aggregates, and rolling metrics
From https://aws.amazon.com/streaming-data/
Tools for stream processing
Stream processing frameworks 
Lots of Apache frameworks and tools
Amazon has several options 
Time series databases: See the write-up in Basecamp
Streaming SQL:  See Part II of Streaming Data, coming soon…
Message brokers: Rabbit MQ, Apache Kafka, Amazon MQ...
Working with Streaming Data
Typically involves two layers: a storage layer for the raw data and a processing layer that consumes data from storage, processes it, and directs the storage layer to delete or archive older data

In the processing layer:
Simple model:
Connect processing to the event source and process each event one by one
Slightly less simple model:
Events stream into message broker and are assigned to a topic. Workers receive and process events from the topic and then publish results back to the broker.
Actor model (Apache):
Actors or agents accept an event and produce another event
Event stream processing frameworks let you write code for each actor, wire the actors up and hook the edge to the data sources. Events are sent directly to the stream processor or via a broker.
An event stream processor collects data, delivers it to each actor, makes sure they run in the right order, collects results, scales automatically, and handles failures.

Resources
Stream Processing 101: From SQL to Streaming SQL in 10 Minutes
	Discussion of streaming SQL
A Gentle Introduction to Stream Processing - Stream Processing
Questions 
“Furthermore, stream processing also enables approximate query processing via systematic load shedding.” 
Chronos: An event-capturing framework
	Capstone project
Understanding Your Options for Stream Processing Frameworks
Discusses “some of the most popular open-source stream processing frameworks” (all of them Apache) with some indications of the problems they were designed to solve.
What is Streaming Data? – Amazon Web Services (AWS) 
	Discussion of use cases for streaming data, comparison of batch processing and stream processing
