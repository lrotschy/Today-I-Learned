Notes on Error Handling Liela
Error Handling in Node.js
Linked by multer docs

Four main ways of handling errors in Node.js:
Throw the error, making it an exception
Pass the error to a callback function for error handling
Pass the error to a reject Promise function
Emit and ‘error’ event on an EventEmitter

An Error is any instance of the Error class. 
Errors may be constructed and then passed directly to another function or thrown 
When you throw an error it becomes an exception 
Code that throws an error as exception:  `throw new Error(‘something bad happened’)`
Code that handles the error without throwing it: `callback(new Error(‘something bad happened’));`
The second is more common because most errors are async. Catching an error from a sync function is more common in Java, C++, other langs that make heavy use of exceptions

Operational Errors vs. programmer errors 

Operational Errors: Runtime problems by correctly written programs, not bugs. Examples:
Failed to connect to server
Failed to resolve hostname
Invalid user input
Request timeout
Server returned 500 response
Socket hang-up
System out of memory

Programmer errors: bugs in program. Can never be handled properly because the code is the problem. Examples: 
Tried to read property of ‘undefined’
Called and async function without a callback
Passed a ‘string’ where an object was expected

This difference is key for understanding how to handle errors.
Operational errors are part of the normal operation of the program.
One problem can cause both types of errors.
Failure to handle operational error is programmer error. E.g. connection failure shouldn’t cause crash.

Handling operational errors
	Consider how code could fail and what failure would indicate
	Error handling at several levels of stack--error gets propagated to called

	Some things you can do:
Deal with it directly
Retry, create missing log file, etc.
Propagate failure to client 
Clean up, deliver error back to client if whatever caused error isn’t going to change soone (e.g. invalid json)
Retry operation 
Network and remote servicer errors 
Clearly document how many times you’ll retry, how long to wait before retrying 
Don’t assume you should always retry--if several layers are retrying, wait can be very long. Instead, let client retry 
Blow up 
If you can’t fix the problem or if it is a problem that represents a programmer error, crash and log an error 
Log the error and don’t do anything else 
A remote service falls out of DNS..? But everything still works. If is will be LOTS of error messages, don’t log them all 


(NOT) handling programmer errors 
Crash immediately and restart 
Continuing to run could cause havoc for various reasons, e.g. connections left open, authentication problem, memory references not cleaned up, db leak, etc.
Clients should be able to retry connections even if down for a sec to restart 
If program is down so much that it creates a problem, the code is too buggy anyway, so fix it already

  A thing I don’t understand, but seems important: 
Best way to debug crashes is to configure Node to dump core on an uncaught exception. You can use core files to see stack trace, and arguments etc. 
https://www.joyent.com/node-js/production/debug#postmortem

Remember that programmer error on server becomes operational error on client. Clients have to deal with servers crashing and network blips.

Patterns for writing functions

How to deliver errors to code that called your function 

Document what your function does, what arguments it takes, what it returns what errors can happen, what those errors mean.

If you don’t know what errors can happen or don’t know what they mean, then your program cannot be correct except by accident.

Three basic patterns for delivering errors: Throw, Callback, Reject, or EventEmitter?

Throw 
Delivers error synchronously, in the same context where function was called 
If caller or caller’s caller.. Used try/catch, they can catch error. 
Otherwise, usually crashes. 
Can also be caught by domain or process-wide “uncaughtException” event…?

Callback
Most basic way of delivering an error asynchronously 
Invoked when async operation completes
Usual pattern is to invoke cb(err, result) where only one of err and result is non-null 
How to use callbacks, see Node fs module: https://nodejs.org/api/fs.html

Promise rejections 
Common way to deliver error asynchronously 
Use async/await with try/catch

EventEmitters 
Complicated operations, complex state machines…. Read more some other time 

Most common in operational error handling is callback: How to use callbacks, see Node fs module: https://nodejs.org/api/fs.html

Next most common is synchronous functions like JSON.parse.
Throw it (most common)
Or return it 
For a given function, if an operational error can be delivered asynchronously, then all operational errors shoulc be delivered asynchronously 
Rule is: a function may deliver operational errors synchronously (e.g. by throwing) or asynchronously (with callback or emit error), but NOT both 
Either handle errors in callback or using try/catch, but not both
Which one to use depends on how function delivers its errors 

Programmer errors-always bugs 
Identify immediate by validating arguments at the start of the function 
Degenerate case is calling an async function but not passing callback 
Throw these errors immediately 



Bad input: programmer error or operational error?
If you get something other than what you’ve documented to accept, that’s a programmer error 
If you get something you’ve documented to accept but can’t process right now, that’s operational

Sometimes you can decide (e.g. IP address ‘bob’ can throw error not valid ip, or emit error ‘cou.d not connect’)
Usually better to be strict to minimize damage and debugging nightmares 

What about domains and process.on(‘uncaughtException’)?
Primarily useful to attempt to handle or recover from unanticipated programmer errors; strongly discouraged.

Specific recommendations for writing new functions (lots of detail here to return to)
Be clear about what your function does
Use Error objects for all errors
User Error’s name property to distinguish errors programmatically
Augment the Error object with properties that explain details 
If you pass a low level error to caller, consider wrapping it instead



