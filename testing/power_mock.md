PowerMock
---

PowerMock is a Java framework that allows you to unit test code normally regarded as untestable.

![powermock.png](./images/powermock.png)

PowerMock is a framework that extends other mock libraries such as EasyMock with more powerful capabilities. PowerMock uses a custom classloader and bytecode manipulation to enable mocking of static methods, constructors, final classes and methods, private methods, removal of static initializers and more. Currently PowerMock supports EasyMock and Mockito.

When writing unit tests it is often useful to bypass encapsulation and therefore PowerMock includes several features that simplifies reflection specifically useful for testing. This allows easy access to internal state, but also simplifies partial and private mocking.

- PowerMock allows mocking of both private and final methods.

- PowerMock allows you to use static methods for performance and mock.

The main advantage from Powermock is that you can use it to test certain constructs (for example static method invocations) that EasyMock can't mock. Thus: when you want to test 3rd party code that you can't change; and that contains static calls; then you might turn to PowerMock.

# Getting Started

PowerMock consists of two extension API's.

One for EasyMock and one for Mockito. To use PowerMock you need to depend on one of these API's as well as a test framework. Currently PowerMock supports JUnit and TestNG. 

**Writing tests**

Write a test like this:

```java

@RunWith(PowerMockRunner.class)
@PrepareForTest( { YourClassWithEgStaticMethod.class })
public class YourTestCase {
...
}
```

---

# Bypass encapsulation

[Whitebox](http://www.javadoc.io/doc/org.powermock/powermock-reflect/1.7.1) class provides a set of methods which could you help bypass encapsulation if it required. Usually, it's not a good idea to get/modify non-public fields, but sometimes it's only way to cover code by test for future refactoring.

- Use `Whitebox.setInternalState(..)` to set a non-public member of an instance or class.
- Use `Whitebox.getInternalState(..)` to get a non-public member of an instance or class.
- Use `Whitebox.invokeMethod(..)` to invoke a non-public method of an instance or class.
- Use `Whitebox.invokeConstructor(..)` to create an instance of a class with a private constructor.


## Access internal state

For mutable objects internal state may change after a method has been invoked. When unit testing such objects it's good to have an easy way to get a hold of this state and see if it has updated accordingly. PowerMock supplies several useful reflection utilities specially designed to be used with unit testing. All of these reflection utilities are located in the `org.powermock.reflect.Whitebox` class.

```java

public class ServiceHolder {

	private final Set<Object> services = new HashSet<Object>();

	public void addService(Object service) {
		services.add(service);
	}

	public void removeService(Object service) {
		services.remove(service);
	}
}
```

To test the `addService` method we need to access private member  `Set<Object> services`. One way of doing this is to add a package-private or protected method called something like `getServices()` which returns the services set. But by doing this we've added a method to the ServiceHolder class that has no other purpose than making the class testable.  

`Whitebox.getInternalState(..)` method in PowerMock to accomplish the same thing without altering the production code.


```java

@Test
public void testAddService() throws Exception {
	ServiceHolder tested = new ServiceHolder();
	final Object service = new Object();

	tested.addService(service);

        // This is how you get the private services set using PowerMock
	Set<String> services = Whitebox.getInternalState(tested,
			"services");

	assertEquals("Size of the \"services\" Set should be 1", 1, services
			.size());
	assertSame("The services Set should didn't contain the expect service",
			service, services.iterator().next());
}

```

Using PowerMock 1.0 or above you can also get the internal state by specifying the type of the field to get.

```java
Set<String> services = Whitebox.getInternalState(tested, Set.class);
```

To set the internal state of an object:

```java
Whitebox.setInternalState(tested, "services", myServiceObject);

```

## Invoking a private method

To invoke a private method you can make use of the `Whitebox.invokeMethod(..)` method in PowerMock.

```java
private int sum(int a, int b) {
	return a+b;
}
```


```java
int sum = Whitebox.<Integer> invokeMethod(myInstance, "sum", 1, 2);
```

## Instantiate a class with a private constructor

To instantiate a class with a private constructor such as:

```java
public class PrivateConstructorInstantiationDemo {

	private final int state;

	private PrivateConstructorInstantiationDemo(int state) {
		this.state = state;
	}

	public int getState() {
		return state;
	}
}
```

```java
PrivateConstructorInstantiationDemo instance =  WhiteBox.invokeConstructor(PrivateConstructorInstantiationDemo.class, 43);
```

where 43 is the state parameter.

---

# Suppressing Unwanted Behavior

To be Continued...

https://github.com/powermock/powermock/wiki/Suppress-Unwanted-Behavior



---

# Important Trivia

Mocking a static method of a class works with a combination of PowerMock + Junit. Mocking static objects with TestNG causes issues

Working code for the same:

```java
import org.junit.runner.RunWith;
import org.powermock.core.classloader.annotations.PrepareForTest;
import org.junit.Test;

@RunWith(PowerMockRunner.class)
@PrepareForTest( { Math.class })
public class MathTest {

    @Test
    public void test2(){
        PowerMock.mockStatic(Math.class);
        EasyMock.expect(Math.abs(-123)).andReturn(1);
        PowerMock.replay(Math.class);
        long returns = Math.abs(-123);
        PowerMock.verify(Math.class);
        assertEquals(1, returns);
    }
}
``` 