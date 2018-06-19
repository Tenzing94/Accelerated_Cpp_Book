# Exercise 0-5

## Problem
Is this a valid program? Why or why not?
```Cpp
#include <iostream>
int main() std::cout << "Hello, world!" << std::endl;
```



## Solution
No. This is not a valid C++ program.

There are two things wrong with the code above.
1. All functions in C++ must include curly `{` `}` braces at the beginning and the end of the function. The braces tell the implementation to treat whatever appears between them as a unit.
2. A `return` statement is missing. While a `return` statement is not strictly necessary for the `main` function, it is good practice to use it.
