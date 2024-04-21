- Software architectural style
- set of small, independent services that communicate with each other through ***APIs***
- monolithic applications are ineffective - scaling such applications is expensive since we have to scale the whole even though only a particular service gets a lot of traffic
- microservices can be built using different technologies and ***deployed, scaled***, updated independently
- they have their own independent ***databases***
![](../Media/Microservice%20Using%20ASP.webp)
- dockerized microservice: https://www.c-sharpcorner.com/article/microservice-using-asp-net-core/

## Principles of Microservices
1. Modelled around business domain: each domain focuses on one thing and its associated logic
	- can migrate easily to next version
	- scale independently
2. Culture of Automation: there is an increase in the number of deployment units compared to monolithic architecture -> the need for ***continuous integration and continuous delivery***.
3. Hide Implementation Details: reduce coupling
4. Decentralization: each service to manage their own database
5. Deploy Independently
6. Failure Isolation
7.  Highly Observable: logging events and stats
## Disadvantages of Microservices
- Additional complexity introduced by inter-process communication mechanisms between services.
- Difficult to create a consistent testing environment involving all services.
- Requires high level of automation to manage multiple instances of diffident services.
- Managing multiple databases.
- Inter-process calls are slow.
- Difficult debugging.
- Complexity in DevOps.
- Higher monitoring costs.
- Formal documentation overhead.
- Lack of governance.


-------------------

# Why Microservices?

- the most popular architecture paradigm
- not tied to specific technology
- solves real problems
- in high demand in the job market
- generates a lot of buzz

# History of Microservices

- Microservies are a result of problems with 2 architecture paradigms:
    - Monolith
    - SOA

### Monolith

- the original architecture
- monolith applications do not expose ways to share data and functionality
- all software components are exceuted in a single process
- no distribution of any kind :arrow_right: the core of the application is monolith
- strong coupling between all classes
- usually implemented as Silo :arrow_right: standalone app
- example:
    - HR App and its parts
        - browser
        - database
        - core of the application

##### Pros

- easier to design
    - no network
    - no messaging mechanisms
    - no queues
    - no cross process debugging

- performance

### SOA (Service Oriented Architecture)

- apps are services exposing functionality to the outside world
- services expose metadata to declare their functionality
- usually implemented using SOAP & WSDL
    - SOAP is a protocol for web service :arrow_right: long and complicated XML document
    - WSDL is another XML document, containing the metadata about the service
- usually implemented with ESB :arrow_right" Enterprise Service Bus is a family of products that were designed to mediate between the client and the services and between the services themselves
- ESB communicates with the services
- client "talks" to the ESB which then routes it to the appropriate service

##### Pros

- sharing data & functionality
- polyglot between services

# Problems with Monolith & SOA

### Single Technology Platform

##### Monolith Problems

- with monolith, all the components must be developed using the same development platform
- not always the best for the task
- can't use specific platform for specific features
- future upgrade is a problem - need to upgrade the whole app

### Inflexible Deployment

- with monolith, new deployment is always for the whole app
- no way to deploy only part of the app
- even when updating only one components - the whole codebase is deployed
- forces rigorous testing for every deployment
- forces long development cycles

### Inefficient Compute Resources

 - with monolith, compute resources (COU and RAM) are divided across all components
 - if a specifis components needs more resources - no way to do that
 - very inefficient

### Large and Complex

- with monolith the codebase is large and complex
- every little change can affect other components
- testing not always detects all the bugs
- very difficult to maintain
- might make the system obsolete

### Complicated and Expensive ESB

- with SOA, the ESB os on of the main components
    - ESB takes care of routing, validation, authentication, aggregation and more
- can quickly become bloated and expensive
- tries to do everything
- very difficult to maintain


### Lack of Tooling

- for SOA to be effective, short development cycles were needed
- allow for quick testing and deployment
- no tooling existed to support this
- no time saving was achieved

# Microservices Architecture

- has to be modular with simple API

## Characteristics of Microservices

- componentization via Services
- organized around business capabilities
- products not projects
- smart endpoints and dumb pipes
- decentralized governance
- decentralized data management
- infrastructure automation
- design for failure
- evolutionary design

