# Exercise 1-1

## Problem
Are the following definitions valid? Why or why not?

`const std::string hello = "Hello";`

`const std::string message = hello + ", world" + "!";`

## Solution
The first definition is valid.

The second definition is also valid. Remember that the concatenate operator `+` is **left associative**.

This means that the second definition is actually `const std::string message = (  (  hello + ", world"  ) + "!"  );`

Remember that one of the operands must be a `std::string` object. As long as we don't encounter a `string literal + string literal` scenario, the definition is valid. 
