Maven Error Resolutions
---

## Exclude Transitive dependencies in maven

 `-`[Resolution](https://stackoverflow.com/questions/547805/exclude-all-transitive-dependencies-of-a-single-dependency/7556707#7556707)


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
