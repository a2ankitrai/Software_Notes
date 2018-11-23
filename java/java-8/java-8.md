# Java 8
---

Overview - Java 8 major features:
---

## Behavior Parameterization

Java 8 adds the ability to pass methods (code) as arguments to other methods. This is referred conceptually as *behaviour parameterization*.


## Functional style programming

The whole point of a programming language is to manipulate values (Objects), which are called as first-class citizens (values) of the program as they are passed from one place to another during execution. Other structures in our programming languages, which perhaps helps us express the structure of values but which can't be passed around during program execution, are second-class citizens. Values are first-class Java citizens, but various other Java concepts, such as methods and classes, exemplify second-class citizens.

Being able to pass methods around at run-time, and hence making them first-class citizens, is very useful in programming. Java 8 decided to allow methods to be used as values by introducing *method reference* `::` syntax (meaning "use this method as a value").

Another way Java 8 allows methods (specifically block of code) to be used as values is *lambdas*(or anonymous functions).

Programming using above concepts are said to be written in functional-programming style - this phrase means **writing programs that pass functions around as first-class values**.


## Streams

Java 8 provides a new API (Streams) that supports many parallel operations to process data. It avoids the need to write code that uses `synchronized`, which is not only highly error prone but is also more expensive on multicore CPUs.

A *stream* is a sequence of data items that are conceptually produced one at a time - a program might read items from an input stream one by one and similarly write items to an output stream. The output stream of one program could well be the input stream of another.

Java 8 adds a Streams API in `java.util.stream` package base on this idea; `Stream<T>` is a sequence of items of type `T`. The Streams API has many methods that can be chained to form a complex pipeline.

## Default methods

An interface can now contain method signatures for which an implementing class doesn't provide an implementation! The missing method bodies are given as part of the interface (hence default implementations) rather than in the implementing class.

---

# Fundamentals

- [Passing code with behavior parameterization](./behavior-parameterization.md)

- [Lambda Expressions](./lambda-expressions.md)

- [Method references](./method-references.md)

# Functional-style data processing

- [Streams](./streams-introduction.md)

- [Working with streams](./working-with-streams.md)

- Collecting data with Streams

- Parallel data processing and performance

# Effective Java 8 Programming

- Refactoring, testing and debugging

- Default methods

- [Optional as an alternative to null](./optional.md)



















----
