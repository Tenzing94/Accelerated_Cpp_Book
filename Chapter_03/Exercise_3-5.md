# Exercise 3-5

## Problem
Write a program that will keep track of grades for several students at once. The program could keep two `vector`s in sync: The first should hold the student’s names, and the second the final grades that can be computed as input is read. For now, you should assume a fixed number of homework grades. We’ll see in [4.1.3/56] how to handle a variable number of grades intermixed with student names.

## Solution

Note: In this program, we will not bother with final and midterm grades. The program will take a fixed number of homework grades per student as input, and output the student's name along with his/her mean (average) homework score.

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

		cout << "Please enter " << num_of_hw << " homeworks: ";

		double total_score = 0;
		double homework_score;

		for (vec_sz i = 0; i != num_of_hw; ++i)
		{
			cin >> homework_score;
			total_score += homework_score;
		}
		studentMeanGrade.push_back(total_score / num_of_hw);

		cout << "Either enter another student's name, or exit via Control+D.";
		cout << endl;
	}

	cout << "-------------------------------------------------------------" << endl;
	cout << "Here are the names and average (mean) grades of the students." << endl;
	cout << "-------------------------------------------------------------" << endl;

	streamsize prec = cout.precision();
	for (vec_sz i = 0; i != studentNames.size(); ++i)
	{
		cout << "The mean homework grade of student with name " << studentNames[i] 
		<< " is " << setprecision(3) << studentMeanGrade[i] << endl;
	}
	setprecision(prec);

	return 0;

}
```
