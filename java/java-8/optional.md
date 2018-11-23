# Using Optional as a better alternative to null
---

`NullPointerException` - We examine a field of an object, perhaps to determine whether its value is one of two expected forms, only to instead find we're examining not an object but a null pointer that promptly raise that annoying `NullPointerException`

## Problems with null

- It's a source of error. `NullPointerException` is by far the most common exception in Java.

- It bloats your code. It worsens readability by making it necessary to fill your code with often deeply nested `null` checks.

- It creates a hole in the type system. `null` carries no type or other information, meaning it can be assigned to any reference type. This is a problem because, when it's propagated to another part of the system, you have no idea what null was initially supposed to be.

## Optional class

Using optionals consistently disambiguates beyond any doubt the case of a value that can be structurally missing from the case of a values that's absent only because of a bug in your algorithm or a problem in your data.

## Patterns for adopting Optional

### Creating Optional Objects

to be continued...


















---