### Componentization

- modular design is always a good idea
- components are the parts that together compose the software
- modularity can be achieved using:
    - libraries - called directly within the process
    - services - called by out-of-process mechanism (Web API, RPC)
- in microservices we prefer using Serivces for the componentization
    - componentization via services
- libraries can be used inside the service
- motivation:
    - independent deployment
    - well defined interface

### Organized Around Business Capabilities

- traditional projects have teams with horizontal responsibilities - UI, API, Logic, DB etc. :arrow_right: slow, cumbersome inter-group communication
- with microservices every service is handled by a single team, responsible for all aspects
- services are organized around business capabilities
- motivation:
    - quick development
    - well-defined boundaries

## Products not Projects

- with traditional projects, the goal is to deliver a working code
    - no lasting relationship with the customer
    - often no acquaintance with the customer
    - after delivering - the team moves on to the next project

<br>

- with microservices - the goal is to deliver a working product
- a product needs ongoing support and requires close relationship with the customer
- the team is responsible for hte microservice after the delivery too

<br>

- motivation
    - increase customer's satisfaction
    - change developers' mindset

## Smart endpoints and dumb pipes

- traditional SOA projects used 2 complicated mechanisms
    - ESB
    - WS-* protocol
- made inter-service communication complicated and difficult to maintain

<br>

- microservices systems use "dumb pipes" - simple protocols
- strive to use what the web already offers
- usually - REST API, the simplest API in existence
- with microservice architecture each microservice exposes a REST API and communicate directly with each other using nothing other than simple HTTP calls
- ``important notes``:
    - direct connections between services is not a good idea
    - better use discovery service or a gateway
    - in recent years more protocols were introduced (GraphQL, gRPC) some of them quite complex

<br>

- motivation:
    - accelerate development
    - make the app easier to maintain
        - less engines and protocols

## Decentralized Governance

- in traditional projects there is a standard for almost anything:
    - which dev platform to use
    - which database to use
    - how logs are created
    - and more

<br>

- with microservices each team makes its own decisions:
    - which dev platform to use
    - which database to use 
    - how logs are created

<br>

- each team is fully responsible for its service
    - "You build it, you run it."
- and so will make the optimal decisions
- enabled by the loosely coupled nature of Microservices
- multi dev platform is called *``Polyglot``*

<br>

- motivation:
    - enables making the optimal technological decisions for the specific service

## Decentralized Data Management

- traditional systems have a single database
- stores all the system's data from all the components

<br>

- with microservices each service has its own database and they are not sharing the database with other components

- important notes:
    - this is the most controversial attribute of Microservices
    - not always possible
    - raises problems such as distributes transactions, data duplication and more
        - for example for an ecommerce website we need to store the customer details and the order details. These needs to be in sync but if they are handled by 2 different microservices with 2 databases it can be a problem as updating data in the databases should happen at the same time. If the databases go out of sync then it can be a problem.
    - **do not insist on it**

<br>

- motivation:
    - right tool for the right task - having the right database is important
    - encourages isolation

## Infrastructure Automation

- the SOA paradigm sufferent from lack of tooling
- tooling greatly helps in deployment using:
    - automated testing
    - automated deployment

<br>

- for microservices automation is essential
- short deployment cycles are a must
- can't be done manually
- there are a lof of automation tools:
    - Azure DevOps
    - GitLab
    - Jenkins

<br>

- motivation:
    - short deployment cycles

## Design for failure

- with microservices there are a lot of processes and a lot of network traffic
- a lot can go wrong
- the code must assume failure can happen and handle it gracefully
- extensive logging and monitoring should be in place

<br>

- catch the exception
- retry
- log the exception
- monitoring
    - alerting
    - monitoring products:
        - Azure Monitor
        - Application Insights
        - Kubernetes

<br>

- motivation:
    - increase system's reliability

## Evolutionary design

- the move to microservices should be gradual
- no need to break everything apart
- start small and upgrade each part separately

## Summary

- the most important attributes:
    - componentization
    - organized around business capabilities
    - decentralized governance
    - decentralized data management (when possible)
    - infrastructure automation


# Problems solved by Microservices

