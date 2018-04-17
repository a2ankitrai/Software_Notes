# Spring Boot Actuator
---

Actuator brings production-ready features to our application.

**Monitoring our app, gathering metrics, understanding traffic or the state of our database becomes trivial with this dependency.**

The main benefit of this library is that we can get production grade tools without having to actually implement these features ourselves.

Actuator is mainly used to **expose operational information about the running application** – health, metrics, info, dump, env, etc. It uses HTTP endpoints or JMX beans to enable us to interact with it.

**spring-boot-actuator dependency**

```xml

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

## Spring Boot 2.x Actuator


In 2.x Actuator keeps its fundamental intent, but simplifies its model, extends its capabilities and incorporate better defaults.

Firstly, this version becomes technology agnostic. Also, it simplifies its security model by merging it with the application one.

Lastly, among the various changes, it’s important to keep in mind that some of them are breaking. This includes HTTP request/responses as well as Java APIs.

Furthermore, the latest version supports now the CRUD model, as opposed to the old RW (read/write) model.


### Technology Support

With its second major version, Actuator is now technology-agnostic whereas in 1.x it was tied to MVC, therefore to the Servlet API.

In 2.x Actuator defines its model, pluggable and extensible without relying on MVC for this.

Hence, with this new model, we’re able to take advantage of MVC as well as WebFlux as an underlying web technology.

Moreover, forthcoming technologies could be added by implementing the right adapters.

Lastly, JMX remains supported to expose endpoints without any additional code.

---

## Endpoints

### Audit Events (auditevents)

The `auditevents ` endpoint provides information about the application’s audit events.

To retrieve the audit events, make a GET request to `/actuator/auditevents`

https://docs.spring.io/spring-boot/docs/2.0.x/actuator-api/html/#overview-auditevents


### Beans (beans)

The beans endpoint provides information about the application’s beans.

To retrieve the beans, make a GET request to `/actuator/beans`




























