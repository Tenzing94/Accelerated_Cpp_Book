# Exercise 1-3

## Problem
Is the following program valid? If so, what does it do? If not, why not?
```Cpp
#include <iostream>
#include <string>

int main()
{
    {
        const std::string s = "a string";
        std::cout << s << std::endl;
    }
    {
        const std::string s = "another string";
        std::cout << s << std::endl;
    }
    return 0;
}
```
## Solution
Yes, this program is valid. By making use of the `{ }`, we made two variables with the same name `s`. This program shows how a variable is local to the scope in which it is defined.
