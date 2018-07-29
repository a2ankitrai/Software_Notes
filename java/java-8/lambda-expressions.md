
# Lambda expressions

A lambda expression can be understood as a concise representation of an anonymous function that can be passed around; it doesn't have a name, but it has a list of parameters, a body, a return type, and also possibly a list of exception that can be thrown.

- *Anonymous* -  It doesn't have an explicit name like a method would normally have

- *Function* - Lambda is not associated with a particular class like a method is. But like a method, a lambda has a list of parameters, a body. a return type, and a possible list of exceptions that can be thrown.

- *Passed around*- A lambda expression can be passed as argument to a method or stored in a variable.

- *Concise* - Not much of a boilerplate code is required.

```java
(Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight());
```

A lambda expression has three parts:

- *A list of parameters* - In this case it mirrors the parameters of the compare method of a `Comparator` - two Apples

- *An arrow* - The arrow `->` separates the list of parameters from the body of the lambda.

- *The body of the lambda* - Compare two Apples using their weights. The expression is considered as lambda's return value.

**Examples of lambdas**

- A boolean expression -

  ```java
    (List<String> list) -> list.isEmpty()
  ```

- Creating objects -

  ```
    () -> new Apple(10)
  ```

- Consuming from an object -

  ```java
  (Apple a) -> {
    System.out.println(a.getWeight());
  }
  ```

- Select/extract from an object -

  ```java
    (String s) -> s.length()
  ```

---

# Functional Interface

A Functional Interface is an interface that specifies exactly one abstract method. An interface is still a functional interface if it has many default methods as long as it specifies only one abstract method.

`Predicate` is a functional interface because it specifies only one abstract method:

```java
public interface Predicate<T>{
  boolean test (T t);
}
```

# Function descriptor

The signature of the abstract method of the functional interface essentially describes the signature of the lambda expression. This abstract method is called as a function descriptor.

For e.g. `Runnable` interface signature accepts nothing and returns nothing(void). Hence it's signature `() -> void`.

A lambda expression can be assigned to a variable or passed to a method expecting a functional interface as argument, provided the lambda expression has the same signature as the abstract method of the functional interface.

A lambda expression let you provide the implementation of the abstract method of a functional interface directly inline, and they treat the whole expression as an instance of a functional interface.

`@FunctionalInterface` annotation is used to indicate that the interface is intended to be a functional interface. The compiler will return a meaningful error if you define an interface using the `@FunctionalInterface` annotation and it isn't functional interface. `@FunctionalInterface` annotation isn't mandatory, but it's good practice to use it when an interface is designed for that purpose like the `@Override` notation is used to indicate that a method is overridden.

**Putting lambdas in practice**

```java
public class ExecuteAroundTest {

    public static void printVariation(String s, OntheFlyPrint p) {
	     System.out.println(p.printThis(s));
    }

    public static void main(String[] args) {

    	String s = "Original_String";

    	printVariation(s, (p) -> p); // normal print

    	printVariation(s, (p) -> p.toUpperCase()); // UpperCase Print

    	printVariation(s, (p) -> p.toLowerCase()); // UpperCase Print

    }
}

@FunctionalInterface
interface OntheFlyPrint {

    String printThis(String s);
}
```

Output:

```
Original_String
ORIGINAL_STRING
original_string
```
---

# Existing Functional Interfaces

Java 8 introduces several new functional interfaces inside the `java.util.function` package.

## Predicate

The `java.util.function.Predicate<T>` interface defines an abstract method named `test` that accepts an object of generic type `T` and returns a boolean.

```java
@FunctionalInterface
public interface Predicate<T>{
  boolean test (T t);
}
```
[Example](https://github.com/a2ankitrai/Java8-Shots/blob/master/src/main/java/com/ank/java8/lambda_exp/PredicateTest.java)

## Consumer

The `java.util.function.Consumer<T>` interface defines an abstract method name `accept` that takes an object of generic type `T` and returns no result(void). Use this interface when you need to access an object of type `T` and perform some operations on it.

```java
@FunctionalInterface
public interface Consumer<T>{
  void accept (T t);
}
```

[Example](https://github.com/a2ankitrai/Java8-Shots/blob/master/src/main/java/com/ank/java8/lambda_exp/ConsumerTest.java)

## Function

The `java.util.function.Function<T,R>` interface defines an abstract method named `apply` that takes an object of generic type `T` as input and returns an object of generic type `R`. Use this interface when you need to define a lambda that maps information from an input object to an output.

```java
@FunctionalInterface
public interface Function<T,R>{
  R apply (T t);
}
```

[Example](https://github.com/a2ankitrai/Java8-Shots/blob/master/src/main/java/com/ank/java8/lambda_exp/FunctionTest.java)

## Primitive Specializations

Java 9 also brings specialized version of the above functional interfaces in order to avoid auto-boxing operations when the inputs or outputs are primitives.
For e.g. `IntPredicate`

```java
public interface IntPredicate{
  boolean test(int t);
}
```

**Common Functional Interfaces in Java 8**

![functional-interfaces.jpg](./images/functional-interfaces.jpg)

> Note that none of the functional interfaces allow for a checked exception to be thrown. You have two options if you need a lambda expression to throw an exception: define your own functional interface that declares the checked exception, or wrap the lambda with a `try/catch` block.

---

# Type checking, type inference, and restrictions

**Type Checking**

The type of a lambda is deduced from the context in which the lambda is used. The type expected for the lambda expression inside the context(a method parameter that it's passed to or a local variable that it's assigned to) is called the *target type*.


**Type inference**

The java compiler deduces what functional interface to associate with a lambda expression from its surrounding context (the target type), meaning it can also deduce an appropriate signature for the lambda because the function descriptor is available through the target type. The benefit is that the compiler has access to the types of the parameters of a lambda expression, and they can be omitted in the lambda syntax.

Without type inference

```java
Comparator<Apple> c = (Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight());
```

With type inference

```java
Comparator<Apple> c = (a1, a2) -> a1.getWeight().compareTo(a2.getWeight());
```

**Using local variables**

Lambda expressions are allowed to use *free variables*(variables that aren't the parameters and defined in an outer scope). Such expressions are called as *capturing lambdas*.

Lambdas are allowed to capture instance variable and static variables without restrictions. But local variable have to be explicitly declared `final` or  are effectively `final`. In other words, lambda expressions can capture local variable that are assigned to them only once.

```java
int portNumber = 8903;
Runnable r = () -> System.out.println(portNumber); // Error. local variables referenced from a lambda must be final or effectively final.
portNumber = 9043;
```

**Resctrictions on local variables** -

Instance variables are stored on the heap, whereas local variables live on the stack and are implicitly confined to the thread they're in. If a lambda could access the local variable directly and the lambda were used in a thread, then the thread using the lambda could try to access the variable after the thread that allocated the variable had deallocated it. Hence, Java implements access to a free local variable as access to a copy of it rather than access to the original variable. This makes no difference if the local variable is assigned to only once - hence the restriction.

Allowing capture of mutable local variables opens new thread-unsafe possibilities, which are undesirable.

This restriction also discourages typical imperative programming patterns that mutate an outer variable.

---
