Event Sourcing
A little history of ideas and a lightly annotated bibliography



From Kleppmann, of course
What is Event Sourcing? 
An architectural pattern in which changes in an application state are stored as a sequence of events. Database entries are immutable facts about events. They are not overwritten or deleted.
Where did it come from? 
	Domain Driven Design (DDD)

“Domain-driven design consists of a set of patterns for building enterprise applications from the domain model out.” 

DDD comes from enterprise software development: complex data models, but smaller datasets than internet companies.
What problem does it solve?
	Enterprise business needs with respect to data
Accurate auditing for business and financial institutions
Microservices integration: 
each service has its own db, which creates consistency problems
difficulty of querying across different dbs
Reliability and atomicity in db transactions
	
	Benefits:
No need to synchronize complex business domain with data model
New services/views can be built from the event log
Complete rebuild: application state can be completely rebuilt from event log
Temporal query: possible to determine the application state at any point, and possible to branch the system
Event replay: if buggy code is introduced or an incorrect event, application can “rewind” to previous state and “replay” with correct information to update current state
Accurate auditing
How is it different than Stream Processing?

Event sourcing comes out of enterprise software developers need to deal with complex business logic. It is primarily an approach to data storage that makes microservice architecture easier. 

Stream processing came out of a need to deal with streams of event data in internet companies like Facebook, Twitter, Google, LinkedIn. It is concerned with how best to analyze and store data streams. 
	Two typical ways to handle it:
 Save it all and query it later (good for analytics)
Keep only aggregated data and throw away events (good for alerts, trends, etc.)
Both: keep aggregated data, but save the events (have it both ways)
Take-aways
	
Kleppmann’s big idea is to combine event sourcing with stream processing, but the idea of saving events in some kind of log as a source of truth for an application has been around for longer.


There is another set of ideas and architectures related to event streams in addition to stream processing.

Stream query languages

Key terms to search: 
event sourcing


CQRS: the idea that the form of data most optimal for writes and the form of data most optimal for reads is not the same


Domain-Driven Design

Some other “Event-ish” ideas that may be helpful in thinking about event streams:

Distributed actor frameworks: less about data management, more a mechanism for programming concurrent systems


“Reactive”: the idea of bringing event streams to the front end 


Change Data Capture (CDC): using a ‘regular’ database, putting changes into a stream of events that other applications can consume


Complex Event Processing

Resources
	Stream Processing
	https://medium.com/stream-processing/what-is-stream-processing-1eadfca11b97
	
See more resources on the one-pager on stream processing
Event Sourcing
	https://martinfowler.com/eaaDev/EventSourcing.html
		Useful, non-product oriented discussion of event sourcing, including drawbacks. 

	https://martinfowler.com/eaaDev/EventNarrative.html
	
http://eventuate.io/whyeventsourcing.html
	
https://microservices.io/patterns/data/event-sourcing.html

https://eventuate.io/whyeventsourcing.html

https://docs.microsoft.com/en-us/azure/architecture/patterns/event-sourcing
	Very helpful discussion of benefits and challenges associated with event sourcing

https://dev.to/barryosull/event-sourcing-what-it-is-and-why-its-awesome

https://josephg.com/blog/api-for-changes/

https://softwareengineeringdaily.com/2016/10/14/kafka-event-sourcing-with-neha-narkhede/

CQRS 
https://martinfowler.com/bliki/CQRS.html

https://docs.microsoft.com/en-us/azure/architecture/patterns/cqrs

Domain Driven Design

http://www.methodsandtools.com/archive/archive.php?id=97
“Domain-driven design consists of a set of patterns for building enterprise applications from the domain model out.” 

https://www.amazon.com/gp/product/0321125215?ie=UTF8&tag=martinfowlerc-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0321125215
Eric Evans 2004 Domain-Driven Design: Tackling Complexity in the Heart of Software

https://cqrs.nu/Faq/domain-driven-design
	Vocabulary related to DDD in an easy to digest form
Comparison of Event Sourcing and Stream Processing
https://www.confluent.io/blog/event-sourcing-cqrs-stream-processing-apache-kafka-whats-connection/

https://www.confluent.io/blog/making-sense-of-stream-processing/

https://martin.kleppmann.com/2019/06/27/hydra-interview.html

https://www.oreilly.com/library/view/making-sense-of/9781492042563/ch01.html
	More Kleppmann Making Sense of Stream Processing 2016
	Book, download for free from O’Reilly

https://www.infoq.com/news/2016/05/event-sourcing-stream-processing/
	Summary of Kleppmann’s talk at DDD Europe, below
https://www.youtube.com/watch?v=avi-TZI9t2I
Martin Kleppmann at Domain Driven Design Europe conference 2016. He introduces the talk by talking about how he does not know anything about DDD. Compares Enterprise Software and why they use Event Sourcing with Internet Companies and why they use Stream Processing. Also goes into some depth about Samza and Kafka. List of references at the end of the talk.

Event Sourcing applied:
https://kickstarter.engineering/event-sourcing-made-simple-4a2625113224 
		Dibs on this idea
Ecosystem - Apache Kafka 
		Lots of ideas here
	https://blog.arkency.com/
		Lots of blog entries about event sourcing and rails
