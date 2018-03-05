MicroServices
---

Essentially, microservice architecture is a method of developing software applications as a suite of independently deployable, small, modular services in which each service runs a unique process and communicates through a well-defined, lightweight mechanism to serve a business goal.

How the services communicate with each other depends on your application’s requirements, but many developers use HTTP/REST with JSON or Protobuf.  DevOps professionals are, of course, free to choose any communication protocol they deem suitable, but in most situations, REST (Representational State Transfer) is a useful integration method because of its comparatively lower complexity over other protocols.

## SOA vs. Microservices

 SOA also focuses on imperative programming, whereas microservices architecture focuses on a responsive-actor programming style.  Moreover, SOA models tend to have an outsized relational database, while microservices frequently use NoSQL or micro-SQL databases (which can be connected to conventional databases).  But the real difference has to do with the architecture methods used to arrive at an integrated set of services in the first place. 

## Understanding Microservice Architecture

Software built as microservices can, by definition, be broken down into multiple component services. Why?  So that each of these services can be deployed, tweaked, and then redeployed independently without compromising the integrity of an application.  As a result, you might only need to change one or more distinct services instead of having to redeploy entire applications.  But this approach does have its downsides, including expensive remote calls (instead of in-process calls), coarser-grained remote APIs, and increased complexity when redistributing responsibilities between components.

The microservices style is usually organized around business capabilities and priorities. Unlike a traditional monolithic development approach—where different teams each have a specific focus on, say, UIs, databases, technology layers, or server-side logic—microservice architecture utilizes cross-functional teams. 

Microservices act somewhat like the classical UNIX system: they receive requests, process them, and generate a response accordingly.  This is opposite to how many other products such as ESBs (Enterprise Service Buses) work, where high-tech systems for message routing, choreography, and applying business rules are utilized. 

Since microservices involve a variety of technologies and platforms, old-school methods of centralized governance aren’t optimal.  Decentralized governance is favored by the microservices community because its developers strive to produce useful tools that can then be used by others to solve the same problems.

Microservices are designed to cope with failure.  Since several unique and diverse services are communicating together, it’s quite possible that a service could fail, for one reason or another (e.g., when the supplier isn’t available).  In these instances, the client should allow its neighboring services to function while it bows out in as graceful a manner as possible. 

## How Microservice Architecture Works

To follow our brief overview of microservices here, it will help to have at least a basic grasp of the following concepts:

- Object Oriented Programming (OOP)— *a modern programming paradigm (see also SOLID)*

- Web service / API— *a way to expose the functionality of your application to others, without a user interface*

- Service Oriented Architecture (SOA)— *a way of structuring many related applications to work together, rather than trying to solve all problems in one application*

- Systems— *in the general sense, meaning any collection of parts that can work together for a wider purpose*

- Single Responsibility Principle (SRP)— *the idea of code with one focus*

- Interface Segregation Principle (ISP)— *the idea of code with defined boundaries.*
