# AOP
---

AOP stands for aspect orientated programming. Essentially, **it is a way for adding behavior to existing code without modifying that code.**

Applications are generally developed with multiple layers. While the responsibilities of each of these layers are different, there are a few common aspects that apply to all layers:

- Logging
- Security

These common aspects are called Cross Cutting Concerns. Aspect Oriented Programming provides a solution to implement Cross Cutting Concerns.

- Implement the cross cutting concern as an aspect.
- Define point cuts to indicate where the aspect has to be applied.

This ensures that the cross cutting concerns are defined in one cohesive code component and can be applied as needed.

---

# AOP Terminology - Pointcut, Advice, Aspect, Join Point

- *Pointcut* - Pointcut is the expression used to define when a call to a method should be intercepted.
  `execution (* com.ank.springaopbasic.**.*.*(..))` is a Pointcut.

- Advice - What do you want to do? It is the logic that you would want to invoke when you intercept a method.

- Aspect - A combination of defining when you want to intercept a method call (Pointcut) and what to do (Advice) is called an Aspect.

- Join Point - When the code is executed and the condition for pointcut is met, the advice is executed. The Join Point is a specific execution instance of an advice.

- Weaver - Weaver is the framework which implements AOP - AspectJ or Spring AOP.

```java
@Aspect
@Configuration
public class UserAccessAspect {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	//What kind of method calls I would intercept
	//execution(* PACKAGE.*.*(..))
	//Weaving & Weaver
	@Before("execution(* com.ank.springaopbasic.*.*(..))")
	public void before(JoinPoint joinPoint){
		//Advice
		logger.info(" Check for user access ");
		logger.info(" Allowed execution for {}", joinPoint);
	}
}
```

---

## Trivia

- When Aspect is annotated with `@Configuration` in the logs Aspect class name comes as `yAspect$$EnhancerBySpringCGLIB$$d63f5b5f`  but when it's annotated with `@Component` actual class name with package gets printed.



















---
