AWS Amplify Notes
Features available in Amplify:
It seems that the whole AWS ecosystem is available.

Storage: S3 
DB: Dynamo, Aurora, apparently possible to use other dbs as well
Data Store: On-device queryable persistent data store that synchronizes data between app and cloud using GraphQl
Authentication: common ones are supported (Facebook, Google, …)
Provides IAM access to app and console: set permissions for who can access your app and what they can do with it
Analytics: drop in analytics to track sessions, attributes, in-ap metrics
API: REST and GraphQL
AR, VR
Predictions: ML, AI 
Interactions: create conversational interfaces using voice and text powered by deep learning, chat bots
Push notifications integrated with analytics 
PubSub: “Pass messages between your app instances and your backend creating real-time interactive experiences. Amplify provides connectivity with cloud-based message-oriented middleware using AWS IoT and Generic MQTT Over WebSocket Providers.”
Lambda
UI components?
Cache LRU
Logger console logging utility
Service Worker: A utility class to work with PWA and Service Worker APIs.
AWS App Synch realtime collaboration 
https://aws.amazon.com/appsync/resources/
https://aws.amazon.com/blogs/mobile/building-a-serverless-real-time-chat-application-with-aws-appsync/
https://news.ycombinator.com/item?id=16812284
AWS Device Farm dev tools (see your app on zillions of different devices)
PWA: https://aws.amazon.com/about-aws/whats-new/2018/05/aws-amplify-service-worker-capabilities/
Web sockets
Tutorials 
https://aws.amazon.com/getting-started/tutorials/deploy-react-app-cicd-amplify/?e=gs&p=gsrc&trk=gs_card
This one is very short. 
Steps:
Set up a React project
Create a GitHub repo for it
Create or log in to an AWS account 
Connect your GitHub repo to Amplify through the Amplify console 
Deploy your app
Make a change to your code and push it to GitHub
See your app re-deploy with the changes you made 
Delete your app (What???) 

Here is the finished app. Notice the extra exclamation marks that I added before redeploying (so exciting!!!): https://master.d2k4kktgv49s3z.amplifyapp.com/

Take away: Amplify accesses your code through GitHub or similar service (there are others to select from)
Does not include: installing the CLI, using the SDK.

In the deployment information there are four steps: 
Provision 
This text: “We are provisioning your build environment with a Docker image on a host with 4 vCPU, 7GB memory. Each build image gets its own host instance, ensuring all resources are isolated. The contents of our Dockerfile are displayed below for your information.” 
Plus code that looks like it is installing a whole Docker setup with the OS packages, Amplify CLI, node, ruby…. ?
Build 
	Two subheading with code: Cloning repository, FrontEnd 
I can guess what cloning repository means, but I don’t know what is going on in front end. Code is provided. I think it is Docker stuff.
Deploy 
	Code says uploading assets of various types
Verify
	Generates snapshots of how it looks on various devices

Another important take away: the console can be used as in the tutorial to host SPAs or static sites without using the Amplify Framework. If your site has no backend, you just use Amplify to host and deploy. (see the FAQ notes below)
You can also use the framework without using the CLI. 

So there are three pieces: 
The console: used to deploy an app from a GitHub repo or similar. 
The framework: used to interact with the backend.
The CLi: to help set up the framework


Questions:  
How is Docker connected and how does it work? Is all the code loaded into a Docker container and then deployed?
Amplify is 
GraphQL 
This keeps coming up. Amplify supports REST and GraphQL APIs. 

This introduction is good: https://www.freecodecamp.org/news/so-whats-this-graphql-thing-i-keep-hearing-about-baf4d36c20cf/
...even though the personal assistant illustration is incredibly sexist and makes me stabby.

https://medium.com/@paigen11/what-is-graphql-really-76c48e720202
This one is also very good

https://graphql.org/
This is the official site


GraphQL is a query language for APIs, not for endpoints. It looks like JSON. It allows you to query different data from different sources all at once, rather than sending multiple queries as you would have to do with a REST API. The data you query does not have to be in the same format as the request, but you do have to specify where to look for the data. Queries are organzied by types and fields, not endpoints.

AWS IAM 
This also keeps coming up. This is Identity and Access Management. It allows you to control access to AWS services and resources

Amplify Developer Guide
https://aws-amplify.github.io/docs
This has a more readable explanation of how to use different components of Amplify.

https://aws-amplify.github.io/docs/js/start


Amplify FAQ
Very useful--funny that they put these in the FAQ instead of front and center…? There is more here than what I copied below. Read more later. This is the high-level, but reasonably detailed overview I have been looking for.

Amplify Framework FAQ
https://aws.amazon.com/amplify/faqs/

What is it?
Amplify framework is open-source 
Provides: an opinionated set of libraries, UI components, CLI 
Integrates with iOS, Android, Web, React Native 
AWS Amplify Developer Tools services includes: Amplify console for building, deploying, and hosting and Device Farm for testing on real devices 

Components 
Amplify Framework
Cloud services such as AppSync and Amazon Cognito leveraged by Amplify framework
Amplify console
AWS Device Farm Dev Tools

