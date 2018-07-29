
Customizing Behavior of the Clean Plugin.
---

 The example below configures clean to remove all .class files in a directory named target-other/ using standard Ant file wildcards: `*` and `\**`.

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    ...
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-clean-plugin</artifactId>
                <configuration>
                    <filesets>
                        <fileset>
                            <directory>target-other</directory>
                            <includes>
                                <include>*.class</include>
                            </includes>
                        </fileset>
                    </filesets>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```
