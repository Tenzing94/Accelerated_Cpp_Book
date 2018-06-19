# Exercise 0-10

## Problem
Rewrite the `Hello, world!` program so that a newline occurs everywhere that whitespace is allowed in the program.
## Solution
There are three entities that are not free-form:
1. string literals
2. `#include` _name_
3. `//` _comments_

In the code below, I could not break up `#include <iostream>` and `Hello, world!` into separate lines.

### Code
```Cpp
#include <iostream>

int 
main
(
    )
{
    std
    ::
    cout
    <<
    "Hello, world!"
    <<
    std
    ::
    endl
    ;
  return
    0
    ;

}
```
