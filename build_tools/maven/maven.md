Maven
---

# Maven Best Practices

http://books.sonatype.com/mvnref-book/reference/pom-relationships-sect-pom-best-practice.html


# References

http://books.sonatype.com/mvnref-book/reference/index.html


**Aggregate POM**

A complete application typically consists of multiple Maven projects. As the number of projects grows larger, however, it becomes a nuisance to build each project separately. Moreover, it is usually necessary to build the projects in a certain order and the developer must remember to observe the correct build order.

To simplify building multiple projects, you can optionally create an aggregate Maven project. This consists of a single POM file (the aggregate POM), usually in the parent directory of the individual projects. The POM file specifies which sub-projects (or modules) to build and builds them in the specified order.

**Parent POM**

Maven also supports the notion of a parent POM. A parent POM enables you to define an inheritance style relationship between POMs. POM files at the bottom of the hierarchy declare that they inherit from a specific parent POM. The parent POM can then be used to share certain properties and details of configuration.

---

# Creating a multi-module project

To create a multi-module project in eclipse, create a quickstart maven project and change the packaging from `jar` to `pom`.

```xml

  <groupId>com.ank</groupId>
  <artifactId>spring-shots</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>pom</packaging>

```



---
#Errors encountered in maven

## Exclude Transitive dependencies in maven

[Stackoverflow question link](https://stackoverflow.com/questions/547805/exclude-all-transitive-dependencies-of-a-single-dependency/7556707#7556707)


## **Java version automatically change to java 1.5 after maven update**

Open your pom.xml file and add the following lines on it:

```xml
<properties>
   <maven.compiler.source>1.8</maven.compiler.source>
   <maven.compiler.target>1.8</maven.compiler.target>
</properties>
```

Where 1.8 is the java version of your current JDK/JRE. Another way of doing this is adding a `<build>` with the `maven-compile-plugin` as

```xml
<build>
<plugins>
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.2</version> <!-- or whatever current version -->
    <configuration>
      <source>1.8</source>
      <target>1.8</target>
    </configuration>
  </plugin>
</plugins>
</build>
```