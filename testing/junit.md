# JUnit

JUnit is a test framework which uses annotations to identify methods that specify a test. JUnit is an open source project hosted at [Github](https://github.com/junit-team).

Annotations for Junit testing

The Junit 4.x framework is annotation based.

- `@Test` annotation specifies that method is the test method.

- `@Test(timeout=1000)` annotation specifies that method will be failed if it takes longer than 1000 milliseconds (1 second).

- `@BeforeClass` annotation specifies that method will be invoked only once, before starting all the tests.

- `@Before` annotation specifies that method will be invoked before each test.

- `@After` annotation specifies that method will be invoked after each test.
 
- `@AfterClass` annotation specifies that method will be invoked only once, after finishing all the tests.

---

# Assert class

The `org.junit.Assert` class provides methods to assert the program logic.

**Methods of Assert class**
The common methods of Assert class are as follows:

- `void assertEquals(boolean expected,boolean actual)`: checks that two primitives/objects are equal. It is overloaded.
- `void assertTrue(boolean condition)`: checks that a condition is true.
- `void assertFalse(boolean condition)`: checks that a condition is false.
- `void assertNull(Object obj)`: checks that object is null.
- `void assertNotNull(Object obj)`: checks that object is not null.


Mockito - Deep Stubs

- When you are having chained calls on an object : `obj.meth1().meth2().meth3()`	

![Stackover flow link](https://stackoverflow.com/questions/37191589/powermock-chained-method-calls-in-final-class?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

---