## Single technology platform

- with monolith, all the components must be developed using the same development platform
- not always the best of the task
- can't use specific platform for specific features
- future upgrade is a problem - need to upgrade the whole app

<br>

- with microservices the decentralized governance attribute solves it

## Inflexible Deployment

- with monolith new deployment is always for the whole app
- no way to deploy only part of the app
- even when updating only one component - the whole codebase is deployed
- forces rigorous testing for every deployment

<br>

- with microservices the componentization via sercices attribute solves it
- also - decentralized data management

## Inefficient compute resources

- with monolith, compute resources (CPU and RAM) are divided across all components
- if a specific components needs more resources - no way to do that
- very inefficient

<br>

- with microservices, the componentization via services attribute solves it

## Large and complex

- with monolith the codebase is large and complex
- every little change can affect other components
- testing not always detects all the bugs
- very difficult to maintain
- might make the system obsolete

<br>

- with microservices the componentization via services attribute solves it
- well bounded code
- also - decentralized data management
and - organized around business capabilities


## Complicated and Expensive ESB

- with SOA the ESB is one of the main components
- can quickly become bloated and expensive
- tries to do everything
- very difficult to maintain

<br>

- with microservices the smart endpoint and dumb pipes attribute solves it
- remember:
    - application gateway and discovery
    - other APIs: GrapQLm gRPC


## Lack of tooling

- for SOA to be effective short development cycles were needed
- allow for quick testing and deployment
- no tooling existed to support this
- no time saving was achieved

<br>

- with microservices the infrastructure automation attribute solves it
- automates testing and deployment
- provides short deployment cycles
- make the architecture efficient and effective

# Designing Microservices Architecture

## Architecture Process

- designing microservices architecture should be methodical
- do not rush into development
- "plan more, code less"
- critical to the success of the system

### Mapping the components

- the single most important step in the whole process
- determines how the system will look like in the long run
- once set - not easy to change

##### What is it?

- defining the various components of the system
- remember: Components = Services

<br>

- Mapping should be based on:
    - ``Business requirements``:
        - the collection of requirements around a specific business capability
        - for example: orders management:
            - add, remove, update, calculate amount
    - ``Functional autonomy``:
        - the maximum functionality that does not involve other business requirements
        - for example:
            - retrieve order made in the last week
            - get all the orders made by users aged 34-45
    - ``Data entities``:
        - service is designed around well-specified data entities
        - for example: orders, items
        - data can be related to other entities byt just by ID
            - example: order stores the Customer ID
    - ``Data autonomy``:
        - underlying data is an atomic unit
        - servcice does not depend on data from other services to function properly
        - for example: employees service that relies on addresses service to return employee's data


### Mapping the components - Example

- eCommerce System
    - services:
        - inventory
            - business requirements:
                - manage inventory items
            - functional:
                - add, remove, update, quantity
            - data entites:
                - items
            - data autonomy:
                - none
        - orders
            - business requirements:
                - manage orders
            - functional:
                - add, cancel, calculate sum
            - data entites:
                - orders, shipping address
            - data autonomy:
                - related to Items by ID
                - related to Customer by ID
        - customers
            - business requirements:
                - manage customers
            - functional:
                - add, update, remove, get account details
            - data entites:
                - customer, address, contact details
            - data autonomy:
                - related to Orders by ID
        - payments
            - business requirements:
                - perform payments
            - functional:
                - perform payments
            - data entites:
                - payment history
            - data autonomy:
                - None

<br>

- Edge case #1:
    - retrieve all customers from NYC with total number of orders for each customer
- three approaches:
    - data duplication:
        - order service and customer service both store the same data in their respective databases
    - service query:
        - 2 services talk to each other
        - problem: loads the network and services
            - **performance problems**
    - aggregation service:
        - data and service are not mixed
        - **it requires additional service and coding**

<br>

- **data duplication is advised** :arrow_right: in other scenarios other approaches can be better

- Edge case #2:
    - retrieve list of all the orders in the system
        - it can be a problem if the data is big and one request can't retrieve all the data


<br>

- services are not designed for this scenario
- find out what's the purpose of this query
    - reports :arrow_right: use report engine
