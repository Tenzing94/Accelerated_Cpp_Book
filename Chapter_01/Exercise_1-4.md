# Exercise 1-4

## Problem
What about this one? What if we change `}}` to `};}` in the third line from the end?
```Cpp
#include <iostream>
#include <string>

int main()
{
	{ 
		const std::string s = "a string";
		std::cout << s << std::endl;

		{
			const std::string s = "another string";
			std::cout << s << std::endl; 
		}}
	return 0;
}
```

## Solution
Yes, the code above is valid. NOTE that the two `s` objects are not the same (even though they have the same name and type). 

If we change `}}` to `};}`, the program is still valid. 

The `;` is simply a null statement.Lets look at the code:
```Cpp
#include <iostream>
#include <string>

int main()
{
	{ 
		const std::string s = "a string";
		std::cout << s << std::endl;

		{
			const std::string s = "another string";
			std::cout << s << std::endl; 
		}
		; // null statement
	}
	return 0;
}
```
