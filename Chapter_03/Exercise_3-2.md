# Exercise 3-2

## Problem
Write a program to compute and print the quartiles (that is, the quarter of the numbers with the largest values, the next highest quarter, and so on) of a set of integers.

## Solution
Note: All the credit goes to Johnny Chan for a wonderful explanation of this problem [[Link]](http://mathalope.co.uk/2014/07/18/accelerated-c-solution-to-exercise-3-2/). My implemention (code) is modeled heavily after his implemention.

### Code
```Cpp
#include <algorithm> // for sort, begin, end
#include <iomanip> // for setprecision
#include <ios> // for streamsize
#include <iostream>
#include <string>
#include <vector>

using std::cin;
using std::cout;
using std::endl;
using std::setprecision;
using std::sort;
using std::streamsize;
using std::string;
using std::vector;

int main()
{
	cout << "_________________________________________________________" << endl;
	cout << "This program computes the quartiles of a set of integers." << endl;
	cout << "_________________________________________________________" << endl;

	cout << "Please enter the set of integers: ";

	vector<double> integerSet;
	double x;
	while (cin >> x)
		integerSet.push_back(x);

	typedef vector<double>::size_type vec_sz;
	vec_sz N = integerSet.size();

	if (N == 0) // If there is 0 integers in the set.
	{
		cout << "No integers were provided!" << endl;
		cout << "Program Terminated" << endl;
		return 1;
	}
	else if (N == 1)
	{
		cout << "Only one integer was provided." << endl;
		cout << "Therefore Q1, Q2, Q3 are all " << integerSet[0] << endl;
		return 0;
	}

	// N >= 2. We need to sort them in ascending order
	sort(integerSet.begin(),integerSet.end()); // O(NlogN)

	string datumDistr = "";   // datum distribution profile
    vec_sz indexM, indexML, indexMU; // vector indices
    double median, medianLower, medianUpper;         // quartile values

    if (N % 4 == 0)
    {
    	datumDistr = "[0 0 0]";
        indexM = N / 2;
        indexML = indexM / 2;
        indexMU = indexM + indexML;

        medianLower= (integerSet[indexML] + integerSet[indexML-1]) / 2;
        median = (integerSet[indexM] + integerSet[indexM-1]) / 2;
        medianUpper = (integerSet[indexMU] + integerSet[indexMU-1]) / 2;
    }
    else if (N % 4 == 1)
    {
    	datumDistr = "[0 1 0]";
        indexM = N / 2;
        indexML = indexM / 2;
        indexMU = indexM + indexML + 1;
 
        datumDistr = "[0 0 0]";
        medianLower= (integerSet[indexML] + integerSet[indexML-1]) / 2;
        median = integerSet[indexM];
        medianUpper = (integerSet[indexMU] + integerSet[indexMU-1]) / 2;
    }
    else if (N % 4 == 2)
    {
    	datumDistr = "[1 0 1]";
        indexM = N / 2;
        indexML = indexM / 2;
        indexMU = indexM + indexML;
 
        medianLower = integerSet[indexML];
        median = (integerSet[indexM] + integerSet[indexM-1]) / 2;
        medianUpper = integerSet[indexMU];
    }
    else if (N % 4 == 3)
    {
    	datumDistr = "[1 1 1]";
        indexM = N / 2;
        indexML = indexM / 2;
        indexMU = indexM + indexML + 1;
 
        medianLower = integerSet[indexML];
        median = integerSet[indexM];
        medianUpper = integerSet[indexMU];
    }
    else
    {
    	cout << "There was an unknown error." << endl;
    	cout << "Program Terminated" << endl;
    	return 1;
    }

    streamsize prec = cout.precision();
    cout << "Here are the quartiles of the set of integers that you provided." << endl;
    cout << "Datum Distribution: " << datumDistr << endl;
    cout << "Q1: " << setprecision(3) << medianLower << endl;
    cout << "Q2: " << median << endl;
    cout << "Q3: " << medianUpper << setprecision(prec) << endl;

    return 0;

}
```
