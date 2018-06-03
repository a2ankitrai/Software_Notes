JUnit 5 
---

JUnit 5 is composed of several different modules from three different sub-projects.

**JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage**

The JUnit Platform serves as a foundation for launching testing frameworks on the JVM. It also defines the [TestEngine](https://junit.org/junit5/docs/current/api/org/junit/platform/engine/TestEngine.html) API for developing a testing framework that runs on the platform.

JUnit Jupiter is the combination of the new programming model and extension model for writing tests and extensions in JUnit 5. The Jupiter sub-project provides a TestEngine for running Jupiter based tests on the platform.

JUnit Vintage provides a TestEngine for running JUnit 3 and JUnit 4 based tests on the platform.

---

## JUnit Jupiter Sample Projects

The [`junit5-samples`](https://github.com/junit-team/junit5-samples) repository hosts a collection of sample projects based on JUnit Jupiter and JUnit Vintage. You’ll find the respective `build.gradle` and `pom.xml` in the projects below.

For Gradle, check out the `junit5-jupiter-starter-gradle` project.

For Maven, check out the `junit5-jupiter-starter-maven` project.

---

# Writing Tests

```java
import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.Test;

class FirstJUnit5Tests {

    @Test
    void myFirstTest() {
        assertEquals(2, 1 + 1);
    }

}
```

## Annotations

https://junit.org/junit5/docs/current/user-guide/#writing-tests-annotations