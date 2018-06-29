# Exercise 1-2

## Problem
Are the following definitions valid? Why or why not?

`const std::string exclam = "!";`

`const std::string message = "Hello" + ", world" + exclam;`

## Solution
The first definition is valid.

The second definition is NOT valid. Remember that the concatenate operator `+` is **left associative**.

This means that the second definition is actually `const std::string message = (  (  "Hello" + ", world"  ) + exclam  );`

Remember that one of the operands must be a `std::string` object. Since we have `string literal + string literal` scenario, the definition is NOT valid. 
