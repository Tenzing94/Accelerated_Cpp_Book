# Exercise 2-7

## Problem
Write a program to count down from `10` to `-5`.

## Solution

### Code
```Cpp
#include <iostream>

int main()
{
	const int number = 10 - (-5) + 1; // Range [10,-6)
	for (int i = 0, j = 10; i != number; ++i)
	{
		std::cout << j - i << std::endl;
	}
	return 0;
}
```

### Output
```
10
9
8
7
6
5
4
3
2
1
0
-1
-2
-3
-4
-5
```
