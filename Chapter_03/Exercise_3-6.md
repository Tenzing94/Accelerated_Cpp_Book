# Exercise 3-6

## Problem
The average-grade computation in [3.1/36] might divide by zero if the student didn’t enter any grades. Division by zero is undefined in C++, which means that the implementation is permitted to do anything it likes. What does your C++ implementation do in this case? Rewrite the program so that its behavior does not depend on how the implementation treats division by zero.

## Solution
When I ran the program from [3.1/36] and supplied it with no homework grades, the result was `nan`. This stands for `not a number`. 

To resolve this, I added a simple `if` statement to check if `count == 0`. If so, the program will terminate.

### Code
```Cpp
#include <iomanip> // for setprecision
#include <ios> // for streamsize
#include <iostream>
#include <string>

using std::cin;
using std::cout;
using std::endl;
using std::setprecision;
using std::string;
using std::streamsize;

int main()
{
	// ask for and read the student's name
	cout << "Please enter your first name: ";
	string name;
	cin >> name;
	cout << "Hello, " << name << "!" << endl;

	// ask for and read the midterm and final grades
	cout << "Please enter your midterm and final exam grades: ";
	double midterm, final;
	cin >> midterm >> final;

	// ask for the homework grades
	cout << "Enter all your homework grades, "
		"followed by end-of-file: ";

	// the number and sum of grades read so far
	int count = 0;
	double sum = 0;

	// a variable into which to read
	double x;

	// invariant:
	// we have read 'count' grades so far, and 
	// sum 'is the sum of the first count grades'
	while (cin >> x) {
		++count;
		sum += x;
	}

	if (count == 0)
	{
		cout << "No homework grades were supplied. Program terminated." << endl;
		return 1;
	}

	// write the result 
	streamsize prec = cout.precision();
	cout << "Your final grade is " << setprecision(3) 
		<< 0.2 * midterm + 0.4 *final + 0.4 * sum / count
		<< setprecision(prec) << endl;

	return 0;

}
```