- report engine is the preferred mechanism for this

### Corss-Cutting Services

- services that provide system-wide utilities
- common examples:
    - logging
    - caching
    - user management
- must be part of the mapping

## Defining Communication Patterns

- efficient communication between services is crucial
- it is important to choose the correct communication pattern
- main patterns:
    - 1-to-1 Sync
    - 1-to-1 Async
    - Pub-Sub / Event Driven

#### 1-to-1 Sync

- a service calls another service and wait for the response
    - synchronous request, the service makes a call to another service and waits for the response
- used mainly when the first service needs the response to continue processing
- for example: order service asks the invetory service if there is an item in stock? It is important for submitting an order.

##### Pros

- immediate response
- error handling simple
- easy to implement

##### Cons

- performance :arrow_right: calling service is blocked 

<br>

- **direct connection communication is not the recommended way for microservices**

#### Service Discovery

- yellow pages
- services only need to know the Directory's URL
- for example: Consul
- this is easy to implement
- CHECK

#### Gateway

- first the service call goes to the gateway and then the gateway directs the request to the other service
- services only need to know the Gateway's URL
- this can provide more services:
    - monitoring
    - authorization
    - authentication

### 1-to1 Async

- a service calls another service and continues working
- doesn't wait for response - Fire and Forget
- used mainly when the first service wants to pass a message to the other service
- for example: order service notifies the payments service

##### Pros

- performance


##### Cons

- needs more setup
- difficult error handling

<br>

- RabbitMQ for messaging for the implementation
- directly sends the message to one service

### Pub-Subv / Event Driven

- a service wants to notify other services about something
- the service has no idea how many services listen
- doesn't wait for response - Fire and Forget
- used mainly when the first service wants to notify about an important event in the system
- for example:
    - order cancelled case, the inventory should be set back to its initial state, payments should be reverted and the customer should be maybe deleted

##### Pros

- peformance
- notify multiple services at once

##### Cons

- needs more setup
- difficult error handling
- might cause load

<br>

- RabbitMQ can be a good solution to handle this

### Summary

- choosing the correct communication pattern is crucial
- affects:
    - performance
    - error handling
    - flow
- almost impossible to reverse

## Selecting Technology Stack

- the decentralized governance allows selecting different technology stack for each service
- make it a concrete decision based on hard evidence

### Development Platform

- .NET :arrow_right: this is the only one that is not cross platform
- .NET Core
- Java
- node.js
- PHP
- Python

<br>

- Web API support is important
- type system:
    - static: hard coded types, compiler
        - errors are found in development 
    - dynamic: whatever type of value
        - faster development

<br>

- .NET Core and node.js are recommended most of the time

### Data Store

- 4 types of data store:
    - relational database
    - NoSQL database
    - cache
    - object store

##### Relational Database

- stores data in tables
- tables have concrete set of columns
- popular databases:
    - SQL Server
    - MySQL
    - PostgreSQL
- data is fully structured

##### NoSQL Database

- emphasis on scale and performance
- schema-less
- data usually stored in JSON format
- popular databases:
    - mongoDB
    - amazon DynamoDB
    - Couchbase
    - Azure Cosmos DB
- semi-structured data
- usually stored for logs and telemetry data

##### Cache

- stores in-memory data for fast access
- distributes data across nodes
- uses proprietary protocol
- stores serializable objects
- popular cache:
    - Redis

##### Object Store

- stores un-structured, large data
    - documents
    - photos
    - files
- popular stores:
    - Microsoft Azure Blob Storage
    - amazon S3
    - Minio

## Design the architecture

- service's architecture is no different from regular software
- based on the layers paradigm

### Layers

- represent horizontal functionality
    - expose user interface / API :arrow_right: US/ SI
        - expose API
        - JSON handling
        - Auth
    - execute logic :arrow_right: Business Logic (BL)
        - validation
        - enrichment
        - computations
    - save / retrieve data :arrow_right: Data Access Layer (DAL)
        - connection handling
        - querying / saving data
        - transaction handling

##### Purpose of Layers

- forces well formed and focused code
- modular

##### Concepts of Lyaers

