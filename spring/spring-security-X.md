# Spring Security X


# Getting Started

Please refer to below GitHub repository to get started on Spring security

[Spring-Security](https://github.com/a2ankitrai/Spring-Shots/tree/master/spring-security)

# Java Configuration

The first step is to create our Spring Security Java Configuration. The configuration creates a Servlet Filter known as the springSecurityFilterChain which is responsible for all the security (protecting the application URLs, validating submitted username and passwords, redirecting to the log in form, etc) within your application. You can find the most basic example of a Spring Security Java Configuration below:

```java

import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.context.annotation.*;
import org.springframework.security.config.annotation.authentication.builders.*;
import org.springframework.security.config.annotation.web.configuration.*;

@EnableWebSecurity
public class WebSecurityConfig implements WebMvcConfigurer {

	@Bean
	public UserDetailsService userDetailsService() throws Exception {
		InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
		manager.createUser(User.withDefaultPasswordEncoder().username("user").password("{noop}password").roles("USER").build());
		return manager;
	}
}

```
---

## Register the `springSecurityFilterChain`

Spring Security provides a base class `AbstractSecurityWebApplicationInitializer` that will ensure the springSecurityFilterChain gets registered. The way in which we use `AbstractSecurityWebApplicationInitializer` differs depending on if we are already using Spring or if Spring Security is the only Spring component in our application.

AbstractSecurityWebApplicationInitializer without Existing Spring - If you are not using Spring or Spring MVC, you will need to pass in the WebSecurityConfig into the superclass to ensure the configuration is picked up.

```java
import org.springframework.security.web.context.*;

public class SecurityWebApplicationInitializer
	extends AbstractSecurityWebApplicationInitializer {

	public SecurityWebApplicationInitializer() {
		super(WebSecurityConfig.class);
	}
}
```

AbstractSecurityWebApplicationInitializer with Spring MVC - If we were using Spring elsewhere in our application we probably already had a WebApplicationInitializer that is loading our Spring Configuration. If we use the previous configuration we would get an error. Instead, we should register Spring Security with the existing ApplicationContext.

```java
import org.springframework.security.web.context.*;

public class SecurityWebApplicationInitializer
	extends AbstractSecurityWebApplicationInitializer {

}
```

## HttpSecurity

The `WebSecurityConfigurerAdapter` provides a default configuration in the configure(HttpSecurity http) method that looks like:

```java
protected void configure(HttpSecurity http) throws Exception {
	http
		.authorizeRequests()
			.anyRequest().authenticated()
			.and()
		.formLogin()
			.and()
		.httpBasic();
}
```

##  Java Configuration and Form Login

To provide custom login page redirection, the configuration can be updated as follows:

```java
protected void configure(HttpSecurity http) throws Exception {
	http
		.authorizeRequests()
			.anyRequest().authenticated()
			.and()
		.formLogin()
			.loginPage("/login")  //The updated configuration specifies the location of the log in page.
			.permitAll(); // 	We must grant all users (i.e. unauthenticated users) access to our log in page.
}
```
---

## Spring JDBC Authentication (httpBasic)

Security Configuration:

```java
import javax.sql.DataSource;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.env.Environment;
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

import com.ank.springjdbcauthentication.repository.UserRepository;
import com.ank.springjdbcauthentication.service.LoginUserDetailService;

@EnableWebSecurity
@Configuration
@EnableJpaRepositories(basePackageClasses = UserRepository.class)
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Bean
    public PasswordEncoder passwordEncoder() {
	     return new BCryptPasswordEncoder();
    }


    @Override
    protected void configure(HttpSecurity http) throws Exception {

    	http

    		.authorizeRequests()

    		.anyRequest().fullyAuthenticated()

    		.and()

    		.httpBasic();
    }

    @Autowired
    LoginUserDetailService loginUserDetailService;

    @Autowired
    public void configure(AuthenticationManagerBuilder auth) throws Exception {

	     auth.userDetailsService(loginUserDetailService).passwordEncoder(passwordEncoder());

    }.
}
```

The Authentication Manager will return an instance of `org.springframework.security.core.userdetails.UserDetails` interface. We have implemented the same in [CustomUser.java](https://github.com/a2ankitrai/Spring-Shots/blob/master/spring-security/spring-jdbc-authentication/src/main/java/com/ank/springjdbcauthentication/model/CustomUser.java).

In this authentication we have used `UserDetailsService` interface implementation to loads user-specific data. This interface contains method `loadUserByUsername` which locates the user based on the username.

> Here, we have used *HttpBasic* for authentication. Basic Authentication wasn't designed to manage logging out. So once the user is logged in, he will remain logged in even after server restarts until he is logged out by invalidating the session.

[Github Repo](https://github.com/a2ankitrai/Spring-Shots/tree/master/spring-security/spring-jdbc-authentication)


---

# Enabling HTTPS in Spring Boot

To enable SSL (https) in a Spring Boot Application take the following steps:

**Get a SSL certificate**

Every Java Runtime Environment (JRE) comes bundled with a certificate management utility, keytool. This can be used to generate our self-signed certificate.

```

keytool -genkey -alias myCertX -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore mycert.p12 -validity 3650

Enter keystore password:
 Re-enter new password:
 What is your first and last name?
 [Unknown]:
 What is the name of your organizational unit?
 [Unknown]:
 What is the name of your organization?
 [Unknown]:
 What is the name of your City or Locality?
 [Unknown]:
 What is the name of your State or Province?
 [Unknown]:
 What is the two-letter country code for this unit?
 [Unknown]:
 Is CN=Unknown, OU=Unknown, O=Unknown, L=Unknown, ST=Unknown, C=Unknown correct?
 [no]: yes

 ```

This will generate a PKCS12 keystore called `mycert.p12` with your newly generate certificate in it, with certificate alias `tomcat`. You will need to reference keystore when we start to configure Spring Boot.

By default your Spring Boot embedded Tomcat container will have HTTP on port 8080 enabled. Spring Boot lets you configure HTTP or HTTPS in the application.properties, but not both at once. If you want to enable both you will need to configure at least one programmatically.  

> SSL can be configured declaratively by setting the various `server.ssl.*` properties, typically in `application.properties` or `application.yml`. The following example shows setting SSL properties in `application.properties`:

```

server.port=8443
server.ssl.key-store=classpath:keystore.jks
server.ssl.key-store-password=secret
server.ssl.key-password=another-secret

```

Using configuration such as the preceding example means the application no longer supports a plain HTTP connector at port 8080. Spring Boot does not support the configuration of both an HTTP connector and an HTTPS connector through application.properties. If you want to have both, you need to configure one of them programmatically. We recommend using application.properties to configure HTTPS, as the HTTP connector is the easier of the two to configure programmatically.

Let’s configure HTTPS in the default `application.yml` file under `src/main/resources` of your Spring Boot application:

```
server:
    port: 8648
    ssl:
      key-store: mycert.p12
      key-store-password: password
      key-store-type: PKCS12
      key-alias: myCertX
```


*Copy the generated keystore file into the `resources` folder and reference the same in `key-store` property as `classpath:` {{file_name}} . If you storing the file directly under the root project, then the prefix `classpath:` is not required.*

Now the application is accessible over HTTPS on `https://localhost:8648`.


---


# Errors and Exceptions encounter and how to resolve them

Following are the errors that you may come across while running the app.

**`java.lang.IllegalArgumentException`: There is no PasswordEncoder mapped for the id "null"**

[Full trace](./exception-trace/noPasswordEncoderMapped.md)

Password storage has undergone a major overhaul to provide more secure defaults and the ability to migrate how passwords are stored. The default `PasswordEncoder` is now [DelegatingPasswordEncoder](https://docs.spring.io/spring-security/site/docs/5.0.0.RC1/api/org/springframework/security/crypto/password/DelegatingPasswordEncoder.html) which is a non-passive change. This change ensures that passwords are now encoded using BCrypt by default, allows for validating passwords in old formats, and allows for upgrading the password storage in the future.

You can easily construct an instance using PasswordEncoderFactories.

```
PasswordEncoder passwordEncoder = PasswordEncoderFactories.createDelegatingPasswordEncoder();
```

Alternatively, you may create your own custom instance. For example:

```
String idForEncode = "bcrypt";
Map encoders = new HashMap<>();
encoders.put(idForEncode, new BCryptPasswordEncoder());
encoders.put("noop", NoOpPasswordEncoder.getInstance());
encoders.put("pbkdf2", new Pbkdf2PasswordEncoder());
encoders.put("scrypt", new SCryptPasswordEncoder());
encoders.put("sha256", new StandardPasswordEncoder());

PasswordEncoder passwordEncoder = new DelegatingPasswordEncoder(idForEncode, encoders);
```

As an immediate fix to the above exception is prefixing the password with {noop}

For example, with a password of
```
password
```
you can simply prefix the password with {noop} like:
```
{noop}password
```
This will work, but it is NOT SECURE so it is not recommended for production environments.

Also, you can achieve the same by adding below bean definition in your security config

```
@SuppressWarnings("deprecation")
	@Bean
	public static NoOpPasswordEncoder passwordEncoder() {
		return (NoOpPasswordEncoder) NoOpPasswordEncoder.getInstance();
	}
```
---





---

# Oauth2 Client Facebook implementation

- Make your client application secure. Facebook does not allow non secured apps anymore for Oauth 2.0 authentication. Use the steps from the previous sections to make your app HTTPS complaint

- Create an app in `https://developers.facebook.com/`

	- Save the client ID and client secret in your `application.yml` file as below.

	```
	security:
  	oauth2:
    client:
      clientId: 169343033729032
      clientSecret: ea31bd0eb13e3657097ed9d186a1276a
      accessTokenUri: https://graph.facebook.com/oauth/access_token
      userAuthorizationUri: https://www.facebook.com/dialog/oauth
      tokenName: oauth_token
      authenticationScheme: query
      clientAuthenticationScheme: form
    resource:
      userInfoUri: https://graph.facebook.com/me

	```

	- Under `Facebook Login` -> `settings` go to the section of **Valid OAuth Redirect URIs**. Add the URLs of the client application from where you are trying to hit Facebook. `https://localhost:8648/login` in my case...

	- Keep the App domains field empty under basic settings.




---


Spring 5 Oauth

https://www.youtube.com/watch?v=WhrOCurxFWU
