Java 9
---

# Java Platform Module System (JPMS)

Java 9 introduces a new level of abstraction above packages, formally known as the Java Platform Module System (JPMS), or “Modules” for short.

---

# Module

**A Module is a group of closely related packages and resources along with a new module descriptor file.** In other words, it’s a “package of Java Packages” abstraction that allows us to make our code even more reusable.

## Packages

The packages inside a module are identical to the Java packages we’ve been using since the inception of Java. When we create a module, we organize the code internally in packages just like we previously did with any other project.

Packages are used to determine what code is publicly accessible outside of the module. 

## Resources

**Each module is responsible for its resources, like media or configuration files.**

Previously we’d put all resources into the root level of our project and manually manage which resources belonged to different parts of the application.

With modules, we can ship required images and XML files with the module that needs it, making our projects much easier to manage.

## Module Descriptor

When we create a module, we include a descriptor file that defines several aspects of our new module:

- **Name** – the name of our module

- **Dependencies** – a list of other modules that this module depends on

- **Public Packages** – a list of all packages we want accessible from outside the module

- **Services Offered** – we can provide service implementations that can be consumed by other modules

- **Services Consumed** – allows the current module to be a consumer of a service

- **Reflection Permissions** – explicitly allows other classes to use reflection to access the private members of a package

The module naming rules are similar to how we name packages (dots are allowed, dashes are not). It’s very common to do either project-style (my.module) or Reverse-DNS (com.ank.mymodule) style names.

**We need to list all packages we want to be public because by default all packages are module private.**

The same is true for reflection. By default, we cannot use reflection on classes we import from another module.

## Module Types

There are four types of modules in the new module system:

There are four types of modules in the new module system:

- **System Modules** – These are the modules listed when we run the list-modules command above. They include the Java SE and JDK modules.

- **Application Modules** – These modules are what we usually want to build when we decide to use Modules. They are named and defined in the compiled module-info.class file included in the assembled JAR.

- **Automatic Modules** – We can include unofficial modules by adding existing JAR files to the module path. The name of the module will be derived from the name of the JAR. Automatic modules will have full read access to every other module loaded by the path.

- **Unnamed Module** – When a class or JAR is loaded onto the classpath, but not the module path, it’s automatically added to the unnamed module. It’s a catch-all module to maintain backward compatibility with previously-written Java code.

## Distribution

Modules can be distributed one of two ways: as a JAR file or as an “exploded” compiled project.

We can create multi-module projects comprised of a “main application” and several library modules.

We have to be careful though because we can only have **one module per JAR file**.

When we set up our build file, we need to make sure to bundle each module in our project as a separate jar.


---

# Default Modules

When we install Java 9, we can see that the JDK now has a new structure.

They have taken all the original packages and moved them into the new module system.

We can see what these modules are by typing into the command line:

```
java --list-modules
```

These modules are split into four major groups: *java*, *javafx*, *jdk*, and *Oracle*.

*java* modules are the implementation classes for the core SE Language Specification.

*javafx* modules are the FX UI libraries.

Anything needed by the JDK itself is kept in the *jdk** modules.

And finally, anything that is Oracle-specific is in the *oracle* modules.

---

# Module Declarations

To set up a module, we need to put a special file at the root of our packages named `module-info.java`.

This file is known as the module descriptor and contains all of the data needed to build and use our new module.

We construct the module with a declaration whose body is either empty or made up of module directives:

```java

module myModuleName {
    // all directives are optional
}

```

We start the module declaration with the module keyword, and we follow that with the name of the module.

The module will work with this declaration, but we’ll commonly need more information.

That is where the module directives come in.

## Requires

Our first directive is requires. This module directive allows us to declare module dependencies:

```java

module my.module {
    requires module.name;
}

```
Now, `my.module` has both a runtime and a compile-time dependency on `module.name`.

And all public types exported from a dependency are accessible by our module when we use this directive.

## Requires Static

Sometimes we write code that references another module, but that users of our library will never want to use.

For instance, we might write a utility function that pretty-prints our internal state when another logging module is present. But, not every consumer of our library will want this functionality, and they don’t want to include an extra logging library.

In these cases, we want to use an optional dependency. By using the requires static directive, we create a compile-time-only dependency:

```
module my.module {
    requires static module.name;
}
```

## Requires Transitive

We commonly work with libraries to make our lives easier.

But, we need to make sure that any module that brings in our code will also bring in these extra ‘transitive’ dependencies or they won’t work.

Luckily, we can use the requires transitive directive to force any downstream consumers also to read our required dependencies:

```java

module my.module {
    requires transitive module.name;
}
```

Now, when a developer requires `my.module`, they won’t also have also to say requires `module.name` for our module to still work.

## Exports

By default, a module doesn’t expose any of its API to other modules. This strong encapsulation was one of the key motivators for creating the module system in the first place.

Our code is significantly more secure, but now we need to explicitly open our API up to the world if we want it to be usable.

We use the exports directive to expose all public members of the named package:

```java 

module my.module {
    exports com.my.package.name;
}
```

Now, when someone does requires `my.module`, they will have access to the public types in our `com.my.package.name` package, but not any other package.

## Exports … To

We can use exports…to to open up our public classes to the world.

But, what if we don’t want the entire world to access our API?

We can restrict which modules have access to our APIs using the exports…to directive.

Similar to the exports directive, we declare a package as exported. But, we also list which modules we are allowing to import this package as a requires.


```java

module my.module {
    export com.my.package.name to com.specific.package;
}
```

## Uses

A service is an implementation of a specific interface or abstract class that can be consumed by other classes.

We designate the services our module consumes with the uses directive.

Note that the class name we use is either the interface or abstract class of the service, not the implementation class:

```java

module my.module {
    uses class.name;
}
```

We should note here that there’s a difference between a requires directive and the uses directive.

We might require a module that provides a service we want to consume, but that service implements an interface from one of its transitive dependencies.

Instead of forcing our module to require all transitive dependencies just in case, we use the uses directive to add the required interface to the module path.



http://www.baeldung.com/java-9-modularity