- Code Flow
    - UI :arrow_right: BL :arrow_right: DAL
    - a layer can't access the layer above it

# Deploying Microservices

- deployment of microservices is extremely important
- slow and complicated deployment will render the whole system ineffective and useless
- architect should be aware of deployment, not responsible

## CI/CD

- Continous Integration / Continuous Delivery
- the full automation of the integration and delivery stages

### Integraion and Delivery

- build, unit tests and integration test all together are called ``Integration``
    - code is built and tested here
- staging, production is called together the ``Delivery / Deployment``

##### Why use CI/CD?

- faster release cycle
- reliability
- reporting

### CI/CD Pipelines

- the heart of the CI/CD process
- define the set of actions to perform as part of the CI/CD
- usually defined using YAML, with UI representation

<br>

- as the architect:
    - make sure there is a CI/CD engine in place
    - help shape the steps in the pipeline

## Containers

- traditional deployment:   
    - code was copiued and built on the production server
    - problems were found on the servers that weren't found in the dev machines

- thin packaging model
- packages software its dependencies and config files
- can be copied between machines
- uses the underlying operating system

### Container vs VM

- with VMs we have the infrastructure which is the hardware and the host operating system
- there is the hypervior as well
- virtual machines are there

<br>

- with containers we have the infrastructure which is mainly the hardware
- the host operating system
- the container runtime
- containers are extermely lightweight
- the containers have the same operating system as the host

### Why containers?


- ``predictability``
    - the same package is deployed from the dev machine to the test to prod
- ``performance``
    - container goes up in seconds vs minutes in VM
- ``density``
    - one server can run thousands of containers vs dozens of VMs

### Why not containers?

- ``isolation``
    - containers share the same OS, so isolation is lighter than VM


## Introduction to Docker

- the most popular container environment
- de-facto standard for containers
- released in 2013

### Docker server - daemon

- service that runs on the server and responsible for managing the docker containers, it tells them on or off
- it keeps tab of the activity
- it builds containers based on images
- it exposes API for management tools
- heart of the docker environment

### Images

- image is the set of definitions in software for a container to run
- images are the building blocks of the containers
- images are static files and they don't run
- they are the basis for the containers but they themselves just lie on the disk and waiting to be called

### Container registry

- basically a collection of images from where you can pull the image you want and either use it as is or customize it to your needs
- container registries can be public :arrow_right: docker hub
    - or they can be private 

### Container

- a container is an image that is built and run
- the container runs in a sandbox created and managed by the docker daemon and is a living breathing instance of the image
- the container is a full-blown process and can do whatever it wants, assuming it has permissions
- it is a piece of software that runs on the machine, isolated from the host but can use its resources

### Client

- CLI command line interface, where you can send instructions to the daemon
- this is the gateway to the whole functionality of docker and using it you can pull images, customize them, run the containers

### Dockerfile

- contains instructions for building custom images
- quite small

### Support for Docker

- supported by all major operating systems
- supported by major cloud providers
    - Amazon ECR
    - Azure ACR


## Containers Management

- containers are a great deployment mechanism
- gain popularity
- what happens when there is too many of them?
- major problems:
    - deployment
    - scalability
    - monitoring
    - routing
    - high availability
- VMs have the same problems
    - load balancers can be a solution

## Kubernetes

- the most popular container management platform
- de-facto standard for container management
- release by Google in 2014
- provides all aspects of management:
    - routing
    - scaling
    - high-availability
    - automated deployment
    - configuration management
    - and more

### Kubernetes architecture

#### Pod

- the atomic unit in Kubernetes and it is the one Kubernetes manages
- you can think of pod as a container of containers
    - the docker container lives inside a pod and the pod functions as a wrapper around it, provides connectivity and monitoring
- usually there is only one docker container inside one pod
- the pod exposes an IP address which is how the Kubernetes communicates with the container
- the containers are accessible for the public network using service
- service is a mechanism used by Kubernetes to expose functionality to the outside world and it masks the inner containers
- the service provides not just an IP, but load balancing, monitoring, high availability and more

# Testing Microservices

- testing is important in all systems and all architecture types
- with microservices it's even more important
- testing microservices poses additional challenges

