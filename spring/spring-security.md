# Spring Security

Spring Security provides comprehensive security services for Java EE-based enterprise software applications.

Two major areas of application security are **authentication** and **authorization** (or **access-control**). These are the two main areas that Spring Security targets. **Authentication** is the process of establishing a principal is who they claim to be (a **principal** generally means a user, device or some other system which can perform an action in your application).**Authorization** refers to the process of deciding whether a principal is allowed to perform an action within your application. To arrive at the point where an authorization decision is needed, the identity of the principal has already been established by the authentication process. 

At an authentication level, Spring Security supports a wide range of authentication models. Most of these authentication models are either provided by third parties, or are developed by relevant standards bodies such as the Internet Engineering Task Force. Specifically, Spring Security currently supports authentication integration with all of these technologies:

- HTTP BASIC authentication headers (an IETF RFC-based standard)
- HTTP Digest authentication headers (an IETF RFC-based standard)
- HTTP X.509 client certificate exchange (an IETF RFC-based standard)
- LDAP (a very common approach to cross-platform authentication needs, especially in large environments)
- Form-based authentication (for simple user interface needs)
- OpenID authentication
- Authentication based on pre-established request headers (such as Computer Associates Siteminder)
- Jasig Central Authentication Service (otherwise known as CAS, which is a popular open source single sign-on system)
- Transparent authentication context propagation for Remote Method Invocation (RMI) and HttpInvoker (a Spring remoting protocol)
- Automatic "remember-me" authentication (so you can tick a box to avoid re-authentication for a predetermined period of time)
- Anonymous authentication (allowing every unauthenticated call to automatically assume a particular security identity)
- Run-as authentication (which is useful if one call should proceed with a different security identity)
- Java Authentication and Authorization Service (JAAS)
- Java EE container authentication (so you can still use Container Managed Authentication if desired)
- Kerberos
- Java Open Source Single Sign-On (JOSSO) *
- OpenNMS Network Management Platform *
- AppFuse *
- AndroMDA *
- Mule ESB *
- Direct Web Request (DWR) *
- Grails *
- Tapestry *
- JTrac *
- Jasypt *
- Roller *
- Elastic Path *
- Atlassian Crowd *

(* Denotes provided by a third party)



Irrespective of the authentication mechanism, Spring Security provides a deep set of authorization capabilities. There are three main areas of interest: authorizing web requests, authorizing whether methods can be invoked and authorizing access to individual domain object instances. 

---

# Release Numbering

It is useful to understand how Spring Security release numbers work, as it will help you identify the effort (or lack thereof) involved in migrating to future releases of the project. Each release uses a standard triplet of integers: `MAJOR.MINOR.PATCH`. The intent is that `MAJOR` versions are incompatible, large-scale upgrades of the API. `MINOR` versions should largely retain source and binary compatibility with older minor versions, thought there may be some design changes and incompatible updates. `PATCH` level should be perfectly compatible, forwards and backwards, with the possible exception of changes which are to fix bugs and defects.

The extent to which you are affected by changes will depend on how tightly integrated your code is. If you are doing a lot of customization you are more likely to be affected than if you are using a simple namespace configuration. 

--- 

# Getting Spring Security

## Usage with Maven

pom.xml. 

```xml

<dependencies>
<!-- ... other dependency elements ... -->
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-web</artifactId>
	<version>5.0.4.RELEASE</version>
</dependency>
<dependency>
	<groupId>org.springframework.security</groupId>
	<artifactId>spring-security-config</artifactId>
	<version>5.0.4.RELEASE</version>
</dependency>
</dependencies>
```

## Gradle

build.gradle. 

```
dependencies {
	compile 'org.springframework.security:spring-security-web:5.0.4.RELEASE'
	compile 'org.springframework.security:spring-security-config:5.0.4.RELEASE'
}
```

--- 

# Project Modules

The codebase has been sub-divided into separate jars which more clearly separate different functionality areas and third-party dependencies.

- **Core - spring-security-core.jar** : Contains core authentication and access-contol classes and interfaces, remoting support and basic provisioning APIs. Required by any application which uses Spring Security. Supports standalone applications, remote clients, method (service layer) security and JDBC user provisioning. Contains the top-level packages:
	
	- `org.springframework.security.core`
	- `org.springframework.security.access`
	- `org.springframework.security.authentication`
	- `org.springframework.security.provisioning`

- **Remoting - spring-security-remoting.jar** : Provides intergration with Spring Remoting. 

- **Web - spring-security-web.jar** : Contains filters and related web-security infrastructure code. Anything with a servlet API dependency. You’ll need it if you require Spring Security web authentication services and URL-based access-control. The main package is `org.springframework.security.web`.

- **Config - spring-security-config.jar** : Contains the security namespace parsing code & Java configuration code. You need it if you are using the Spring Security XML namespace for configuration or Spring Security’s Java Configuration support. The main package is `org.springframework.security.config`. None of the classes are intended for direct use in an application.

- **LDAP - spring-security-ldap.jar** : LDAP authentication and provisioning code. Required if you need to use LDAP authentication or manage LDAP user entries. The top-level package is `org.springframework.security.ldap`.

- **OAuth 2.0 Core - spring-security-oauth2-core.jar** : `spring-security-oauth2-core.jar` contains core classes and interfaces that provide support for the *OAuth 2.0 Authorization Framework* and for *OpenID Connect Core 1.0*. It is required by applications that use *OAuth 2.0* or *OpenID Connect Core 1.0*, such as Client, Resource Server, and Authorization Server. The top-level package is `org.springframework.security.oauth2.core`.

- **OAuth 2.0 Client - spring-security-oauth2-client.jar** : `spring-security-oauth2-client.jar` is Spring Security’s client support for OAuth 2.0 Authorization Framework and OpenID Connect Core 1.0. Required by applications leveraging **OAuth 2.0 Login** and/or OAuth Client support. The top-level package is `org.springframework.security.oauth2.client`.

- **OAuth 2.0 JOSE - spring-security-oauth2-jose.jar** : `spring-security-oauth2-jose.jar` contains Spring Security’s support for the JOSE (Javascript Object Signing and Encryption) framework. The JOSE framework is intended to provide a method to securely transfer claims between parties. It is built from a collection of specifications:

	- JSON Web Token (JWT)
	- JSON Web Signature (JWS)
	- JSON Web Encryption (JWE)
	- JSON Web Key (JWK)

- **ACL - spring-security-acl.jar** : Specialized domain object ACL implementation. Used to apply security to specific domain object instances within your application. The top-level package is `org.springframework.security.acls`.

- **CAS - spring-security-cas.jar** : Spring Security’s CAS client integration. If you want to use Spring Security web authentication with a CAS single sign-on server. The top-level package is `org.springframework.security.cas`.

- **OpenID - spring-security-openid.jar** : OpenID web authentication support. Used to authenticate users against an external OpenID server. `org.springframework.security.openid`. Requires OpenID4Java.

- **Test - spring-security-test.jar** : Support for testing with Spring Security.

---









































