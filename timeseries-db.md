Time Series Databases 

What problem do they address? 
	Handling large volumes of data that track patterns of change over time.

Some examples:
Sensor data -- the Internet of Things
App Analytics and DevOps metrics (e.g. event data--see Chronos)
Financial services 
Weather forecasting 

What are the key features of a time series database?
Time is the primary axis
Every record is a new entry 
Data is recorded in order
A single data point is not meaningful on its own; the pattern of data over time is what is meaningful
Often connected with a visualization engine
Generally append only; values are not updated or overwritten
Regular or irregular timestamps with values for a metric or metrics 
Optimized for querying time series data 
Functions for dealing with time series data
Can be SQL or NoSQL

Challenges 
Huge volumes of data (e.g. a Boeing 787 generates half a terabyte of data per flight, a single connected car will collect 4,000 GB of data per day)
Write-heavy 
Scaling and archiving

Trade-offs 
Higher volume of writes is more important than durability. The general pattern of data over time is more important than any single data point 

Examples of time series dbs 
MemSQL -- scalable SQL database
Timescale DB -- built on PostgreSQL
Prometheus -- open source, data stored as metric with labels
Amazon Timestream
CrateDB -- RDBMS
InfluxDB -- NoSQL
Kdb+
RRDtool
RiakTS -- NoSQL

Resources 
https://www.grin.com/document/299975 ???
https://www.beautifulcode.co/blog/49-introduction-to-working-with-timeseries-data
https://blog.timescale.com/blog/time-series-data-why-and-how-to-use-a-relational-database-instead-of-nosql-d0cd6975e87c/
https://severalnines.com/database-blog/introduction-time-series-databases
https://blog.timescale.com/blog/what-the-heck-is-time-series-data-and-why-do-i-need-a-time-series-database-dcf3b1b18563/
https://thenewstack.io/use-time-series-database/ 
https://www.memsql.com/blog/choosing-a-time-series-database/
https://fabxc.org/tsdb/

