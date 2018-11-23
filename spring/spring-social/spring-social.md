# Spring - social

Spring Social project enables your applications to establish Connections with Software-as-a-Service (SaaS) Providers such as Facebook and Twitter to invoke APIs on behalf of Users.

Social integration is a three-way conversation between a service provider, a service consumer, and a user who holds an account on both the provider and consumer. All interactions between the consumer and the service provider are scoped to the context of the user's profile on the service provider.

With Spring Social, your application can play the part of the service consumer, interacting with a service provider on behalf of its users. The key features of Spring Social are:

- A **Connect Framework** that handles the core authorization and connection flow with service providers.

- A **Connect Controller** that handles the OAuth exchange between a service provider, consumer, and user in a web application environment.

- A **Signin Controller** that allows users to authenticate with your application by signing in with their Provider accounts, such as their Twitter or Facebook accounts.

---

## Spring Social Modules

- `spring-social-core`	Spring Social's Connect Framework and OAuth client support. (Required)

- `spring-social-web`	Spring Social's ConnectController which uses the Connect Framework to manage connections in a web application environment.

- `spring-social-test`	Support for testing Connect implementations and API bindings.


To let Spring Social handle the back-and-forth authorization handshake between your web application and a service provider, you'll need the web module:

```xml
<dependency>
    <groupId>org.springframework.social</groupId>
    <artifactId>spring-social-web</artifactId>
    <version>${spring-social.version}</version>
</dependency>
```

If you're developing your own client module (Chapter 3, Adding Support for a New Service Provider) and API binding, you'll need the test module to test it:

```xml
<dependency>
    <groupId>org.springframework.social</groupId>
    <artifactId>spring-social-test</artifactId>
    <version>${spring-social.version}</version>
</dependency>
```













----
