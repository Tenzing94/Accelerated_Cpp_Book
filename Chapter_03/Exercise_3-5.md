# Exercise 3-5

## Problem
Write a program that will keep track of grades for several students at once. The program could keep two `vector`s in sync: The first should hold the student’s names, and the second the final grades that can be computed as input is read. For now, you should assume a fixed number of homework grades. We’ll see in [4.1.3/56] how to handle a variable number of grades intermixed with student names.

## Solution

### Code
```Cpp
#include <iomanip> // for setprecision
#include <ios> // for streamsize
#include <iostream>
#include <string>
#include <vector>

using std::cin;
using std::cout;
using std::endl;
using std::setprecision;
using std::streamsize;
using std::string;
using std::vector;

int main()
{
	typedef vector<double>::size_type vec_sz;

	// How many hw per student?
	const vec_sz num_of_hw = 3;

	vector<string> studentNames; 
	vector<double> studentMeanGrade; // mean hw grade of each student

	cout << "Please enter the student's name: ";
	string studentName;
	while (cin >> studentName)
	{
		studentNames.push_back(studentName);

		cout << "Please enter the midterm exam grade: ";
		double midterm;
		cin >> midterm;

		cout << "Please enter the final exam grade: ";
		double final;
		cin >> final;

		cout << "Please enter " << num_of_hw << " homeworks: ";

		double total_hw = 0;
		double homework;

		for (vec_sz i = 0; i != num_of_hw; ++i)
		{
			cin >> homework;
			total_hw += homework;
		}

		double final_grade = 0.2 * midterm + 0.4 * final + 0.4 * total_hw / num_of_hw;

		studentMeanGrade.push_back(final_grade);

		cout << "Either enter another student's name, or exit via Control+D.";
		cout << endl;
	}

	cout << "-------------------------------------------------------------" << endl;
	cout << "Here are the names and final grades of the students." << endl;
	cout << "-------------------------------------------------------------" << endl;

	streamsize prec = cout.precision();
	for (vec_sz i = 0; i != studentNames.size(); ++i)
	{
		cout << "The final grade of student with name " << studentNames[i] 
		<< " is " << setprecision(3) << studentMeanGrade[i] << endl;
	}
	setprecision(prec);

	return 0;

}
```
