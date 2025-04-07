# Microservices or modular monolith?

In today’s tech world people scream microservices when they don't know what to say :) 

Instead of going straight to microservices, there’s an alternative solution: a **Modular Monolith**. The modular monolith provides many of the benefits of microservices, such as clear separation of concerns and maintainability, without the complexity and overhead that come with managing multiple distributed services. Think like applying [bounded contexts](https://martinfowler.com/bliki/BoundedContext.html) pattern on a monorepo.

Here’s a closer look at why microservices might not be the right answer for every team or project and why a **Modular Monolith** might be a better approach.

## 1. Network Latency
When you break down a monolith into microservices, you inevitably introduce inter-service communication over a network, which adds latency. Unlike a monolithic application where method calls are local and efficient, communication between microservices typically involves HTTP requests, message queues, or event streaming. This additional network hop can slow down response times, leading to performance bottlenecks that were never an issue in the monolithic design.

While you can optimize some network communication strategies, like using gRPC or caching, the fundamental latency problem remains. So, if your use case demands ultra-low latency, moving to microservices may create a performance gap you can’t easily bridge.

### The Modular Monolith Alternative:
In a modular monolith, services and modules are logically separated within a single codebase, allowing you to structure your application with clear boundaries while keeping all interactions local. There is no added network latency, and your system remains efficient without sacrificing the organizational benefits of separation.

## 2. Data Consistency Challenges
One of the significant issues in a microservices architecture is managing data consistency across services. In a monolith, it’s easier to maintain consistency since all data resides in a shared database. However, in a microservices model, each service often owns its own data store, and managing consistency between them can be tricky.

Techniques like eventual consistency, event sourcing, or distributed transactions (Saga pattern) can be used to handle this, but they come with added complexity. Ensuring that all services maintain accurate and up-to-date data without conflicts or race conditions requires careful design and additional overhead.

### The Modular Monolith Alternative:
In a modular monolith, you can maintain a single database, which simplifies the consistency and transactional guarantees across services. By structuring your application into modular components, you can still achieve clear separation of concerns without introducing the complexities of managing multiple data sources and eventual consistency.

## 3. Operational Complexity
Microservices introduce significant operational complexity. With multiple independent services running, monitoring, logging, deployment, and failure recovery become much more complicated. You have to deal with service discovery, orchestration, load balancing, and managing state across distributed systems.

Additionally, the complexity increases when you consider the need for automated testing, CI/CD pipelines, and the increased burden on DevOps teams to ensure that all services are functioning optimally. If your organization is not equipped with the right tools and expertise, this operational burden can significantly slow down development velocity.

### The Modular Monolith Alternative:
A modular monolith can achieve much of the organizational structure and separation that microservices offer but without the operational overhead. Since everything resides in one codebase and deployment unit, you can simplify operations while still organizing your system in a way that allows for independent development and testing of different modules. This reduces the need for complex orchestration tools and multiple deployment pipelines.

## 4. Single Responsibility & Service Ownership
Before splitting your monolith, ask yourself: does each service have a clear, single responsibility? Microservices require strict boundaries between services to avoid overlapping responsibilities, which can lead to “service bloat” or a fractured system. Without a clear domain model and a well-defined responsibility for each service, you'll end up with chaos instead of clarity.

Moreover, microservices require each service to be owned by a dedicated team, which might not always be feasible. The team must have sufficient expertise and autonomy to maintain, deploy, and scale their service. But this leads to another challenge: silos. If your team structure isn’t aligned to support microservices, you might inadvertently create isolated teams that focus only on their services, which could lead to inefficiencies and communication problems.

### The Modular Monolith Alternative:
In a modular monolith, you can define clear boundaries between components or modules without necessarily separating them into independent services. This allows teams to work on specific areas of the system while avoiding the overhead of service ownership, deployment, and scaling. As teams grow, they can progressively modularize the system to move towards a microservices architecture when necessary, but without jumping into it prematurely.

## 5. Communication Between Services: Synchronous vs. Asynchronous
Microservices need to communicate with each other, but the way this communication happens is crucial. There are two primary types: synchronous and asynchronous.

- **Synchronous communication** (e.g., REST APIs) means that one service must wait for the other to respond before continuing. This can introduce performance bottlenecks, especially if services are dependent on each other in a complex chain.

- **Asynchronous communication** (e.g., message queues, event-driven systems) allows services to continue processing without waiting for a response. While this is more scalable and decouples services, it introduces its own challenges in terms of handling eventual consistency, retries, and message processing order.

Choosing the right communication pattern is essential for maintaining system reliability and performance.

### The Modular Monolith Alternative:
In a modular monolith, communication is always local, and modules can call each other directly through method invocations or shared data models. This avoids the overhead and complexity of handling inter-service communication. Since there is no need for a network call, the system can operate efficiently without the need for complex messaging or event systems.

## 6. Fault Tolerance and Service Isolation
A monolithic architecture often has natural resilience built in—if one component fails, the rest of the system may still function, albeit in a degraded mode. In a microservices architecture, however, failures can be much more widespread, especially if services aren’t isolated properly.

You need to carefully design your system so that failures can be isolated without bringing down the entire system. Techniques like circuit breakers, retries, and fallbacks can help mitigate failure propagation, but they require careful implementation.

### The Modular Monolith Alternative:
While a modular monolith may not provide the same level of isolation as microservices, it’s often easier to maintain fault tolerance within a single application. Modules can still be isolated to a degree, and failures in one part of the system won’t necessarily cause the entire application to fail. In addition, error handling can be simpler without the need for managing distributed systems.

## Conclusion
Microservices are not a magic bullet. They introduce complexities that can sometimes outweigh the benefits. While they work well for large, complex systems with independent teams and well-defined service boundaries, they might not be the right fit for every organization or project. Before diving into microservices, ask yourself if your system needs them.

Instead of jumping straight to microservices, consider adopting a **Modular Monolith**. It offers many of the same benefits of microservices—such as clear module separation and easier maintenance—without the operational overhead and complexity. In many cases, a modular monolith is all you need, and it can evolve into microservices later if and when your system truly requires it.

Remember: before you go micro, be sure you’ve asked the right questions.
