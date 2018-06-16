# Passing code with behavior parameterization

*Behavior Parameterization* is a software development pattern that lets you handle frequent requirement changes. In a nutshell, it means taking a block of code and making it available without executing it. This block of code can be called later by other parts of your programs, which means that you can defer the execution of that block of code. You could pass the block of code as an argument to another method that will execute it later. As a result, the method's behavior is parameterized based on that block of code.

The ability to tell method to take multiple behaviors (or strategies) as parameters and use them internally to accomplish different behaviors.(Strategy Design Pattern)

Predicate - The word predicate is often used in mathematics to mean something function-like that takes a values for an argument and returns `true` or `false`.


```java
import java.util.List;

import com.ank.java8.behavior_param.common.Apple;
import com.ank.java8.behavior_param.common.Color;

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

	// Passing behavior in-line. Lambdas in Action!
	List<Apple> greenApples = filterApples(list, (apple) -> apple.getColor() == Color.GREEN);

	List<Apple> heavyApples = filterApples(list, (apple) -> apple.getWeight() > 120);


	System.out.println("Green Apples:" + greenApples);

	System.out.println("Heavy Apples:" + heavyApples);
    }
}
```

---
