Spring Web
---

## DispatcherServlet

`DispatcherServlet` acts as front controller for Spring based web applications. It provides a mechanism for request processing where actual work is performed by configurable, delegate components. It is inherited from `javax.servlet.http.HttpServlet`.

A web application can define any number of `DispatcherServlet` instances. Each servlet will operate in its own namespace, loading its own application context with mappings, handlers, etc. Only the root application context as loaded by `ContextLoaderListener`, if any, will be shared. In most cases, applications have only single `DispatcherServlet` with the context-root URL`(/)`, that is, all requests coming to that domain will be handled by it.

`DispatcherServlet` uses Spring configuration classes to discover the delegate components it needs for request mapping, view resolution, exception handling etc.

---

## WebApplicationContext

In a Spring-based application, our application objects live within an object container. This container creates objects and associations between objects, and manages their complete life cycle. These container objects are called Spring-managed beans (or simply beans), and the container is called an application context (via class `ApplicationContext`) in the Spring world.

`WebApplicationContext` is an extension of a plain `ApplicationContext`. it is web aware `ApplicationContext` i.e it has Servlet Context information. When `DispatcherServlet` is loaded, it looks for the bean configuration file of `WebApplicationContext` and initializes it.

---
