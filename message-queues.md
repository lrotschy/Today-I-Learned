Message Queues 

What is the problem? 
With synchronously processed code, when a request is sent to another function, thread, or process, execution stops and waits for the job to complete. This causes your application to run slowly or stop if the request fails.

How do message queues solve the problem?

Message queues are a tool for asynchronous processing. Instead of waiting for a request to be fulfilled, the request is sent to a message queue for processing and execution continues. The message queue sends the job to the appropriate worker to be processed. While there is still some latency, it is less than with batch processing.

Basics of message queues 
	Message producers
Code that initiates processing by creating a message and sending it to a message broker or queue
	Queue
 		Can be implemented in a variety of ways:
A component backed by SQL database
Dedicated message broker 
Simple thread running in same application process
Independent application, i.e. message-oriented middleware
	Message brokers 
Also called Message-Oriented Middleware (MOM) or Enterprise Service Bus (ESB)
Specialized application that is responsible for message queueing, routing, and delivery 

	Message consumers 
Components that receive and process requests 
No dependency on producers, only need a valid message to fulfill request
Usually on a separate server 

	Messages 
Typically JSON or XML with all the data needed to fulfill the request

	Routing methods
Direct worker queue method: a single queue with (possibly) multiple producers and workers
Pub/sub
Consumers subscribe to topics
Producer publishes message to a topic, not a queue 
Broker receives messages and routes to queues for that topic
Custom

Benefits of message queues 
Enable asynchronous processing for synchronous platforms
Not that useful for platforms like Node.js that are already asynchronous ???
Scalability--can add multiple workers for costly processes
Load balancing 
Even out traffic spikes--message queues can back up without affecting front end user 
Decoupling allows for independent systems
Isolate failures
Producers do not depend on consumers so system can remain functional if consumer fails or stops for maintenance 
Multiple workers make system more resilient

Challenges associated with message queues
Race conditions: message workers are independent, so messaged can be fulfilled out of order 
Messages can be dropped if a worker fails
If a message is dropped and requeued, it could be fulfilled more than once	

Resources 
Web Scalability, chapter 7 
Designing Data Intensive Applications, pp. 440-451 
https://en.wikipedia.org/wiki/Message_queue
https://www.ibm.com/cloud/learn/message-queues
https://techblog.bozho.net/you-probably-dont-need-a-message-queue/
https://medium.com/omarelgabrys-blog/threads-vs-queues-a71e8dc30156
This is the article I wish I would have had when I wrote this paper!


** Side question: what are the relationships between event streams, message queues, background processing, and batch processing? 
	Event streams are a continuous data flow 
	Those events can be many things, including requests ?
	Message queues and batch processing are different ways of handling a stream of requests ?
	Background processing is….. Both??? And some other things as well?
