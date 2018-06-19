# Exercise 0-4

## Problem
Write a program that, when run, writes the `Hello, world!` program as its output.

## Solution
### Code
```Cpp
#include <iostream>

int main()
{
	std::cout << "#include <iostream>" << std::endl << std::endl;
	std::cout << "int main()" << std::endl;
	std::cout << "{" << std::endl;
	std::cout << "\t std::cout << \"Hello, world!\" << std::endl;" << std::endl;
	std::cout << "\t return 0;" << std::endl;
	std::cout << "}" << std::endl;
	return 0;
}
```
