
Spring Session
---

Spring Session provides an API and implementations for managing a user’s session information, while also making it trivial to support clustered sessions without being tied to an application container specific solution. It also provides transparent integration with:

- HttpSession - allows replacing the HttpSession in an application container (i.e. Tomcat) neutral way, with support for providing session IDs in headers to work with RESTful APIs.

- WebSocket - provides the ability to keep the HttpSession alive when receiving WebSocket messages

- WebSession - allows replacing the Spring WebFlux’s WebSession in an application container neutral way.






Spring Data Redis
---

Spring Data provides API to perform Redis operations with ease. Redis is an open source, in memory data-structure store that can be used as database, cache and message broker. Redis supports data-structure such as strings, hashes, lists, sets etc. Redis is a NoSQL storage and uses key/value to store data.

Spring Data provides different connection factories to get Redis connections. The example of connection factories are `JedisConnectionFactory`, `LettuceConnectionFactory` etc. Jedis is a Redis Java client that is easy to use and small in size. 

Spring Data provides `RedisTemplate` to perform Redis operations. `RedisTemplate` has methods such as `opsForList()`, `opsForSet()`, `opsForHash()` etc that return `ListOperations`, `SetOperations`, `HashOperations` respectively. Most of the time we perform Redis operations with string datatype. So Spring Data has provided a string-focused extension as `StringRedisTemplate` that extends `RedisTemplate`. So `StringRedisTemplate` has all methods of `RedisTemplate` to perform Redis operations based on string datatype.


---

## Dependencies

pom.xml

```xml
<dependencies>
	<!-- ... -->

	<dependency>
		<groupId>org.springframework.session</groupId>
		<artifactId>spring-session-data-redis</artifactId>
	</dependency>
</dependencies>
```

Spring Boot provides dependency management for Spring Session modules, so there’s no need to explicitly declare dependency version.


## Spring Boot Configuration

Setting up Spring Session backed by Redis is as simple as adding a single configuration property to your `application.properties`:

*src/main/resources/application.properties*

```
spring.session.store-type=redis # Session store type.
```
Under the hood, Spring Boot will apply configuration that is equivalent to manually adding `@EnableRedisHttpSession` annotation. This creates a Spring Bean with the name of `springSessionRepositoryFilter `that implements Filter. The filter is what is in charge of replacing the `HttpSession` implementation to be backed by Spring Session.

Further customization is possible using application.properties:

*src/main/resources/application.properties*
```
server.servlet.session.timeout= # Session timeout. If a duration suffix is not specified, seconds will be used.
spring.session.redis.flush-mode=on-save # Sessions flush mode.
spring.session.redis.namespace=spring:session # Namespace for keys used to store sessions.
```

## Configuring the Redis Connection

Spring Boot automatically creates a RedisConnectionFactory that connects Spring Session to a Redis Server on localhost on port 6379 (default port). For customization update the following:

*src/main/resources/application.properties*
```
spring.redis.host=localhost # Redis server host.
spring.redis.password= # Login password of the redis server.
spring.redis.port=6379 # Redis server port.
```

---

# Simple Application to store and manage sessions

Create a Spring-boot application and set a connection factory to get Redis connections. We will use `JedisConnectionFactory`. Also, create a `RedisTemplate` using this connection factory.

```java  
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.data.redis.connection.jedis.JedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.core.StringRedisTemplate;

@SpringBootApplication
public class SpringSessionBootApplication {

    @Bean
    JedisConnectionFactory jedisConnectionFactory() {
	return new JedisConnectionFactory();
    }

    @Bean
    public RedisTemplate<String, Object> redisTemplate() {
	RedisTemplate<String, Object> template = new RedisTemplate<>();
	template.setConnectionFactory(jedisConnectionFactory());
	return template;
    }
    
    @Bean
    public StringRedisTemplate stringRedisTemplate() {
	StringRedisTemplate stringRedisTemplate = new StringRedisTemplate();
	stringRedisTemplate.setConnectionFactory(jedisConnectionFactory());
	return stringRedisTemplate;
    }

    public static void main(String[] args) {
	SpringApplication.run(SpringSessionBootApplication.class, args);
    }
}
```

<br>

Create the Security configuration authenticating with HTTP-Basic and setting the auth-token-header with spring's `HeaderHttpSessionIdResolver`

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.crypto.bcrypt.BCrypt;
import org.springframework.security.web.savedrequest.NullRequestCache;
import org.springframework.session.web.http.HeaderHttpSessionIdResolver;
import org.springframework.session.web.http.HttpSessionIdResolver;

@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {

	http

		.authorizeRequests()

		.anyRequest().authenticated()

		.and()

		.requestCache().requestCache(new NullRequestCache())

		.and()

		.httpBasic(); 
    }

    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {

	String pw = BCrypt.hashpw("password", BCrypt.gensalt());
	auth.inMemoryAuthentication().withUser("user").password("{bcrypt}" + pw).roles("USER");
    }
     
    @Bean
    public HttpSessionIdResolver httpSessionIdResolver() {
	return HeaderHttpSessionIdResolver.xAuthToken();
    }
} 
```

Update `application.properties` to include redis configuration settings.

```properties
# Session store type.
# Under the hood, Spring Boot will apply configuration that is equivalent to manually adding @EnableRedisHttpSession annotation. 
# This creates a Spring Bean with the name of springSessionRepositoryFilter that implements Filter. 
# The filter is what is in charge of replacing the HttpSession implementation to be backed by Spring Session.
spring.session.store-type=redis 

# Session timeout. If a duration suffix is not specified, seconds will be used.
server.servlet.session.timeout= 6000 
# Sessions flush mode.
spring.session.redis.flush-mode=on-save 
# Namespace for keys used to store sessions.
spring.session.redis.namespace=spring:session 

# Redis server host.
spring.redis.host=localhost 

# Login password of the redis server.
# spring.redis.password= 

# Redis server port.
spring.redis.port=6379 
```

Controller Code:

```java 
import javax.servlet.http.HttpSession;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
    
    public static final Logger logger = LoggerFactory.getLogger(HelloController.class);

    @GetMapping("/hello")
    public String hello(HttpSession session) {
		logger.info("hello: Start: ");
		System.out.println(session.getId());
	 
		logger.info("hello: End: ");
		return "Helo Ankit!";
    }
    
    @GetMapping("/")
    public String welcomeMessage() {
		logger.info("welcomeMessage: Start: ");
		logger.info("welcomeMessage: End: ");
		return "Welcome To Distopia!!";
    }
    
    @GetMapping("/logout")
    @ResponseStatus(HttpStatus.NO_CONTENT)
    public void logout(HttpSession session) {
		logger.info("logout: Start: ");
		logger.info("invalidating the session: ");
		session.invalidate();
		logger.info("logout: end: ");
    }
}
```

Each of the endpoints request will be authenticated as we have set `http.authorizeRequests().anyRequest().authenticated()` in our `SecurityConfiguration` class. Therefore, we either need to pass the credentials (username & password) with each request or the session token value under the header `X-Auth-Token`. On calling the `/logout` endpoint, we are invalidating the session so that no further requests having the session token header will be able to access the same. 









