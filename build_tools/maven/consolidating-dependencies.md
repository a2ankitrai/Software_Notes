
### Consolidating Dependencies in a Single POM Project.

```xml 

<project>
    <groupId>org.sonatype.mavenbook</groupId>
    <artifactId>persistence-deps</artifactId>
    <version>1.0</version>
    <packaging>pom</packaging>
    <dependencies>
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate</artifactId>
            <version>${hibernateVersion}</version>
        </dependency>
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-annotations</artifactId>
            <version>${hibernateAnnotationsVersion}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-hibernate3</artifactId>
            <version>${springVersion}</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>${mysqlVersion}</version>
        </dependency>
    </dependencies>
    <properties>
        <mysqlVersion>(5.1,)</mysqlVersion>
        <springVersion>(2.0.6,)</springVersion>
        <hibernateVersion>3.2.5.ga</hibernateVersion>
        <hibernateAnnotationsVersion>3.3.0.ga</hibernateAnnotationsVersion>
    </properties>
</project>
```
