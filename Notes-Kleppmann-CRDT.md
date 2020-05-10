CRDT Distributed Consistency InfoQ Kleppmann Notes
https://www.infoq.com/presentations/crdt-distributed-consistency/

Algorithms for convergence:
1989 - 2006 Operational Transform (OT)
Many versions of this (12?) most failed, Google docs based on one of the successful ones
Problem is that they require a central server for convergence
Google docs, MS office online
2006 - present CRDT
Riak, TomTom GPS, Teletype for Atom Code Editor

Around 16:00
Consensus protocol = pick one of the proposed values (e.g. blockchain--only spend your money once)
Collaboration protocol = save all edits and merge (e.g. collaborative apps)

Around 18:00
Proving CRDTs Correct using Isabelle (theorem-proving software)
RGA - CRDT for text editor
OpSet - CRDT for sets
Counter- CRDT for counter

Satisfies strong eventual consistency (SEC)
SEC satisfied in all possible executions of faulty network model

Around 20:00
Automerge 
Built in JS, open source
Data model/data structure library with collaborative apps built on top of it
Abstraction that looks like JSON that can be modified and used to build apps on top of it
Implement without servers using P2P and Web RTC
Keeps track of changes with event log of changes
Does not have a networking layer
Just JS, json object as data structure
Can plug different network layers underneath, e.g. WebRTC, Hypercore/DAT, Hypermerge, MPL, WebSockets 

Around 25:00
Example application data (ordered list and map)
{ “to-do”: [
	{ “title”: “buy milk”,
	  “done” : false},
	{ “title”: “water plants”,
	  “done” : false},
	],
	“Settings”: {“alert-sound”: “ring”...}
}

Edit JSON values ….
Example JS code about state in Automerge (really similar to Redux… immutable state object)

state = Automerge.change(state, “Add todo item, ( ) => {
	doc.todos.push({
		Title: “buy milk”,
		Done: fale 
	)}
  )}

Arguments: state, optional commit message, callback--doc is mutable only within this block with proxy object
Automerge captures changes and stores in changes log as action

Operation log -- you never deal with this; it goes on internally
{action:”make Map”, obj: id1}
{action:”set”, obj: id1, key: “title”, value: “Buy milk”}
….

For now it keeps all changes forever (if git can do it, why can’t we?)
This allows time travel 

Automerge.getHistory(state) 
=> [{change: {message: “Add todo item”, …}, 
      Snapshot: {todos: [{title: “buy milk”.......}]}

Around 30:00
Concurrent Changes 
Immediately apply changes to local version 
When devices come online, automerge merges changes if they are compatible 

Convergence Guarantee: 
Any two nodes have seen the same set of operations (but maybe in a different order!) => They are in the same state
Only serious problem is when value of same field is set differently
Picks one arbitrarily but keeps other on inside object  in _conflicts 


{ “to-do”: [
	{ “title”: “buy milk”,
	  “done” : false,
_conflics: {title: {1234: “Buy almond milk”}}
},
	{ “title”: “water plants”,
	  “done” : false},
	],
	“Settings”: {“alert-sound”: “ring”...}
}

With text conflicts, keep both and put them in arbitrary order that is same on all nodes 
Hey guys! -> Hey folks!/Hey everyone! -> Hey folkseveryone!

Around 37:00?
Ordered Lists 
Insertions and deletions are determined relative to element ids, which are unique identifiers, not indexes
Insertions in the same place: skip over any existing list items with greater id so that insertions end up in same order 
Abc -> axybc/ apqbc -> apqxybc


