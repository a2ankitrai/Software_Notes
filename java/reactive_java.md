Reactive Java
---

Reactive programming is defined by the following principle:

> Any “getter” for mutable state causes problems. Instead of using getters, any calculated, generated, loaded or received state values should be immediately sent into a channel and any part of the program that wants access to these values must subscribe to the channel.

The idea is that we remove state from exposed parts of our program and encapsulate it inside channels instead. Channels clearly show data dependencies and effects, make changes easy to reason about and easy to maintain and otherwise simplify how we modify application state.

Simply put: reactive programming manages asynchronous data flows between sources of data and components that need to react to that data.



---

Reactive Programming is a new paradigm in which you use declarative code (in a manner that is similar to functional programming) in order to build asynchronous processing pipelines. It is an event-based model where data is pushed to the consumer, as it becomes available: we deal with asynchronous sequences of events.

This is important in order to be more efficient with resources and increase an application's capacity to serve large number of clients, without the headache of writing low-level concurrent or and/or parallelized code.

By being built around the core pillars of being fully **asynchronous** and **non-blocking**, Reactive Programming is an alternative to the more limited ways of doing asynchronous code in the JDK: namely `Callback` based APIs and `Future`.

It also facilitates composition, which in turn makes asynchronous code more readable and maintainable.

---

# Reactive Streams

The **Reactive Streams** specification is an industry-driven effort to standardize Reactive Programming libraries on the JVM, and more importantly specify how they must behave so that they are interoperable. Implementors include Reactor 3 but also RxJava 2, Akka Streams, Vert.x and Ratpack. Reactive Streams have been incorporated into the JDK as java.util.concurrent.Flow in version 9.

It contains 4 very simple interfaces as well as a TCK, which shouldn't be overlooked since it is the rules of the specification that bring the most value to it.

From a user perspective however, it is fairly low-level. Reactor 3  and other libraries aims at offering an higher level API that can be leverage in a large breadth of situations, building it on top of Reactive Streams `Publisher`.

---

Java is not a "reactive language" in the sense that it doesn’t support coroutines natively. There are other languages on the JVM (Scala and Clojure) that support reactive models more natively, but Java itself does not until version 9. Java, however, is a powerhouse of enterprise development, and there has been a lot of activity recently in providing Reactive layers on top of the JDK. 

**Reactive Streams** is a very low level contract, expressed as a handful of Java interfaces (plus a TCK), but also applicable to other languages. The interfaces express the basic building blocks of Publisher and Subscriber with explicit back pressure, forming a common language for interoperable libraries. Reactive Streams have been incorporated into the JDK as java.util.concurrent.Flow in version 9. The project is a collaboration between engineers from Kaazing, Netflix, Pivotal, Red Hat, Twitter, Typesafe and many others.

**RxJava**: Netflix were using reactive patterns internally for some time and then they released the tools they were using under an open source license as Netflix/RxJava (subsequently re-branded as "ReactiveX/RxJava"). Netflix does a lot of programming in Groovy on top of RxJava, but it is open to Java usage and quite well suited to Java 8 through the use of Lambdas. There is a bridge to Reactive Streams. RxJava is a "2nd Generation" library according to David Karnok’s Generations of Reactive classification.

**Reactor** is a Java framework from the Pivotal open source team (the one that created Spring). It builds directly on Reactive Streams, so there is no need for a bridge. The Reactor IO project provides wrappers around low-level network runtimes like Netty and Aeron. Reactor is a "4th Generation" library according to David Karnok’s Generations of Reactive classification.

**Spring Framework 5.0** (first milestone June 2016) has reactive features built into it, including tools for building HTTP servers and clients. Existing users of Spring in the web tier will find a very familiar programming model using annotations to decorate controller methods to handle HTTP requests, for the most part handing off the dispatching of reactive requests and back pressure concerns to the framework. Spring builds on Reactor, but also exposes APIs that allow its features to be expressed using a choice of libraries (e.g. Reactor or RxJava). Users can choose from Tomcat, Jetty, Netty (via Reactor IO) and Undertow for the server side network stack.

**Ratpack** is a set of libraries for building high performance services over HTTP. It builds on Netty and implements Reactive Streams for interoperability (so you can use other Reactive Streams implementations higher up the stack, for instance). Spring is supported as a native component, and can be used to provide dependency injection using some simple utility classes. There is also some autoconfiguration so that Spring Boot users can embed Ratpack inside a Spring application, bringing up an HTTP endpoint and listening there instead of using one of the embedded servers supplied directly by Spring Boot.

**Akka** is a toolkit for building applications using the Actor pattern in Scala or Java, with interprocess communication using Akka Streams, and Reactive Streams contracts are built in. Akka is a "3rd Generation" library according to David Karnok’s Generations of Reactive classification.


