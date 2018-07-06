# Exercise 2-9

## Problem
Write a program that asks the user to enter two numbers and tells the user which number is larger than the other.

## Solution

### Code
```Cpp
#include <iostream>
#include <string>

using std::cin;
using std::cout;
using std::endl;
using std::string;

int main()
{
	cout << "This program takes two numbers as input and computes which " 
		 << "number is larger than the other." << endl;
		 
	cout << "Please enter the first number: ";
	int firstNum;
	cin >> firstNum;

	cout << "Please enter the second number: ";
	int secondNum;
	cin >> secondNum;

	if (firstNum > secondNum)
		cout << "The first number is larger." << endl;
	else if (firstNum < secondNum)
		cout << "The second number is larger." << endl;
	else
		cout << "The numbers are equal" << endl;

}
```
