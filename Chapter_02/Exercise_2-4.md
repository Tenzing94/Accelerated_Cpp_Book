# Exercise 2-4

## Problem
The framing program writes the mostly blank lines that separate the borders from the greeting one character at a time. Change the program so that it writes all the spaces needed in a single output expression.

## Solution

### Code
```Cpp
/* Note that in addition to making the changes requried by this exericse, 
I also changed the program so that the top and bottom borders also get written 
in a single output expression.

I also changed the program so that we can have different amount of space to 
separate the sides from the greeting than top and bottom of the greeting.
*/
#include <iostream>
#include <string>

// say what standard-library names we use
using std::cin;
using std::cout;
using std::endl;
using std::string;

int main()
{
	// ask for the person's name
	cout << "Please enter your first name: ";

	// read the name
	string name;
	cin >> name;

	// build the message that we intend to write
	const string greeting = "Hello, " + name + "!";

	cout << endl;

	// the number of blanks surrounding the greeting
	cout << "Please enter the amount of horizontal padding you require: ";
	int horizontalPad;
	cin >> horizontalPad;

	cout << "Please enter the amount of vertical padding you require: ";
	int verticalPad;
	cin >> verticalPad;

	// the number of rows and columns to write
	const int rows = verticalPad * 2 + 3;
	const string::size_type cols = greeting.size() + horizontalPad * 2 + 2;

	const string padTopBottom(cols - 2, ' ');//Padding between top/bottom border and greeting
	const string padLeftRight(horizontalPad, ' '); //Padding between left,right border and greeting

	// All the rows
	const string topBottomRow(cols, '*');  //Top and bottom row
	const string greetingRow = "*" + padLeftRight + greeting + padLeftRight + "*";
	const string nonGreetingRow = "*" + padTopBottom + "*"; // Row without greeting

	// write a blank line to separate the output from the input
	cout << endl;

	// write rows 'rows of output'
	// invariant: we have written r rows so far
	for (int r = 0; r != rows; ++r)
	{
		string::size_type c = 0;

		// invariant: we have written c characters so far in the current row
		while (c != cols)
		{
			// are we on the greeting row?
			if (r == verticalPad + 1)
			{
				cout << greetingRow;
				c += greetingRow.size();
			}
			// are we on top or bottom row?
			else if (r == 0 || r == rows - 1)
			{
				cout << topBottomRow;
				c += topBottomRow.size();
			}
			else 
			{
				cout << nonGreetingRow;
				c += nonGreetingRow.size();
			}
		}

		cout << endl;
	} 

	return 0;
}
```
NOTE: One downside to the code above is that I'm using variables `topBottomRow` `greetingRow` `nonGreetingRow` to store the strings that will be printed on the screen. On the previous exercise, we only had one string,`greeting`, while the rest of the frame was built and displayed on the screen (but not stored on a variable). Not a big deal, but something to keep in mind.
