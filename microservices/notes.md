# Microservices

##### So, what does this lovely word means?

We can say that its a software development ***architecture*** or we can also say it's an extension of SOA but improved and better thought. This type of architecture aims to break down an application and isolate it's functions or business logic. Let's call this isolations services. 

> By the way, SOA means Service Oriented Architecture.

A service is designed to **meet specific and unique business need**. If a service or this isolated business logic do more than it's needed or it contains logic that shouldn't be there, this will pollute the service and won't be aligned in the definition of a microservice.

##### A few examples on what a service can be:

- User Management
- Payments
- Sending Emails

This type of architecture allows to be developed and deplyed without affecting others, we will talk about this later on when describing some advantages of it.

Also, it's inteded to be the opposite of monolith architecture, which are built as a single autonomous unit.

##### Let's do a quick definition of Monolith Architecture

This is the traditional unified model design of a software program ***Composed all in one piece*** 

> The definition of microservice might recall another type of architecture like SOA, which is a software design that is well formed.

##### Let's have some differences

- **Size**: In microservices, the size of each service should be small, because each service has a single responsability, while in SOA can contain many business logic.
- **Reusability**: One of the goals of SOA is to reuse components without worrying about coupling, while in microservices we try to minimize this.
- **Comunication**: In SOA this happens usually synchronously through an enterpise service bus ***ESB***. This introduces a critical point of failure and latency. While in microservices failure is weaker thanks to the indepence of each service. For example, a pub-sub model can be used to allow a service to stay up to date on changes.
- **Data Duplication**: In SOA the goal is to allow all aplications or services to access data synchronously directly at the source. With microservices, each service has access to all the data it needs locally. In other words, each service will have it's own DB. This brings better performance and agility, sometimes this is prefered even if we duplicate some data over a few services touching the same DB and having performance issue.


##### Advantages of Microservices

- **Indepent Development**: Teams can choose the technologies that best suites each service, they can use different stacks without limiting other services. A single team can build, test, deploy a service, promoting faster deployment and with no risk on hurting other services
- **Indepent Deployment**: Microservices can be deploy independently, meaning that we can update a service and this wont redeploy or risk the entire app. This make easier to handle and narrow bugs. In the traditional monolith architecture, if there's a bug, it can block the entire release process.
- **Indepent Scaling**: Services can scale separately to it needs, optimizing cost and time, since there's no need to scale the entire app
- **Small Targeted Teams**: Teams can be targeted to only one service. This will make code easier to read, mantain and even for new members to join quicker and smoother.
- **Small Code Base**: In a monolith app the code dependency its too high, and it gets mixed up over the time. Which makes adding a new functionality a bit of a hell because you might end up writing lines of code in places where you shouldn't. 
- **Data Isolation**: Each service will point to it's own DB, meaning that no other service will have transactions on it. This is good because it cannot harm other services if a change happens. And also, having it's own DB improves performance
- **Resilence**: With microservices, critical points of failure are reduced when a service goes down, the whole app doesn't stop functioning when a monolith does. Errors will be isolated and therefore easier to handle.
 
##### Disadvantages of Microservices
- **Complexity**: while each service is simpler, the system is more complex. We should be carefull to select and setup all services and databases, then deploy each of these components independently.
- **Testing**: It gets tricky because having multiple services can make writing test more complex, especially when there are many dependencies between.
- **Data Integrity**: Microservices have a distributed database architecture, which is a challenge for data integrity. Some business transactions require update multiple functions of the app, needing to update multiple databases owned by different services. This requires to setup an eventual consistency of data. Which is more complex.
- **Network Latency**: Using small services can result in increased communication between services. Also, if you have a chan of dependency, additional latency can become a problem. We should use asynchronous communication which also adds complexity.


In microservices its inevitable that some services needs to communicate with each other. This can be done in two ways ***Orchestration or Choreography***

##### Orchestration

Is where an *orchestrator* is the only one to have knowledge of the other services, in case of an update of the service, we should be carefull to not break it. This approach is not good because one of the issue is the latency due to the sync calls, and also having to many services will convert it like a monolith in the end.

##### Choreopraphy

With this approach we won't have dependency or latency problems in the system. The solution here is to use events with a publish-subscribe model. When an action is taken, the service will publish an event to which the other service will be subscribed to make the necesary changes.

Communication is asynchronous and services are unware from each other, therefore the system is efficient and easy to mantain an scale.


*Information taken from [https://medium.com/swlh/microservices-architecture-from-a-to-z-7287da1c5d28](https://medium.com/swlh/microservices-architecture-from-a-to-z-7287da1c5d28)*


