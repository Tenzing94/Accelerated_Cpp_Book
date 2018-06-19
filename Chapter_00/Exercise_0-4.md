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
or
```Cpp
#include <iostream>

int main()
{
	std::cout << "#include <iostream>\n\n";
	std::cout << "int main()\n";
	std::cout << "{\n";
	std::cout << "\t std::cout << \"Hello, world!\" << std::endl;\n";
	std::cout << "\t return 0;\n";
	std::cout << "}\n";
	return 0;
}
```
