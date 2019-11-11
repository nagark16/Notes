* Horizontal -- load balancing required, resilient to failures, remote procedure calls, data inconsistency, scales well with users increase
* Vertical -- load balancing not applicable, single point of failure, inter process communication, data consistency, hardware limitation

* In real world we take best of both Horizontal and Vertical
            * - we take resilient to failures and scales well with users increase from Horizontal
            * - we take inter process communication speed and data consistency from Vertical
                    * by large number of powerful computer systems

## Load balancing  
    * consistent hashing
        *  x requests n servers. so each server will have x/n load and load factor is 1/n
    * sticky & non-sticky:
        * user <----> load balancer <---->  instance(n number of instances)   
        * when a request reaches a load balancer. the load balancer can forward to any instance (called non-sticky) or it can be forwarded to same instance all the time (called sticky)

    * Load Balancing is a key concept to system design. One simple way would be hashing all requests and then sending them to the assigned server.

    * The standard way to hash objects is to map them to a search space, and then transfer the load to the mapped computer. A system using this policy is likely to suffer when new nodes are added or removed from it. 

    * Some terms you would here in system design interviews are Fault Tolerance, in which case a machine crashes. And Scalability, in which case machines need to be added to process more requests. Another term used often is request allocation. This means assigning a request to a server.

    * Load balancing is often tied with service discovery and global locks. The type of load we want to balance is that of sticky sessions.

    * Load Balancing is a key concept to system design. One of the popular ways to balance load in a system is to use the concept of consistent hashing. Consistent Hashing allows requests to be mapped into hash buckets while allowing the system to add and remove nodes flexibly so as to maintain a good load factor on each machine.

    * The standard way to hash objects is to map them to a search space, and then transfer the load to the mapped computer. A system using this policy is likely to suffer when new nodes are added or removed from it. 

    * Consistent Hashing maps servers to the key space and assigns requests(mapped to relevant buckets, called load) to the next clockwise server. Servers can then store relevant request data in them while allowing the system flexibility and scalability.

    * Some terms you would here in system design interviews are Fault Tolerance, in which case a machine crashes. And Scalability, in which case machines need to be added to process more requests. These two principles are allowed by Consistent Hashing, and hence it is an important building block to a system design architect's toolbox.

    * Another term used often is request allocation. This means assigning a request to a server. Consistent hashing assigns requests to the servers in a way that the load is balanced are remains close to equal. 

    * Server architecture is a subjective concept, and there are outliers for many cases. Don't think of Consistent Hashing as a silver bullet for fault tolerance and scalability, but a useful concept for request allocation.

    (https://stackoverflow.com/questions/10494431/sticky-and-non-sticky-sessions)
    (https://www.citrix.com/en-in/glossary/load-balancing.html)
    (https://www.nginx.com/resources/glossary/load-balancing/)
    (http://michaelnielsen.org/blog/consistent-hashing/)
    (https://www.hackerearth.com/practice/data-structures/hash-tables/basics-of-hash-tables/tutorial/)
    (http://www.tomkleinpeter.com/2008/03/17/programmers-toolbox-part-3-consistent-hashing/)


## Message/Task Queue
    * = notification + load balancing + heart beat + persistance
    * ex: RabbitMQ, ZeroMQ, JMS(Java Messaging Service)

    * Messaging Queues are widely use in asynchronous systems. Message processing in an asynchronous fashion allows the client to relieve itself from waiting for a task to complete and, hence, can do other jobs during that time. It also allows a server to process it's jobs in the order it wants to.

    * Messaging Queues provide useful features such as persistence, routing and task management. We will be discussing the benefits of a message queue in future videos.

    * A system having a message queue can move to higher level requirements while abstracting implementation details of message delivery and event handling to the messaging queue.

    * The 'queue' is just a name for this data structure. In practice, it could be storing messages using any policy. Some examples of message queues are Kafka and RabbitMQ. They are widely used for various purposes such as command query request segregation (CQRS) and event sourcing.

    (http://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html)
    (https://stackoverflow.com/questions/16715380/what-is-the-difference-between-asynchronous-and-synchronous-http-request)
    (https://www.enterpriseintegrationpatterns.com/patterns/conversation/RequestResponse.html)
    (http://blog.codepath.com/2013/01/06/asynchronous-processing-in-web-applications-part-2-developers-need-to-understand-message-queues/)
    (http://highscalability.com/blog/2012/12/17/11-uses-for-the-humble-presents-queue-er-message-queue.html)
    (https://www.cloudamqp.com/blog/2014-12-03-what-is-message-queuing.html)
    (https://www.rabbitmq.com/getstarted.html)

## Monolith: 
    * adv: scales out, good for small teams, less complex, less duplication, procedure call is faster
    * dis adv: more context requried for new change/devlopment, complicated deployments, too much responsibility on each server, single point of failure

## Microservices
    * adv: scalability, easier for new team members, working in parallel, easier to reason about, needs skilled architects

## Sharding:
    * sql opitimzation, indexing, 
    * distribute data based on columns is called Vertical partitioning    
    * break data into pieces and allocate to different database servers is called Horizontal partitioning(sharding) - availability, consistency
        * problems: 1. joins
                    2. shards are inflexible we can make database servers flexible by having consistent hashing(followed by memcache)
        * best practices: use index