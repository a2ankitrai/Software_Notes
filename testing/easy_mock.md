EasyMock
---

EasyMock is a mock framework which can be easily used in conjunction with JUnit. EasyMock instantiates an object based on an interface or class.

```java

import static org.easymock.EasyMock.createNiceMock;
....

// ICalcMethod is the object which is mocked
ICalcMethod calcMethod = createNiceMock(ICalcMethod.class);
```

The `createNiceMock()` method creates a mock which returns default values for methods which are not overriden. A mock created with the `Mock()` method will fails in such a case.

EasyMock has several methods which are used to configure the Mock object. 

- The `expect()` method tells EasyMock to simulate a method with certain arguments. 

- The `andReturn()` method defines the return value of this method for the specified method parameters. 

- The `times()` method defines how often the Mock object will be called.

- The `replay()` method is called to make the Mock object available.

```java

// setup the mock object
expect(calcMethod.calc(Position.BOSS)).andReturn(70000.0).times(2);
expect(calcMethod.calc(Position.PROGRAMMER)).andReturn(50000.0);

// Setup is finished need to activate the mock
replay(calcMethod);

```

---

# Issues while running EasuMock test

```
java.lang.IllegalStateException: 0 matchers expected, 7 recorded.
This exception usually occurs when matchers are mixed with raw values when recording a method:
 foo(5, eq(6)); // wrong
You need to use no matcher
```


