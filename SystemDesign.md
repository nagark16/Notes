Horizontal -- load balancing required, resilient to failures, remote procedure calls, data inconsistency, scales well with users increase
Vertical -- load balancing not applicable, single point of failure, inter process communication, data consistency, hardware limitation

in real world we take best of both Horizontal and Vertical - we take resilient to failures and scales well with users increase from Horizontal
                                                           - we take inter process communication speed and data consistency from Vertical

                                                           by large number of powerful computer systems

Load balancing  
    consistent hashing
    x requests n servers. so each server will have x/n load and load factor is 1/n
    sticky & non-sticky:
        user <----> load balancer <---->  instance(n number of instances)   
        when a request reaches a load balancer. the load balancer can forward to any instance (called non-sticky) or it can be forwarded to same instance all the time (called sticky)

    https://stackoverflow.com/questions/10494431/sticky-and-non-sticky-sessions
    https://www.citrix.com/en-in/glossary/load-balancing.html
    https://www.nginx.com/resources/glossary/load-balancing/
    http://michaelnielsen.org/blog/consistent-hashing/
    
Message/Task Queue = notification + load balancing + heart beat + persistance
    ex: RabbitMQ, ZeroMQ, JMS(Java Messaging Service)

Monolith: 
    adv: scales out, good for small teams, less complex, less duplication, procedure call is faster
    dis adv: more context requried for new change/devlopment, complicated deployments, too much responsibility on each server, single point of failure

Microservices
    adv: scalability, easier for new team members, working in parallel, easier to reason about, needs skilled architects

Sharding:
    sql opitimzation, indexing, 
    distribute data based on columns is called Vertical partitioning    
    break data into pieces and allocate to different database servers is called Horizontal partitioning(sharding) - availability, consistency
        problems: 1. joins
                  2. shards are inflexible we can make database servers flexible by having consistent hashing(followed by memcache)
        best practices: use index