### Tests Types

- unit tests
- integration tests
- end-to-end tests

## Challenges with microservices testing

- testing state across services
- microservices systems have a lot of moving parts
- testing and tracing all the services is not trivial

## Unit tests

- tests individual code units
    - method, interface etc.
- in-process only
- usually automated
- developed by the developers

### Unit tests in microservices

- no different than usual unit tests
- test only in-process code
- use the same frameworks and methodologies

## Integration Tests

- test the service's functionality
- cover (almost) all code paths in the service
- some paths might include accessing external objects
    - database, other services
- use the service's API
- developed and conducted by the QA team
- should be automated
- most unit testing frameworks support integration test

#### Test Double

- pretends to be the real object / service to allow testing
- three types:
    - Fake
    - Stub
    - Mock

<br>

##### Fake

- implements a shortcut to the external service
- for example - stores data in-memory
- many times implemented in-process
- requires code change in the code

##### Stub

- holds hard-coded data
- usually replaces data stored in a DB
- allows simulating data services quickly
- no code change required

##### Mock

- verifies access was made
- holds no data
- no code change required


## End-to-end tests

- test the whole flow(s) of the system
- touch all services
- test for end state
- extermely fragile
- require code 
- usually used for main scenarios only
    - edge scenarios should be tested with integration tests

## Testing microservices - summary

- extermely important
- focus on the integration tests
- as an architect
    - make sure there is a test automation framework in place
    - be involved in the test results analysis, may require architecture changes

# <ins>Service Mesh</ins>

- manages all service-to-service communication
- provides additional services
- platform agnostic (usually)

## Problems Solved by Service Mesh

- microservices communicate between them a lot
- the communication might cause a lot of problems and challenges:
    - timeouts
    - security
    - retries
    - monitoring

<br>

- software components that sit near the service and manage all service-to-service communication
- provides all communication services
- the service interacts with the service mesh only

### Service Mesh Services

- protocol conversion
- communication security
- authentication
- reliability (timeouts, retries, health checks, circuit breaking)
- monitoring
- service discovery
- testing (A/B testing, traffic splitting)
- load balancing

#### Circuit Breaker

- prevents cascading failures when a service fails
- it is in front of the service
- monitors the service
- the circuit breaker sends response to a service which called the service that is behind the circuit breaker so the caller service won't wait for the service to timeout


## Service Mesh Architecture

- ``data plane``: the components that actually does all the heavy lifting
    - converts protocols, handles security, implements the circuit breaker, retries timeout handling etc.
- on top of the data plane is the ``control plane``:
    - controls and manages the various data planes
    - configures managers and monitors the data planes and makes sure they work according to the actual needs
    - defines what kind of security is needed or the protocols required for this application
    - controls planes can communicate with different data planes
    - mainly still the data and controls planes are bundled together
- **data planes and control planes are the main building blocks or service mesh**

## Types of Service Mesh

### In-Process

- service mesh is implemented as a software components so it is part of the services process itself
- so when one service calls the other one basically one service mesh will call the other one so they do a network call
- no inter-process communication is required to use it


### Sidecar

- service mesh is implemented as an out of process component and is not part of the services process
- so when a service wants to communicate with another service, first it makes a network call to the mesh componenets that belongs to it :arrow_right: the mesh component makes another call to the mesh component of the called service :arrow_right: this component then calls the service we want to talk to
- the mesh component is located near the service

### In-Process vc Sidecar

#### In-Process

- performance :arrow_right: no need to call the service mesh with a network call as it is part of the process


#### Sidecar :arrow_right: MORE POPULAR

- platform agnostic :arrow_right: service mesh is outside of the process
- code agnostic :arrow_right: an API call is made so it doesn't matter what technology was used to build the service or the service mesh

## Products and Implementations

- quite a few Service Mesh implementations
- some in-process, most sidecar
- most free, some aren't
- DO NOT develop your own

#### Sidecar

- Istio
    - most popular one
    - designed to work with containers managed by Kubernetes
- Linkerd
- Maesh

#### In-Process

- DDS
    - great performance
    - very popular in the military industry
    - it is not free

