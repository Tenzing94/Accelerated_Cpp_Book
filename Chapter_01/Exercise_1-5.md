# Exercise 1-5

## Problem
Is this program valid? If so, what does it do? If not, say why not, and rewrite it to be valid.

### Code
```Cpp
#include <iostream>
#include <string>

int main()
{
	{
		std::string s = "a string";
		{
			std::string x = s + ", really";
			std::cout << s << std::endl;
		}
		std::cout << x << std::endl;
	}
	return 0;
}
```
## Solution
No. The program above is not valid. `x` is being used outside of the scope in which it is defined.

We can fix this program by simply getting rid of the inner most `{}`.

### Code
```Cpp
#include <iostream>
#include <string>

int main()
{
	{
		std::string s = "a string";
		std::string x = s + ", really";
		std::cout << s << std::endl;
		std::cout << x << std::endl;
	}
	return 0;
}
```
