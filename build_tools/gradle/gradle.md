Gradle
---

Gradle is a build tool which replaces XML based build scripts with an internal DSL which is based on Groovy programming language.


# Installing Gradle

If we are using OS X, we can install Gradle by using Homebrew. We can do this by running the following command at command prompt:

```
brew install gradle
```

[Additional guide](https://docs.gradle.org/current/userguide/installation.html)


---

# Gradle Concepts

Gradle has two basic concepts: projects and tasks

- A **project** is either something we build (e.g. a jar file) or do (deploy our application to production environment). **A project consists of one or more tasks.**

- A **task** is an atomic unit work which is performed our build (e.g. compiling our project or running tests).

Every Gradle build contains one or more projects.

![gradle_relationship](./images/gradle_relationship.png)

---

We can configure our Gradle build by using the following configuration files:

- The Gradle build script (build.gradle) specifies a project and its tasks.

- The Gradle properties file (gradle.properties) is used to configure the properties of the build.

- The Gradle Settings file (settings.gradle) is optional in a build which has only one project. If our Gradle build has more than one projects, it is mandatory because it describes which projects participate to our build. Every multi-project build must have a settings file in the root project of the project hierarchy.

## Gradle Plugins

The design philosophy of Gradle is that all useful features are provided by Gradle plugins. A Gradle plugin can:

- Add new tasks to the project.

- Provide a default configuration for the added tasks. The default configuration adds new conventions to the project (e.g. the location of source code files).

- Add new properties which are used to override the default configuration of the plugin.

- Add new dependencies to the project.

We can apply a Gradle plugin (this term is used when we add a plugin to a project) by using either its name or type.

-  by name (the name of the plugin is foo) - by adding the following line to the build.gradle file:

	- `apply plugin: 'foo'`


-  by type (the type of the plugin is com.bar.foo) - we must add the following line to the build.gradle file:

	- `apply plugin: 'com.bar.foo'`


---

## Gradle Wrapper

Gradle wrapper is a convinient feature of gradle that allows to maintain the version of the gradle build across differnt executions and platforms. Gradle Wrapper task can be created as below:

```

task wrapper(type: Wrapper) {
	gradleVersion = '4.6'
}

```

---

## Gradle Tasks

**What is a Task?**

Code that Gradle executes

- Has a lifecycle
- Has properties
- Has 'actions'
- Has dependencies

Ways to declare tasks in gradle

```
project.task("Task1")

task("Task2")

task "Task3"

task Task4

Task4.description = "Task4 description"

```

**Running a Task**

All tasks have a method called `doLast{}`

```
Task4.doLast {println "This is Task 4 in Action"}

```

or

```
Task3 << {println "This is Task 3 (three) in Running mode"}

```

---

[Building a spring project in gradle](https://spring.io/guides/gs/gradle/#scratch)

---

## How to define Gradle's home in IDEA?

https://stackoverflow.com/questions/18495474/how-to-define-gradles-home-in-idea

---

To be continued...

https://www.petrikainulainen.net/programming/gradle/getting-started-with-gradle-our-first-java-project/
