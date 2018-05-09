```


  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.0.1.RELEASE)

2018-04-21 21:05:37.643  INFO 2384 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 774 ms
2018-04-21 21:05:38.162  INFO 2384 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/**/favicon.ico] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
2018-04-21 21:05:38.205  INFO 2384 --- [           main] s.w.s.m.m.a.RequestMappingHandlerAdapter : Looking for @ControllerAdvice: org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@1ab3a8c8: startup date [Sat Apr 21 21:05:36 IST 2018]; root of context hierarchy
2018-04-21 21:05:38.249  INFO 2384 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/index]}" onto public java.lang.String org.HelloSpringSecurityBoot.security.web.MyController.index()
2018-04-21 21:05:38.249  INFO 2384 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/]}" onto public java.lang.String org.HelloSpringSecurityBoot.security.web.MyController.root()
2018-04-21 21:05:38.249  INFO 2384 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/login],methods=[POST]}" onto public java.lang.String org.HelloSpringSecurityBoot.security.web.MyController.postLogin()
2018-04-21 21:05:38.250  INFO 2384 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/login-error]}" onto public java.lang.String org.HelloSpringSecurityBoot.security.web.MyController.loginError(org.springframework.ui.Model)
2018-04-21 21:05:38.251  INFO 2384 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/user/index]}" onto public java.lang.String org.HelloSpringSecurityBoot.security.web.MyController.userIndex()
2018-04-21 21:05:38.251  INFO 2384 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/login]}" onto public java.lang.String org.HelloSpringSecurityBoot.security.web.MyController.login()
2018-04-21 21:05:38.254  INFO 2384 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error]}" onto public org.springframework.http.ResponseEntity<java.util.Map<java.lang.String, java.lang.Object>> org.springframework.boot.autoconfigure.web.servlet.error.BasicErrorController.error(javax.servlet.http.HttpServletRequest)
2018-04-21 21:05:38.254  INFO 2384 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error],produces=[text/html]}" onto public org.springframework.web.servlet.ModelAndView org.springframework.boot.autoconfigure.web.servlet.error.BasicErrorController.errorHtml(javax.servlet.http.HttpServletRequest,javax.servlet.http.HttpServletResponse)
2018-04-21 21:05:38.272  INFO 2384 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/webjars/**] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
2018-04-21 21:05:38.272  INFO 2384 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/**] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
2018-04-21 21:05:47.421  INFO 2384 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : FrameworkServlet 'dispatcherServlet': initialization started
2018-04-21 21:05:47.435  INFO 2384 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : FrameworkServlet 'dispatcherServlet': initialization completed in 14 ms
2018-04-21 21:06:29.498 ERROR 2384 --- [nio-8080-exec-9] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception

java.lang.IllegalArgumentException: There is no PasswordEncoder mapped for the id "null"
	at org.springframework.security.crypto.password.DelegatingPasswordEncoder$UnmappedIdPasswordEncoder.matches(DelegatingPasswordEncoder.java:238) ~[spring-security-core-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.crypto.password.DelegatingPasswordEncoder.matches(DelegatingPasswordEncoder.java:198) ~[spring-security-core-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.config.annotation.authentication.configuration.AuthenticationConfiguration$LazyPasswordEncoder.matches(AuthenticationConfiguration.java:289) ~[spring-security-config-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.authentication.dao.DaoAuthenticationProvider.additionalAuthenticationChecks(DaoAuthenticationProvider.java:86) ~[spring-security-core-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.authentication.dao.AbstractUserDetailsAuthenticationProvider.authenticate(AbstractUserDetailsAuthenticationProvider.java:166) ~[spring-security-core-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.authentication.ProviderManager.authenticate(ProviderManager.java:174) ~[spring-security-core-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.authentication.ProviderManager.authenticate(ProviderManager.java:199) ~[spring-security-core-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter.attemptAuthentication(UsernamePasswordAuthenticationFilter.java:94) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.authentication.AbstractAuthenticationProcessingFilter.doFilter(AbstractAuthenticationProcessingFilter.java:212) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.authentication.logout.LogoutFilter.doFilter(LogoutFilter.java:116) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.csrf.CsrfFilter.doFilterInternal(CsrfFilter.java:124) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.header.HeaderWriterFilter.doFilterInternal(HeaderWriterFilter.java:66) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.context.SecurityContextPersistenceFilter.doFilter(SecurityContextPersistenceFilter.java:105) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter.doFilterInternal(WebAsyncManagerIntegrationFilter.java:56) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.FilterChainProxy.doFilterInternal(FilterChainProxy.java:215) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.security.web.FilterChainProxy.doFilter(FilterChainProxy.java:178) ~[spring-security-web-5.0.4.RELEASE.jar:5.0.4.RELEASE]
	at org.springframework.web.filter.DelegatingFilterProxy.invokeDelegate(DelegatingFilterProxy.java:357) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.springframework.web.filter.DelegatingFilterProxy.doFilter(DelegatingFilterProxy.java:270) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:99) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.springframework.web.filter.HttpPutFormContentFilter.doFilterInternal(HttpPutFormContentFilter.java:109) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.springframework.web.filter.HiddenHttpMethodFilter.doFilterInternal(HiddenHttpMethodFilter.java:81) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:200) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-5.0.5.RELEASE.jar:5.0.5.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:198) ~[tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:96) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:496) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:140) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:81) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:87) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:342) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:803) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:66) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:790) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1459) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142) [na:1.8.0_121]
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617) [na:1.8.0_121]
	at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61) [tomcat-embed-core-8.5.29.jar:8.5.29]
	at java.lang.Thread.run(Thread.java:745) [na:1.8.0_121]

```