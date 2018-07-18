# Exercise 5-0

## Problem
Compile, execute, and test the programs in this chapter.

## Solution

### First Program (5.5/85) - Extracting students with failing grades from the list. This is an extension to the Second Program (4.5/70) from Exercise 4-0.

NOTE: In the code below, I only wrote the two functions as defined in the book. If you want to make use of the functions below in a program, please take the Second Program (4.5/70) from Exercise 4-0 and make the appropriate changes in order to accomodate the functions below. The main change should be that the vectors should be changed to lists. 

```Cpp

bool fgrade(const Student_info& s)
{
	return grade(s) < 60;
}

list<Student_info> extract_fails(list<Student_info>& students)
{
	list<Student_info> fail;
	list<Student_info>::iterator iter = students.begin();

	while (iter != students.end()) 
	{
		if (fgrade(*iter))
		{
			fail.push_back(*iter);
			iter = students.erase(iter);
		}
		else
			++iter;
	}
	return fail;
}
```

----------------------------------------------------------------------------------------------------------

### Second Program (5.7/90) - Spliting a line of text (string) into individual words and storing them in a vector.

split.h
```Cpp
#ifndef GUARD_split_h
#define GUARD_split_h
 
#include <vector>
#include <string>
 
std::vector<std::string> split(const std::string&);
 
#endif // GUARD_SPLIT_H
```

split.cpp
```Cpp
#include <cctype>    // for isspace
#include <string>
#include <vector>
#include "split.h"

using std::isspace;
using std::string;
using std::vector;

vector<string> split(const string& s)
{
    vector<string> ret;
    typedef string::size_type string_size;

    string_size i = 0;
 
    // invariant: we have processed characters [original value of i, i)
    while (i != s.size() )
    {
        // ignore leading blanks
        // invariant: characters in range [original i, current i) are all spaces
        while (i != s.size() && isspace(s[i]))
            ++i;
 
        // find end of next word
        string_size j = i;
 
        // invariant: none of the characters in range [original j, current j) is a space
        while (j != s.size() && !isspace(s[j]))
            ++j;
 
        // if we found some nonwhitespace characters
        if (i != j)
            // copy from s starting at i and taking j - i chars
            ret.push_back(s.substr(i, j - i));
            i = j;
    }
    return ret;
}
```

main.cpp
```Cpp
#include <iostream> // getline
#include <vector>
#include <string>
#include "split.h"   // split

using std::cin;
using std::cout;
using std::endl;
using std::getline;
using std::string;
using std::vector;

int main()
{
    string s;
 
    // read and split each line of input
    while (getline(cin, s))
    {
        vector<string> v = split(s);
 
        // write each word in v
        for (vector<string>::size_type i = 0; i != v.size(); ++i)
            cout << v[i] << endl;
    }
    return 0;
```

----------------------------------------------------------------------------------------------------------


### Third Program (x.x/xx) - //
