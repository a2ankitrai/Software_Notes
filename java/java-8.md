Java 8
---

# Overview - Java 8 major features:
 
## Behaviour Parameterization

Java 8 adds the ability to pass methods (code) as arguments to other methods. This is referred conceptually as *behaviour parameterization*.
 

## Functional style programming

The whole point of a programming language is to manipulate values (Objects), which are called as first-class citizens (values) of the program as they are passed from one place to another during execution. Other structures in our programming languages, which perhaps helps us express the structure of values but which can't be passed around during program execution, are second-class citizens. Values are first-class Java citizens, but various other Java concepts, such as methods and classes, exemplify second-class citizens..
Being able to pass methods aroung at run-time, and hence making them first-class citizens, is very useful in programming. Java 8 decided to allow methods to be used as values by introducing *method reference* `::` syntax (meaning "use this method as a value").

Another way Java 8 allows methods (specifically block of code) to be used as values is *lambdas*(or anonymous functions).

Programming using above concepts are said to be written in functional-programming style - this phrase means **writing programs that pass functions around as first-class values**.


## Streams

Java 8 provides a new API (Streams) that supports many parallel operations to process data. It avoids the need to write code that uses `synchronized`, which is not only highly error prone but is also more expensive on multicore CPUs.

A *stream* is a sequence of data items that are conceptually produced one at a time - a program might read items from an input stream one by one and similarly write items to an output stream. The output stream of one program could well be the input stream of another.

Java 8 adds a Streams API in `java.util.stream` package base on this idea; `Stream<T>` is a sequence of items of type `T`. The Streams API has many methods that can be chained to form a complex pipeline.

## Default methods

An interface can now contain method signatures for which an implementing class doesn't provide an implementation! The missing method bodies are given as part of the interface (hence default implementations) rather than in the implementing class. 

---

# Passing code with behavior parameterization

*Behaviour Parameterization* is a software development pattern that lets you handle frequent requirement changes. In a nutshell, it means taking a block of code and making it available without executing it. This block of code can be called later by other parts of your programs, which means that you can defer the executionn of that block of code. You could pass the block of code as an arguement to another method that will execute it later. As a result, the method's behavior is parameterized based on that block of code.

The ability to tell method to take multiple behaviors (or strategies) as parameters and use them internally to accomplish different behaviors.(Strategy Design Pattern)

Predicate - The word predicate is often used in mathematics to mean something function-like that takes a values for an arguement and returns `true` or `false`.


```java
import java.util.ArrayList;
import java.util.List;

import com.ank.Java8_Shots.behavior_param.approach2.ApplePredicate;
import com.ank.Java8_Shots.behavior_param.common.Apple;
import com.ank.Java8_Shots.behavior_param.common.AppleUtil;
import com.ank.Java8_Shots.behavior_param.common.Color;

public class AppleFilterTestApproach3 {

    public static List<Apple> filterApples(List<Apple> inventory, ApplePredicate predicate) {
	List<Apple> result = new ArrayList<>();

	for (Apple apple : inventory) {
	    if (predicate.test(apple)) {
		result.add(apple);
	    }
	}
	return result;
    }

    public static void main(String[] args) {

	List<Apple> list = AppleUtil.produceApples();

	// Passing behavior in-line
	List<Apple> greenApples = filterApples(list, (apple) -> apple.getColor() == Color.GREEN);
	
	List<Apple> heavyApples = filterApples(list, (apple) -> apple.getWeight() > 120);
	

	System.out.println("Green Apples:" + greenApples);
	
	System.out.println("Heavy Apples:" + heavyApples);
    }
}
```



































