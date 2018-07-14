# Exercise 4-0

## Problem
Compile, execute, and test the programs in this chapter.

## Solution

### First Program (4.1.5/59) - This program calcuates a single student's grade
```Cpp
#include <algorithm>
#include <iomanip> // for setprecision
#include <ios> // for streamsize
#include <iostream>
#include <stdexcept>
#include <string>
#include <vector>

using std::cin;
using std::cout;
using std::domain_error;
using std::endl;
using std::istream;
using std::setprecision;
using std::sort;
using std::streamsize;
using std::string;
using std::vector;

// compute the median of a vector<double>
// note that calling this function copies the entire arument vector
double median(vector<double> vec)
{
	typedef vector<double>::size_type vec_sz;

	vec_sz size = vec.size();
	if (size == 0)
		throw domain_error("median of an empty vector");

	sort(vec.begin(), vec.end());

	vec_sz mid = size/2;

	return size % 2 == 0 ? (vec[mid] + vec[mid-1]) / 2 : vec[mid];
}

// compute a student's overall grade from midterm and final exam grades and hw
double grade(double midterm, double final, double homework)
{
	return 0.2 * midterm + 0.4 * final + 0.4 * homework;
}

// compute a student's overall grade from mindterm and final exam grades
// and vector of homework grades.
// this function does not copy its argument, because median does so for us.
double grade(double midterm, double final, const vector<double>& hw)
{
	if (hw.size() == 0)
		throw domain_error("student has done no homework");
	return grade(midterm, final, median(hw));
}

// read homework grades from an input stream into a vector<double>
istream& read_hw(istream& in, vector<double>& hw)
{
	if (in) {
		// get rid of previous contents
		hw.clear();

		// read homework grades
		double x;
		while (in >> x)
			hw.push_back(x);

		// clear the stream so that input will work for the next student
		in.clear();
	}
	return in;
}

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
	cout << "Enter all your homework grades followed by end-of-file: ";

	vector<double> homework;

	// read the homework grades
	read_hw(cin, homework);

	// compute and generate the final grade, if possible
	try 
	{
		double final_grade = grade(midterm, final, homework);
		streamsize prec = cout.precision();
		cout << "Your final grade is " << setprecision(3) 
		<< final_grade << setprecision(prec) << endl;
	}
	catch (domain_error)
	{
		cout << endl << "You must enter your grades. Please try again." << endl;
		return 1;
	}
	
	return 0;
}
```

### Second Program (4.5/70) - This program calcuates multiple students' grades. This program is separated into multiple files

#### Student_info.h
```Cpp
#ifndef GUARD_Student_info
#define GUARD_Student_info

// Student_info.h header file
#include <iostream>
#include <string>
#include <vector>

struct Student_info {
	std::string name;
	double midterm, final;
	std::vector<double> homework;
};

bool compare(const Student_info&, const Student_info&);

std::istream& read(std::istream&, Student_info&);

std::istream& read_hw(std::istream&, std::vector<double>&);

#endif
```

#### Student_info.cpp
```Cpp
// source file for Student_info related functions
#include "Student_info.h"

using std::istream;
using std::vector;

bool compare(const Student_info& x, const Student_info& y)
{
	return x.name < y.name;
}

istream& read(istream& is, Student_info& s)
{
	// rad and store the student's name and midterm and final exam grades
	is >> s.name >> s.midterm >> s.final;

	read_hw(is, s.homework); // read and store all the student's homework grades
	return is;
}

// read homework grades from an input stream into a 'vector'
istream& read_hw(istream& in, vector<double>& hw)
{
	if (in) {
		// get rid of previous contents
		hw.clear();

		// read homework grades
		double x;
		while (in >> x)
			hw.push_back(x);

		// clear the stream so that input will work for the next student
		in.clear();
	}
	return in;
}
```

#### median.h
```Cpp
#ifndef GUARD_median_h
#define GUARD_median_h

// median.h header file
#include <vector>

double median(std::vector<double>);

#endif
```

#### median.cpp
```Cpp
// source file for the median function

#include <algorithm> // sort
#include <stdexcept> // domain_error
#include <vector> 
#include "median.h"

using std::domain_error;
using std::sort;
using std::vector;

// compute the median of a vector<double>
// note that calling this function copies the entire argument vector
double median(vector<double> vec)
{
	typedef vector<double>::size_type vec_sz;

	vec_sz size = vec.size();
	if (size == 0)
		throw domain_error("median of an empty vector");

	sort(vec.begin(), vec.end());

	vec_sz mid = size/2;

	return size % 2 == 0 ? (vec[mid] + vec[mid-1]) / 2 : vec[mid];
}
```

#### grade.h
```Cpp
#ifndef GUARD_grade_h
#define GUARD_grade_h

// grade.h
#include <vector>
#include "Student_info.h"

double grade(double, double, double);

double grade(double, double, const std::vector<double>&);

double grade(const Student_info&);

#endif
```

#### grade.cpp
```Cpp
#include <stdexcept>
#include <vector>
#include "grade.h"
#include "median.h"
#include "Student_info.h"

using std::domain_error; 
using std::vector;

// compute a student's overall grade from midterm and final exam grades and hw
double grade(double midterm, double final, double homework)
{
	return 0.2 * midterm + 0.4 * final + 0.4 * homework;
}

// compute a student's overall grade from midterm and final exam grades
// and vector of homework grades.
// this function does not copy its argument, because median does so for us.
double grade(double midterm, double final, const vector<double>& hw)
{
	if (hw.size() == 0)
		throw domain_error("student has done no homework");
	return grade(midterm, final, median(hw));
}

double grade(const Student_info& s)
{
	return grade(s.midterm, s.final, s.homework);
}
```

#### Ex4-0.cpp
```Cpp
#include <algorithm>
#include <iomanip> // for setprecision
#include <ios> // for streamsize
#include <iostream>
#include <stdexcept>
#include <string>
#include <vector>
#include "grade.h"
#include "Student_info.h"

using std::cin;
using std::cout;
using std::domain_error;
using std::endl;
using std::max;
using std::setprecision;
using std::sort;
using std::streamsize;
using std::string;
using std::vector;

int main()
{
	vector<Student_info> students;
	Student_info record;
	string::size_type maxlen = 0; // the length of the longest name

	// read and store all the students data.
	// Invariant: students contains all the student records read so far
	// maxlen contains the length of the longest name in students
	while (read(cin, record)) 
	{
		// find length of longest name
		maxlen = max(maxlen, record.name.size());
		students.push_back(record);
	}

	// alphabetize the student records
	sort(students.begin(), students.end(), compare);

	// write the names and grades
	for (vector<Student_info>::size_type i = 0; i != students.size(); ++i)
	{
		// write the name, padded on the right to maxlen + 1 characters
		cout << students[i].name << string(maxlen + 1 - students[i].name.size(), ' ');

		// compute and write the grade
		try 
		{
			double final_grade = grade(students[i]);
			streamsize prec = cout.precision();
			cout << setprecision(3) << final_grade << setprecision(prec);
		}
		catch (domain_error e) {
			cout << e.what();
		}
		cout << endl;
	}
	return 0;
}

```
