# Keycloak

**Keycloak is an open source Identity and Access Management solution targeted towards modern applications and services.**

Keycloak offers features such as Single-Sign-On (SSO), Identity Brokering and Social Login, User Federation, Client Adapters, an Admin Console, and an Account Management Console.

---

# Installing and Booting

**Download and Install**

Download the keycloak server from [here](https://www.keycloak.org/downloads.html). Unzip the same.

**Booting the Server**

go to the `bin/` directory of the server distribution. To boot the server:

Linux/Unix

```
$ .../bin/standalone.sh
```

Windows
```
> ...\bin\standalone.bat
```

**Creating the Admin Account**

Create the admin on the welcome page.

> Note: You can only create an initial admin user on the Welcome Page if you connect using localhost. This is a security precaution. You can also create the initial admin user at the command line with the `add-user-keycloak.sh`

**Logging in to the Admin Console**

1. Click the Administration Console link. Alternatively you can go to the console URL directly at http://localhost:8080/auth/admin/

2. Type the username and password you created on the Welcome page

---


# Creating a Realm and User

**Creating a New Realm**

Keycloak defines the concept of a realm in which you will define your clients, which in Keycloak terminology means an application that will be secured by Keycloak, it can be a Web App, a Java EE backend, a Spring Boot etc.

In the top left corner dropdown menu that is titled Master in Admin console, click Add Realm. Type any name and click Create.

**Creating a New User**

create a new user in the demo realm created. Also set a temporary password for your new user in the Credentials tab.

**User Account Service**

Log in to the User Account Service of your realm with the user you just created by clicking this link:

*User Account Link*

http://localhost:8080/auth/realms/{{Realm_name}}/account

Type the username and password you created previously.

---

# Securing a java Servlet Application

There is one caveat: you must run a separate WildFly instance on the same machine as the Keycloak server to run your Java servlet application. Run the Keycloak using a different port than the WildFly, to avoid port conflicts.

to run the Keycloak under a different port so that there are no port conflicts when running on the same machine. Use the `jboss.socket.binding.port-offset` system property on the command line. The value of this property is a number that will be added to the base value of every port opened by the Keycloak server.

To boot the Keycloak server:
Linux/Unix

```
$ .../bin/standalone.sh -Djboss.socket.binding.port-offset=100
```

Windows
```
> ...\bin\standalone.bat -Djboss.socket.binding.port-offset=100
```


Further read:

https://www.baeldung.com/spring-boot-keycloak

https://developers.redhat.com/blog/2017/05/25/easily-secure-your-spring-boot-applications-with-keycloak/

https://www.keycloak.org/docs/latest/getting_started/index.html#_create-realm


http://localhost:8180/auth/realms/spring-demo/broker/google/endpoint


----
