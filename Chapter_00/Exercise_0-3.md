# Exercise 0-3

## Problem
The string literal `"\t"` represents a tab character; different C++ implementations display tabs in different ways. Experiment with your implementation to learn how it treats tabs. 
## Solution

### Code
```Cpp
#include <iostream>

int main()
{
	std::cout << "One \t Tab" << std::endl;
	std::cout << "Two \t\t Tabs" << std::endl;
	std::cout << "Three \t\t\t Tabs" << std::endl;
	return 0;
}
```
