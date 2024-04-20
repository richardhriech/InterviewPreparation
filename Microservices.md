- Software architectural style
- set of small, independent services that communicate with each other through **APIs**
- monolithic aplications are ineffective - scaling such applications is expensive since we have to scale the whole even though only a particular service gets a lot of traffic
- microservices can be built using different technologies and **deployed, scaled**, updated independently
- they have their own independent **databases**
- ![[Microservice Using ASP.webp]]
- dockerized microservice: https://www.c-sharpcorner.com/article/microservice-using-asp-net-core/

## Principles of Microservices
1. Modelled around business domain: each domain focuses on one thing and its associated logic
	- can migrate easily to next version
	- scale independently
2. Culture of Automation: there is an increase in the number of deployment units compared to monolithic architecture -> the need for **continuous integration and continuous delivery**.
3. Hide Implementation Details: reduce coupling
4. Decentralization: each service to manage their own database
5. Deploy Independently
6. Failure Isolation
7.  Highly Observable: logging events and stats