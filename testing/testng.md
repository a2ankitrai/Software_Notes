TestNG
---

TestNG is an open source automated testing framework; where NG of TestNG means Next Generation. 

# Annotations in TestNG

- `@BeforeSuite`: The annotated method will be run before all tests in this suite have run.

- `@AfterSuite`: The annotated method will be run after all tests in this suite have run.

- `@BeforeTest`: The annotated method will be run before any test method belonging to the classes inside the tag is run.

- `@AfterTest`: The annotated method will be run after all the test methods belonging to the classes inside the tag have run.

- `@BeforeGroups`: The list of groups that this configuration method will run before. This method is guaranteed to run shortly before the first test method that belongs to any of these groups is invoked.

- `@AfterGroups`: The list of groups that this configuration method will run after. This method is guaranteed to run shortly after the last test method that belongs to any of these groups is invoked.

- `@BeforeClass`: The annotated method will be run before the first test method in the current class is invoked.

- `@AfterClass`: The annotated method will be run after all the test methods in the current class have been run.

- `@BeforeMethod`: The annotated method will be run before each test method.

- `@AfterMethod`: The annotated method will be run after each test method.

- `@Test`: The annotated method is a part of a test case.

---

# Configure TestNG to use the PowerMock object factory (Mocking static objects with TestNG)

## Using suite.xml

In your suite.xml add the following in the suite tag: `object-factory="org.powermock.modules.testng.PowerMockObjectFactory"` e.g.

```xml
<suite name="dgf" verbose="10"
    object-factory="org.powermock.modules.testng.PowerMockObjectFactory">
    <test name="dgf">
        <classes>
            <class name="com.mycompany.Test1"/>
            <class name="com.mycompany.Test2"/>
        </classes>
    </test> 
```

If you're using Maven you may need to point out the file to Surefire:

```xml

<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <configuration>
        <suiteXmlFiles>
        <suiteXmlFile>suite.xml</suiteXmlFile>
        </suiteXmlFiles>
    </configuration> 
</plugin> 
```

## Programmatically

Add a method like this to your test class:

```java

@ObjectFactory public IObjectFactory getObjectFactory() {
     return new org.powermock.modules.testng.PowerMockObjectFactory(); 
} 
```

or to be on the safe side you can also extend from the `PowerMockTestCase`:

```java
@PrepareForTest(IdGenerator.class) 
public class MyTestClass extends PowerMockTestCase { ... }
```