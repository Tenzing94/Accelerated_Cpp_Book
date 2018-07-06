# Exercise x-x

## Problem
Write a program to generate the product of the numbers in the range `[1, 10)`.

## Solution

### Code
```Cpp
#include <iostream>

int main()
{
	const int range = 10 - 1; // [1, 10)

	int product = 1;

	for (int i = 0; i != range; ++i) // loop 9 times
	{
		product *= (i + 1);
	}
	std::cout << "The product is: " << product << std::endl;
}
```

### Output
```
The product is: 362880
```
