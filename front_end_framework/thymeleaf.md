# thymeleaf
---

## HTML5-valid

Using non-standard attribute in the th:* form are not allowed by the HTML5 specification. If we want to make this template HTML5-valid? Easy: switch to Thymeleaf’s data attribute syntax, using the `data-` prefix for attribute names and hyphen `(-)` separators instead of semi-colons `(:)`

```html
<!DOCTYPE html>

<html>

  <head>
 <title>Good Thymes Virtual Grocery</title>
 <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
 <link rel="stylesheet" type="text/css" media="all"
  href="../../css/gtvg.css" data-th-href="@{/css/gtvg.css}" />
  </head>

  <body>

<p data-th-text="#{home.welcome}">Welcome to our grocery store!</p>

  </body>

</html>
```

## Unescaped Text

 If we want Thymeleaf to respect our HTML tags and not escape them, we will have to use a different attribute: `th:utext` (for “unescaped text”):

```html
<p th:utext="#{home.welcome}">Welcome to our grocery store!</p>
```

---

## Standard Expression Syntax

**the Standard Expression features:**

Simple expressions:

- Variable Expressions: `${...}`
- Selection Variable Expressions: `*{...}`
- Message Expressions: `#{...}`
- Link URL Expressions: `@{...}`
- Fragment Expressions: `~{...}`

Literals

- Text literals: 'one text', 'Another one!',…
- Number literals: 0, 34, 3.0, 12.3,…
- Boolean literals: true, false
- Null literal: null
- Literal tokens: one, sometext, main,…

Text operations:

- String concatenation: +
- Literal substitutions: |The name is ${name}|

Arithmetic operations:

- Binary operators: `+, -, *, /, %`
- Minus sign (unary operator): -

Boolean operations:

- Binary operators: and, or
- Boolean negation (unary operator): !, not

Comparisons and equality:

- Comparators: >, <, >=, <= (gt, lt, ge, le)
- Equality operators: ==, != (eq, ne)

Conditional operators:

- If-then: (if) ? (then)
- If-then-else: (if) ? (then) : (else)
- Default: (value) ?: (defaultvalue)

Special tokens:

- No-Operation: _


```
'User is of type ' + (${user.isAdmin()} ? 'Administrator' : (${user.type} ?: 'Unknown'))

```
---

## Boolean literals

The boolean literals are true and false. For example:

```
<div th:if="${user.isAdmin()} == false"> ...
```

In this example, the `== false` is written outside the braces, and so it is Thymeleaf that takes care of it.
