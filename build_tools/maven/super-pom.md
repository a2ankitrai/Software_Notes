## The Super POM

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <name>Maven Default Project</name>

    <repositories>
        <repository>
            <id>central</id> (1)
                <name>Maven Repository Switchboard</name>
                <layout>default</layout>
                <url>http://repo1.maven.org/maven2</url>
                <snapshots>
                    <enabled>false</enabled>
                </snapshots>
        </repository>
    </repositories>

    <pluginRepositories>
        <pluginRepository>
            <id>central</id> (2)
                <name>Maven Plugin Repository</name>
                <url>http://repo1.maven.org/maven2</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>false</enabled>
                </snapshots>
                <releases>
                    <updatePolicy>never</updatePolicy>
                </releases>
        </pluginRepository>
    </pluginRepositories>

    <build> (3)
            <directory>${project.basedir}/target</directory>
            <outputDirectory>
                ${project.build.directory}/classes
            </outputDirectory>
            <finalName>${project.artifactId}-${project.version}</finalName>
            <testOutputDirectory>
                ${project.build.directory}/test-classes
            </testOutputDirectory>
            <sourceDirectory>
                ${project.basedir}/src/main/java
            </sourceDirectory>
            <scriptSourceDirectory>src/main/scripts</scriptSourceDirectory>
            <testSourceDirectory>
                ${project.basedir}/src/test/java
            </testSourceDirectory>
            <resources>
                <resource>
                    <directory>${project.basedir}/src/main/resources</directory>
                </resource>
            </resources>
            <testResources>
                <testResource>
                    <directory>${project.basedir}/src/test/resources</directory>
                </testResource>
            </testResources>


            <pluginManagement> (4)
                    <plugins>
                        <plugin>
                            <artifactId>maven-antrun-plugin</artifactId>
                            <version>1.3</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-assembly-plugin</artifactId>
                            <version>2.2-beta-2</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-clean-plugin</artifactId>
                            <version>2.2</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-compiler-plugin</artifactId>
                            <version>2.0.2</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-dependency-plugin</artifactId>
                            <version>2.0</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-deploy-plugin</artifactId>
                            <version>2.4</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-ear-plugin</artifactId>
                            <version>2.3.1</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-ejb-plugin</artifactId>
                            <version>2.1</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-install-plugin</artifactId>
                            <version>2.2</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-jar-plugin</artifactId>
                            <version>2.2</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-javadoc-plugin</artifactId>
                            <version>2.5</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-plugin-plugin</artifactId>
                            <version>2.4.3</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-rar-plugin</artifactId>
                            <version>2.2</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-release-plugin</artifactId>
                            <version>2.0-beta-8</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-resources-plugin</artifactId>
                            <version>2.3</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-site-plugin</artifactId>
                            <version>2.0-beta-7</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-source-plugin</artifactId>
                            <version>2.0.4</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-surefire-plugin</artifactId>
                            <version>2.4.3</version>
                        </plugin>
                        <plugin>
                            <artifactId>maven-war-plugin</artifactId>
                            <version>2.1-alpha-2</version>
                        </plugin>
                    </plugins>
            </pluginManagement>

            <reporting>
                <outputDirectory>target/site</outputDirectory>
            </reporting>
</project>
```