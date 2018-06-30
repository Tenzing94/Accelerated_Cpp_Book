# Exercise 1-6

## Problem
What does the following program do if, when it asks you for input, you type two names (for example, Samuel Beckett)? Predict the behavior before running the program, then try it.

### Code
```Cpp
#include <iostream>
#include <string>

int main()
{
	std::cout << "What is your name? ";
	std::string name;
	std::cin >> name;
	std::cout << "Hello, " << name 
	          << std::endl << "And what is yours? ";
	std::cin >> name;
	std::cout << "Hello, " << name 
	          << "; nice to meet you too!" << std::endl;
	return 0;
}
```

## Solution
When we write `Samuel Beckett`, two words get stored in the **buffer**. Remember that inside a buffer, words are separated by a blank space. 

1. So, after the first `std::cin >> name;`, there are two words in the buffer.
2. In the next line, the word `Samuel` gets removed from the buffer and is displayed in your computer. The buffer now has one word `Beckett`.
3. In the next line, `std::cin >> name;` is ignored because the buffer already has a word.
4. In the next line, `Beckett` gets removed from the buffer and is displayed in your computer.
