Code Review
---

**Peer code reviews are the single biggest thing you can do to improve your code.**

# Basics

- **Formatting**: Where are the spaces and line breaks? Are they using tabs or spaces? How are the curly braces laid out?

- **Style**: Are the variables/parameters declared as final? Are method variables defined close to the code where they’re used or at the start of the method?

- **Naming**: Do the field/constant/variable/param/class names conform to standards? Are the names overly short?

- **Test coverage**: Is there a test for this code?

These are all valid things to check – you want to minimise context switching between different areas of code and reduce cognitive load, so the more consistent your code looks, the better.

However, having humans looking for these is probably not the best use of time and resources in your organisation, as many of these checks can be automated. There are plenty of tools that can ensure that your code is consistently formatted, that standards around naming and the use of the final keyword are followed, and that common bugs caused by simple programming errors are found.

--- 

# What should you look for?

## Design

- How does the new code fit with the overall architecture?

- Does the code follow SOLID principles, Domain Driven Design and/or other design paradigms the team favours?

- What design patterns are used in the new code? Are these appropriate?

- If the codebase has a mix of standards or design styles, does this new code follow the current practices? Is the code migrating in the correct direction, or does it follow the example of older code that is due to be phased out?

- Is the code in the right place? For example, if the code is related to Orders, is it in the Order Service?

- Could the new code have reused something in the existing code? Does the new code provide something we can reuse in the existing code? Does the new code introduce duplication? If so, should it be refactored to a more reusable pattern, or is this acceptable at this stage?

- Is the code over-engineered? Does it build for reusability that isn’t required now? How does the team balance considerations of reusability with YAGNI?

## Readability & Maintainability

Do the names (of fields, variables, parameters, methods and classes) actually reflect the thing they represent?

Can I understand what the code does by reading it?

Can I understand what the tests do?

Do the tests cover a good subset of cases? Do they cover happy paths and exceptional cases? Are there cases that haven’t been considered?

Are the exception error messages understandable?

Are confusing sections of code either documented, commented, or covered by understandable tests (according to team preference)?

## Functionality

Does the code actually do what it was supposed to do? If there are automated tests to ensure correctness of the code, do the tests really test the code meets the agreed requirements?

Does the code look like it contains subtle bugs, like using the wrong variable for a check, or accidentally using an `and` instead of an `or`?

## Have you thought about…?

Are there potential security problems with the code?

Are there regulatory requirements that need to be met?

For areas that are not covered with automated performance tests, does the new code introduce avoidable performance issues, like unnecessary calls to a database or remote service?

Does the author need to create public documentation, or change existing help files?

Have user-facing messages been checked for correctness?

Are there obvious errors that will stop this working in production? Is the code going to accidentally point at the test database, or is there a hardcoded stub that should be swapped out for a real service?

---

# Tests

## Are there tests for this new/amended code?

It would be rare that new code, whether a bug fix or new feature, wouldn’t need a new or updated test to cover it. Even changes for “non-functional” reasons like performance can frequently be proved via a test. If there are no tests included in the code review, as a reviewer the first question you should ask is “why not?”.

## Do the tests at least cover confusing or complicated sections of code?

One step beyond simply “is there a test?”, is to answer the question “is the important code actually covered by at least one test?“.

Checking test coverage is certainly something we should be automating. But we can do more than just check for specific percentages in our coverage, we can use coverage tools to ensure the correct areas of code are covered.

## Can I understand the tests?

Having tests that provide adequate coverage is one thing, but if I, as a human, can’t understand the tests, they have limited use – what happens when they break? It’ll be hard to know how to fix them.

## Do the tests match the requirements?
Here’s an area that really requires human expertise. Whether the requirements being met by the code under review are encoded in some formal document, on a piece of card in a user story, or contained in a bug raised by a user, the code being reviewed should relate to some initial requirement.

The reviewer should locate the original requirements and see if:

1. The tests, whether they’re unit, end-to-end, or something else, match the requirements. For example, if the requirements are “should allow the special characters ‘#’, ‘!’ and ‘&’ in the password field”, there should be a test using these values in the password field. If the test uses different special characters then it’s not proving the code meets the criteria.

2. The tests cover all the criteria mentioned. In our example of special characters, the requirements might go on to say “…and give the user an error message if other special characters are used”. Here, the reviewer should be checking there’s a test for what happens when an invalid character is used.


tbc...
https://blog.jetbrains.com/upsource/2015/08/03/what-to-look-for-in-a-code-review-tests/






