## Should you use Service Mesh?

- only if:
    - you have a lot of services
    - which communicate a lot with each other
    - or you have a complex communication requirement with various protocols or brittle network


# Logging and Monitoring

## Introduction

### Logging and Monitoring

- extremely important in microservices
- flow goes through multiple processes
- hard to get wholistic view
- hard to know what's going on with the services

## Logging vs Monitoring

#### Logging

- recording the system's activity
- audit
- documenting errors

#### Monitoring

- based on system's metrics
    - CPU, memory usage and so on
- alerting when needed

## Implementing Logging

- logging should provide wholistic view on the system
- should allow tracing end-to-end flow
- should contain as much information as possible
    - time stamp, severity and so on
- can be filtered using severity, module, time etc.

#### Traditional logging

- when we have 2 separate services they use their own logging service
- they log into their own repository

##### Problems of traditional logging in microservices

- ``separate`` :arrow_right: the logs are separated from each other on the different services
- ``different formats`` :arrow_right: using different logging libraries it can be a problem how the information is stored, maybe it is stored in JSON format or raw text :arrow_right: going through the logs will be hard and slow provess
- ``not aggregated`` :arrow_right: we can't have aggregated logs for example how many errors we had 
- ``can't be analyzed`` :arrow_right: not stored in a central place


#### Microservices

- we have 2 services **and another one which is responsible for logging**
- when the services want to log something they will write it to the logging service as it is the central place
- advantages:
    - logs are unified and stored in the same location
    - aggregated
    - can be analyzed

### Logging Library

- better use one library for all the services
    - Winston (nodeJS), Serilog (.NET Core)
- if using various platforms - one library for each platform
- use severity wisely
    - ``debug``: only useful for the developers, used during debugging
    - ``info``: to log events we should be aware of but not a reason for concern. For example: system startup 
    - ``warning``: indicates there is some kind of problem, but not something we should really worry about. We need to keep an eye on it.
    - ``error`` and ``critical``: showing that the system is about to go down. Something really severe happened. 
- log as much info as possible at least: 
    - timestamp
    - user
    - severity
    - service
    - message
    - stack trace (if error)
    - correlation ID

### Correlation ID

- a flow identifier
- correlates events between services
- enables stitching separate events to a single flow
- it should be unique in the system

### Transport

- preferably queue
- balances the load
- no perforamnce hit on the client side
- usually RabbitMQ/Kafka

### Logging Service

- preferably based on indexing / digesting / search product
- can index any log format
- provides great visualization
- no development required
- ELK Stack / Splunk

## Implementing Monitoring

- monitoring looks at metrics and detects anomalies
- provides simplified view of the system status
- alerts when there is a problem

### Types of Monitoring

#### Infrastructure

- monitors the server
- CPU/ RAM / Disk / Network
- alerts when infrastructure problem is detected
- data source : agent on the machine

#### Application

- monitors the application
- looks at metrics published by the app
    - Requests / min, Orders / day etc.
- alerts when application problem is detected
- data source: application's logs,event log

### Most monitoring products provide both!

### Monitoring products

- do not develop your own
- Nagios / ELK Stack :arrow_right: on premise application
-  New Relic / Application Insights :arrow_right: cloud-based tools

# When not to use microservices

- microservice are not onze-size-fits-all
- there are cases where they shouldn't be used
- might even cause damage
- need to evaluate on a case-by-case basis

## Small systems

- small systems with low complexity should usually be a monolith
- microservices add complexity
- if the service mapping results in 2-3 services - microservices are probably not the right option

## Intermingled Functionality or Data

- one of the most important microservice's attributes is its autonomy
- when there is no way to separate logic or data - microservices will not help
- if almost all requests for data span more than one service - there's a problem

## Performance Sensitive Systems

- microservices systems have performance overhead
- result of the network hops
- if the system is VERY performance sensitive - think twice
    - SLA is in the low-milliseconds or even microseconds

## Quick-and-Dirty Systems

- microservices design and implementation takes time
- if you need a small quick systems and need it NOW - don't go with microservices
- usually has a short lifespan

## No Planned Updates

