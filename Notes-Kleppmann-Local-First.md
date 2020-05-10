Local-First Software... Liela’s Notes

Motivation: Collaboration and Ownership

We depend on cloud apps--collaborative web applications--for both solo and collaborative work. But we don’t control the data that we create using these apps. If the service is unavailable, or the network is down, or if the service shuts down completely, our data is not available. In contrast, old fashioned apps that live in our local file system give us complete control over our own data. We would like the best of both worlds.

Seven ideals for local-first software
In local-first, the data on the local device is the primary copy, not the data in the remote server. They hold copies but only in order to assist with access.

2.1 No spinners: your work at your fingertips 
Because data is on local machine, it should be fast. No request-response latency
2.2 Your work is not trapped on one device 
You should be able to sync across devices easily
2.3 The network is optional 
	You should be able to work offline. Desirable to run as locally installed executable.
2.4 Seamless Collaboration with colleagues 
	Support real-time collaboration with both direct editing and suggestions.
2.5 The long now 
	Work should be accessible indefinitely. Use standard formats, stored locally.
2.6 Security and privacy by default 
Store your data. Remote storage should use end-to-end encryption.
2.7. You retain ultimate ownership and control

Existing Data Storing and Sharing Models 
3.1 How Application Architecture Affects User Experience 
3.1.1 Files and email attachments
Relatively fast, easy, secure, totally local-first storage. Not collaborative. Lesson and first step for apps that want to incorporate local-first is to offer export feature in common format that makes it easy to share.

3.1.2 Web apps: google docs, trello, figma, pinterest, etc. 
Thin client, data lives on server. Offer real time collaboration, but total loss of ownership and control. Little to no support for offline work. , though some hide server latency with JS and provide limited offline support. 

3.1.3 Dropbox, Google Drive, Box, OneDrive, etc.
Watch a designated folder on local file system and copied to all devices that share that folder. Fast, offline, local storage. Mobile versions do not work offline and do not have local storage. No real-time collaboration. Must be manually merged. 

3.1.4 Git and GitHub 
Local repo is primary copy of data. Not subordinate to remote data. Github enables collaboration, data access from multiple devices, backup and archive location. Weak mobile support. Two weaknesses: (1) No real-time collaboration, though great asynch collaboration. (2) optimized for code.

Note that software engineers don’t trust cloud storage.

3.2 Developer Infrastructure for Building Apps 
Typically data on server and web browser is thin client. 

Benefits: no installation, nothing for user to manage, data is stored and managed by professionals, users can access from all devices, colleagues can collaborate. 

Easy to add real time collaboration to web apps built on protocols such as WEbSocket (see sources here):
JS frameworks: Meteor, Share DB
Services: PUsher, Ably 

Drawbacks: slow due to latency, not very offline-friendly, data is not private, users have no control, data may be lost if website shuts down  
Efforts: manifests, localStorage, service workers Progressive Web Apps (check out sources) 
If user clears cookies, all data in local storage is also deleted 
	
	3.2.2 Mobile App with Local Storage (thick client) 
	Many apps are locally installed, but still thin clients with reliance on server 
	
	Others are locally installed, store data using persistence layer like SQLite, Core Data, or files (sources) 
	Fast, work offline, server sync happens in background, different degrees of privacy and control  
	Collaboration can be difficult, as mobile devs are usually not expert in distributed systems 

	3.2.3 Backend as a service: Firebase, CloudKit, Realm 

	Firebase is a local, on-device database combined with cloud database service and data sync 
Allows sharing of data across multiple devices
Supports offline use 
Low on privacy and longevity 
Good access to data for dev, but none for user 

	CloudKit is good for iOS and mac platforms. Similar to Firebase.
	Realm is another iOS platform. 
	
	“Mobile apps that treat the on-device data as the primary copy (or at least more than a disposable cache), and use sync services like Firebase or iCloud, get us a good bit of the way toward local-first software.”

***not clear if all this only applies to mobile


3.2.4 CouchDB
Pioneered multi-master replication approach. Each replican can write changes; any pair can sync to exchange write info. Couch DB is for use on servers; Pouch DB and Hoodie are designed to run on end-user devices (see sources) 

Allow concurrent changes; these lead to conflicts that need to be resolved in application code. Difficult for fine-grained collaboration like google docs. 

Reasons that CouchDB has not been widely adopted: 
Scalability when a separate db per user is required 
Difficulty embedding native js client in native apps on iOS and Android 
Conflict resolution problems 
Unfamiliar MapReduce model for queries 
And more ...
Implementation has not been able to realize local-first vision in practice 

***So is Couch DB for web apps or mobile apps?

Towards a Better Future 

4.1 CRDTs as a foundational technology
Family of distributed systems algorithms 
General purpose data structure, like hash map and list
Multi-user from ground up 
Every app needs data structure to store its state 
In single-user app, store this data in memory
...Or swap out for CRDT 

CRDTs can manage any concurrent changes except conflicting changes to same exact piece of data 
Can work with any communication channel 
Can work with single, atomic changes, or in batches 
See sources in this section 

Ink & Switch developed Automerge: open-source, JS CRDT implementation
Also Hypermerge: Automerge combined with Dat networking stack 

4.2 Ink & Switch Prototypes 
Try them. Read the code. 
Lessons learned: 
CRDTs work
Offline is good 
Works well with React (Functional Reactive Programming) 
Conflicts are not a significant problem
Possible to implement a time travel interface
URLS are a good mechanism for sharing--no access permissions set up at this point 
P2P system are never fully online or offline and it can be hard to reason about how data moves in them 
Different version of a document can lead to confusion 
How to manage versions?
CRDTS accumulate large change history, storage and performance problems 
How to handle data? Compression, age to live, central server sync…?
Network communication remains unsolved problem 
 In order to realize longevity, want apps to outlive backend services by vendors--decentralization 
P2P is mixed
Tried these:
WebRTC
‘Sneakernet’ implementation of copying files with dropbox and usb kes 
IPFS protocols
Settled on: 
Hypercore peer-to-peer libraries from Dat 
Cloud servers still have their place for discover, backup and burst compute 
Not central authorities but as ‘cloud peers’
“The key difference between traditional systems and local-first systems is not an absence of servers, but a change in their responsibilities: they are in a supporting role, not the source of truth.”

4.3 How can you help 
4.3.1 For Distributed Systems and Programming Languages Researchers 
4.3.2 For Human-Computer Interaction (HCI) Researchers 
4.3.3 For Practitioners 
Fast: aggressive caching 
Multi-device: sync infrastructure like Firebase, self-hosted infrastructure like Real Object Server 
Offline: PWAs…
Collaboration: OT, as in ShareDB 
Longevity: make sure software can easily export to standard data types 
Privacy: make clear to users where data is stored 
User control: make sure users can back up, duplicate, or delete their documents. Reimplement file structure as in google docs.
4.3.4 Call for Startups 
“Firebase for CRDTs” 
Great developer experience 
Local persistence library 
Available for mobile, desktop, web 
User control, privacy, multi-device support, collaboration 
Longevity 

	



4.3



	



	