Console and Framework
Can be used together or separately 
Console can host SPA and static websites 
Conolse provisions or updates backend resources provided by framework CLI

Cloud Services
When you configure features using CLI, AWS cloud services are provisioned for you
Config is persisted in CloudFormation templates that can be checked into source control and shared with other developers (?)
Amplify library makes calls to AWS features (e.g. ‘amplify add analytics’ configures Pinpoint)



Amplify Console FAQ
https://aws.amazon.com/amplify/console/faqs/
Complete workflow for developing, deploying and hosting SPA or static sites 
Continuous deployment--deploy updates on every code commit to Git 
Connect to custom domain 
Supports all SPA frameworks (e.g. React, Angular, Vue.js, Ionic, Ember) as well as static-site generators (e.g. Gatsby, Eleventy, Hugo, VuePress, Jekyll)
Framework provides CLI and library. CLI provisions backend resources
Console can provision/update resources on each check-in to source control. Variety of configurations, such as isolated backend deployment per branch. (?) 
Connect source repo. Console determines framework used. Builds and deploys app to CDN. Detects backend using framework and deploys resources.
An ‘app’ is a project container. Each app contains list of branches from source repo. Can connect additional feature branches, custom domain, or access build logs
Continuous deployment: devops strategy where every code commit is automatically released to production or staging environment. Hosted app always reflects latest code in repo.
Supports GitHub, BitBucket, GitLab, AWS CodeCommit.Does not support private Git servers
Git access tokens…
Environment variables such as db connection details, API keys, etc. are encrypted. Applies env vars across all branches.
When a build is run: AWS Amplify Console will create a temporary compute container (4 vCPU, 7GB RAM), download the source code, execute the commands configured in the project, deploy the generated artifact to a web hosting environment, and then destroy the compute container. During the build, the AWS Amplify Console will stream the build output to the service console and Amazon CloudWatch
AWS Amplify Console leverages Git’s branching model to create new environments every time a developer pushes code to a new branch. In typical development teams, developers deploy their ‘master’ branch to production, keep the ‘dev’ branch as staging, and create feature branches when working on new functionality. The AWS Amplify console can create frontend and backend environments linked to each connected branch. This allows developers to work in sandbox environments, and use ‘Git’ as a mechanism to merge code and resolve conflicts. Changes are automatically pushed to production once they are merged into the master (or production) branch. 
Atomic deploys: do not have to invalidate CDN caches, site is ready to view after deployment
Can be password protected and set access for different users 


Amplify Device Farm FAQ
https://aws.amazon.com/device-farm/faqs/

“AWS Device Farm allows developers to increase application quality, time to market, and customer satisfaction by testing and interacting with real Android and iOS devices in the AWS Cloud. Developers can upload their app and test scripts and run automated tests in parallel across 100s of real devices, getting results, screenshots, video, and performance data in minutes. They can also debug and reproduce customer issues by swiping, gesturing, and interacting with a device through their web browser.”



Amplify Docs
https://aws-amplify.github.io/amplify-js/api/
This is bare bones docs, very little explanation once you get past the introduction, but it does have classes and methods all in one place.

From the introduction:

“AWS Amplify is a JavaScript library for frontend and mobile developers building cloud-enabled applications”

Declarative, easy to use interface across cloud operations
Goes well with any JS based frontend workflow

Features/APIs 
Authenitcaiton
Analytics
API (for 3rd party?)
GraphQL Client
Storage 
Push Notifications
Interactions
PubSub
Internationalization
Cache
Predictions (AI and ML)

Installation 
Npm install aws-amplify --save 
Or install individual module: npm install @aws-amplify/auth --save 

If you are using a framework (e.g. React), install additional packages

Configuration
“Somewhere in your app, preferably at the root level, configure Amplify with your resources.” 
Amplify.configure….
Whaaaat? Maybe a little more specificity?

Console User Guide
https://docs.aws.amazon.com/amplify/latest/userguide/amplify-console-ug.pdf
Various Amplify videos, none of which were very helpful

https://medium.com/@christophe.bougere/aws-amplify-beyond-the-quickstart-c389f8e44c92

What is AWS Amplify
https://www.youtube.com/watch?v=QlWtERFpKNU

Problem it tries to solve:
Seamless experience between platforms

Compares to Firebase

Blah blah, aws fanboy 

Firebase vs. AWS Amplify
https://www.youtube.com/watch?v=ucmbO2lWC2A

Amplify 
	Different env.
	Continuous deployment, github
	Integration with graphql
Firebase 
	Cloud firestore dedicated db 
	Callable functions with auth context from frontend 
	More features, analytics, etc. 
	ML Kit machine learning features

Prices
	Amazon prices are low 
	Both have free tier
	Amplify is slightly cheaper for lots of user 
	Firebase might be cheaper for realtime 

Raason to use: increase speed and flexibility of development 

Amplify 
Vanilla js ok 
Amplify folder in root 

Firebase is a little simpler but less flexible 

Both add lots of stuff to node

Both provide Js librarires 

Firebase single nosql db hard to migrate into our out of 


Other Resources
https://github.com/dabit3/awesome-aws-amplify
 




