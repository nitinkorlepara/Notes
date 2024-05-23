# MicroServices Using Spring 

- Small applications. 
- scaling is easier.
### Communication 
    - Synchronous
    - Asynchronous
        - Kafka 
        - Rabbit MQ
        - Google Pub/Sub
        - Amazon services
### Design Patterns
- SAGA
    - A sequence of local transactions in which a microservices triggers another microservice via event \ message
        - Orchestration 
            - a central controller
        - Choreography 
            - Each microservice knows what needs to be done when an event occurs and is posted on an event stream/bus.
- API Composition
    - Queries are implemented by defining an API composer, which invokes the services that own the data and performs an in mermory join of results
- CQRS
    - Command query Responsibility Segregation
- Event Sourcing
    - It stores all the changes,rather than jus tthe its current state.

- Service mesh
    - The application networking functions are delegated to the infrastructure rather than being mixed with business logic.


### Rest Template 
- RestTemplate provides certain methods to perform the REST calls. The following are some of these methods:
    - DELETE:              delete(String, String...)
    - GET:                 getForObject(String, Class, String...)
    - POST:                   postForLocation(String, Object, String...)
    - PUT:               put(String, Object, String...)


##### Additional Resources
[12 Factors](https://12factor.net/) <br>
[Communication](https://medium.com/the-sixt-india-blog/microservice-communication-53cbc93cf4de) <br>
[communication Design patterns](https://blog.devgenius.io/microservice-architecture-communication-design-patterns-70b37beec294) <br>
[SAGA](https://dzone.com/articles/microservices-using-saga-pattern) [SAGA](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/saga/saga)<br>

