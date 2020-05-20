# JAM Stack, Headless CMS, and Backend-as-a-Service

## JAM Stack Overview 

JAM Stack architecture, headless CMS, and Backend-as-a-Service (BaaS) are concepts with a lot of overlap, and none of them has clearly defined boundaries where we can easily distinguish one from the other. So what are these concepts? What do they have in common? How are they related?

The term “JAM Stack” was coined by the founder of Netlify, Mathias Biilman, to replace the term “static site” with something more descriptive in terms of modern web practices. “JAM” refers to JavaScript, API, and Markup. Typically JAM Stack architecture refers to sites or applications built with a static-site generator or frontend frameworks like React or Angular. They include JavaScript for interactivity, and backend features are provided through APIs, either third-party or home-brewed. Frontend files are pre-rendered and served from a CDN. JAM Stack applications often employ a Git-based flow where the frontend static files are compiled with every commit to master. 

The benefit of using a JAM stack approach is that page loads are very fast since they are not built on the fly, but hosted on a CDN. Frontend and backend code is completely decoupled. By taking a microservices approach to backend functionality, scaling can be accomplished more easily, and much of the responsibility of building, maintaining, and securing backend functions can be off-loaded to specialized service providers.

## Headless CMS Overview 

A  CMS is a Content Management System, such as WordPress. A CMS is typically a service with a WYSIWYG editor for creating a frontend and hosting and managing related content, such as blog posts. A “headless” CMS is essentially the same thing, except that the service does not provide a frontend; rather it provides an API for accessing the content that is stored and managed by the CMS. A related term is “decoupled” CMS. In the case of a decoupled CMS, the service does provide a frontend, but it still uses an API interface for accessing content. 

## Backend-as-a-Service Overview 

A BaaS is very similar to a headless CMS, in that it provides backend functionality that is accessible through an API while taking a BYOB approach to the frontend. In both cases, a user is free to create any kind of frontend they want to interact with the API backend interface.

The main difference seems to be in the kind of features and functionality each of these services prioritizes. CMS features unsurprisingly tend to be related to content storage and retrieval, while BaaS functionality focuses on backend functions like authentication, SMTP, push notifications, and realtime.

## Putting it all together 

According to jamstack.org, an application cannot be considered a JAM Stack application if:
It is built with server-side cms
It is a monolithic server-run app that relies on a backend language 
It is a SPA that uses isomorphic rendering to build views at runtime

So applications and websites built with a headless CMS or a BaaS are not necessarily JAM Stack examples, but they can be, depending on how their frontend is built and hosted.

Furthermore, there is no reason an application can’t take a JAM Stack approach using both a headless CMS and a BaaS to provide content and backend functionality. See the Baqend example under Further Reading > Putting it all together below.

The JAM Stack, along with BaaS and headless CMS services as well other “serverless” approaches are all part of a trend toward decentralization and specialization in web development, where developers mix and match services in a way that meets their unique needs.

## Further Reading

#### Putting it all together
https://medium.baqend.com/building-static-sites-in-2017-cloud-hosted-cms-backed-and-api-driven-f68b5debc396
A description of how one might integrate a headless CMS with a BaaS. 
https://www.contentful.com/r/knowledgebase/jamstack-cms/

### JAM Stack
https://jamstack.org/
	A compendium of resources. The videos of Mathias Biilman talks are particularly useful.
https://www.gridhaus.com/blog/jamstack-modern-web-architecture-in-digestible-terms
An overview.
https://medium.com/front-end-weekly/the-issues-with-jamstack-you-might-need-a-backend-d101791de36a
A critique of JAM Stack architecture.

### Headless CMS and Content-as-a-Service
https://headlesscms.org/projects/webiny
https://www.coredna.com/blogs/headless-vs-decoupled-cms
https://css-tricks.com/what-is-a-headless-cms/
https://en.wikipedia.org/wiki/Content_management


https://css-tricks.com/jamstack-cmss-have-finally-grown-up/
https://www.storyblok.com/tp/headless-cms-explained
https://www.contentful.com/r/knowledgebase/content-as-a-service/
https://simplea.com/Articles/what-is-content-as-a-service
https://www.sanity.io/blog/headless-cms-explained

### Backend-as-a-Service
https://bkpk.dev

### Related Concepts

#### Build tools 
https://medium.com/xebia-engineering/a-general-introduction-to-build-tools-9070a47ed405
https://survivejs.com/webpack/appendices/comparison/

#### Static site generators

https://css-tricks.com/really-makes-static-site-generator/
https://www.quora.com/How-does-a-static-site-generator-like-Jekyll-work
https://medium.com/@alexsanchezdesigns/an-introduction-to-static-site-generators-a75ab6149285

#### Isomorphic rendering /Server-Side Rendering (SSR)
https://www.onebigfluke.com/2015/01/experimentally-verified-why-client-side.html?m=1
https://en.wikipedia.org/wiki/Isomorphic_JavaScript