- some systems have almost no planned future updates
- for example - embedded systems
- microservices' main strength is in the short update cycle
- no updates == no microservices

# Microservices and the Organization

- microservices require different mindset
- traditional organizations will have hard time succeeding with microservices
- without adapting - there is no point in going with microservices

## Conway's Law

- still relevant
- describes the relationship between the organization and the software structure / architecture
- **"Any organization that designs a system (defined broadly) will produce a design whose structure is a copy ot the organization's communication structure."**

#### Traditional architecture

- Frontend - Backend - DB - IT Services
    - if you think about this usually according to this structure there are 4 teams as well

## The problem with traditional team

- products not projects what we want in microservices
- when there are multiple teams - no one takes responsibility
- teams are horizontal - Backend, Frontend, IT etc.
- no wholistic view on the product


## The ideal team

- the ideal teams is responsible for all aspects of the service:
    - backend
    - frontend
    - DB
    - deployment
- with this in mind as the team is responsible for everything we eliminate inter-team communication

### The ideal team size

- **"Every internal team should be small enough that it can be fed with 2 pizzas."** - Jeff Bezos

- exact number varies
- should be small (usually 3-7)

## Changing Mindset

- traditional organizations have hard time transitioning to microservices
- need help in the process
- you can and should help

- How to help?
    - training - lecture on microservices, success stories, basic principles
    - POC - Go small, quick win
    - work closely with the team during design and development

# Anti-Patterns and Common Mistakes

- microservices require thorough design
- they are not "fire and forget"
- it is easy to make mistakes that will cause the project to fail

## No well-defined services

- map the components
    - split to:
        - mapping
        - communication patterns

- negligent mapping results in bloated services
- dependent functionality gets added continuously
    - and creates a mini-monolith



### Mapping the components

- the single most important step in the whole process
- determines how the system will look like in the long run
- once set - not easy to change

## No well-defined API

- API is the door to the service
- should be well thought of and easy to learn
- MUST be consistent
- MUST be versioned
- MUST be platform agnostic
    - use only serializable types
- MUST be part of the design

## Implement Cross-Cutting Last

- every system has cross-curring (system-wide) services
    - logging
    - caching
    - users managemenet
    - authorization and authentication
    - and more

- should be implemented first
- other services are going to use them
- no one likes to go back and modify existing code

### Cross-Cutting Services MUST BE DEVELOPED FIRST!

#### Cross Cutting Concerns

- first we implement the cross-cutting services
    - logging
    - caching
- then we develop the business related services that use the cross-cutting services as well

## Expanding Service Boundaries

- every service has well-defined boundaries
- expanding these boundaries makes the service inefficient and bloated
- it's tempting - don't do that!
- many times new service should be used instead of expanding existings service's boundaries

# Breaking Monolith to Microservices

- quite common scenario
- the organization wants to improve the current system
- needs to be thoroughly planned
- high rate of failures

## Motivation for Breaking Monolith

- shorten update cycle
- modularize the system
- save costs
    - software and hardware costs
    - HR costs
        - large bloated teams, with microservices not a lot of people is needed
- modernize the system
- being attractive

## Strategies for Breaking Monolith

- breaking monolith is a delicate process
- muse be planned ahead
- there are 3 main strategies for that: 
    - new modules as services
    - separate existing modules to services
    - complete rewrite

## New Modules as Services

- we do not modify existing code but we add new services
- so basically we leave the monolith alone, only modify it to be able to communicate with our new standalone service


#### Pros 

- easy to implement
- minimum code change in the monolith

#### Cons

- takes time
- end result is not pure microservices architecture

## Separate Existing Modules to Services

- we will handle each component of the system separately and convert it from a library to a service
- we will go through each component and one-by-one we put it out to a service

#### Pros

- end result is pure microservices architecture

#### Cons

- takes time
- a lot of code changes
- regression testing required

## Complete Rewrite

- dump everything you have and develop it from scratch
- this strategy is used when the other 2 can't be an option
- we need to add web api to all of the services

#### Pros

- end result is pure microservices architecture
- opportunity for modernization

#### Cons

- takes time
- rigorous testing required

<br>

- the more complex the system is the more likely that it needs a full rewrite
