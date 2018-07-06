# Exercise 2-5

## Problem
Write a set of "*" characters so that they form a square, a rectangle, and a triangle.

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
	int selectedShape;
	bool correctShapeSelectedFlag = false;

	// Keep asking the user to input 1, 2, or 3
	do{
	cout << "Which object would you like me to draw?" << endl;
	cout << "1. Square" << endl;
	cout << "2. Rectangle" << endl;
	cout << "3. Triangle" << endl;
	cout << "Type in the number corresponding to the shapes listed (1, 2, or 3): ";
	
	cin >> selectedShape;

	cout << endl;

	if (selectedShape == 1 || selectedShape == 2 || selectedShape == 3)
		correctShapeSelectedFlag = true;
	else
		cout << "PLEASE ENTER 1, 2, or 3." << endl << endl;


	}
	while (correctShapeSelectedFlag == false);


	// Entering the dimensions of the shape
	int shapeHeight; 
	int shapeWidth;

	if (selectedShape == 1) // Square
	{
		cout << "Please enter the height of the square: ";
		cin >> shapeHeight;

		shapeWidth = shapeHeight; // Square has same length and width		
	}
	else if (selectedShape == 2) // Rectangle
	{
		cout << "Please enter the height of the rectangle: ";
		cin >> shapeHeight;
		cout << "Please enter the width of the rectangle: ";
		cin >> shapeWidth;
	}
	else // Triangle
	{
		cout << "Please enter the height of the triangle: ";
		cin >> shapeHeight;

		shapeWidth = shapeHeight*2 - 1;
	}

	cout << endl;

	// rows and cols values based on the dimension of the shape
	const int rows = shapeHeight;
	const int cols = shapeWidth;

	for(int r = 0; r != rows; ++r)
	{
		int c = 0;

		while (c != cols) // write one column
		{
			if (selectedShape == 1 || selectedShape == 2) // Square or Rectangle
			{
				cout << "*";
				++c;
			}
			else // Triangle
			{
				if ((c >= ((cols-1)/2)-r) && (c <= ((cols-1)/2)+r ))
				{
					cout << "*";
				}
				else 
				{
					cout << " ";
				}
				++c;
			}

		}
		cout << endl; // go to the next row after on column is finished

	}

	return 0;
}
```
