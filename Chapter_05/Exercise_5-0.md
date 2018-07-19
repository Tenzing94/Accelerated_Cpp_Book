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


### Third Program (5.8.1/92) - Framing a picture, vertical concatenation, and horizontal concatenation.

The program below takes in a paragraph, storing each line as a string in a vector, and then outputs the following:
1. The paragraph
2. The paragraph inside a frame
3. The paragraph and the framed paragraph, concatenated vertically
4. The paragraph and the framed paragraph, concatenated horizontally

NOTE: I did not bother splitting the program into multiple files. 

```Cpp
#include <iostream> //getline
#include <string>
#include <vector> 

using std::cin;
using std::cout;
using std::endl;
using std::getline;
using std::max;
using std::string;
using std::vector;

// output the vector on the console
void vec_output(const vector<string>& v)
{
	for (vector<string>::size_type i = 0; i != v.size(); ++i)
		cout << v[i] << endl;

}

// find the length of the longest string in the vector
string::size_type width(const vector<string>& v)
{
	string::size_type maxlen = 0;
	for (vector<string>::size_type i = 0; i != v.size(); ++i)
		maxlen = max(maxlen, v[i].size());
	return maxlen;
}

// this function will produce a new vector, with the frame around it
vector<string> frame(const vector<string>& v) 
{
	vector<string> ret;
	string::size_type maxlen = width(v);
	string border(maxlen + 4, '*');

	// write the top border
	ret.push_back(border);

	// write each interior row, bordered by an asterisk and a space
	for (vector<string>::size_type i = 0; i != v.size(); ++i)
	{
		ret.push_back("* " + v[i] + string(maxlen - v[i].size(), ' ')
			+ " *");
	}

	// write the bottom border
	ret.push_back(border);
	return ret;
}

// takes two vectors of type string and concatnates them vertically
vector<string> vcat (const vector<string>& top, const vector<string>& bottom)
{
	// copy the top picture 
	vector<string> ret = top;

	// copy the entire bottom picture
	ret.insert(ret.end(), bottom.begin(), bottom.end());

	return ret;
}

// takes two vectors of type string and concatnates them horizontally
vector<string> hcat(const vector<string>& left, const vector<string>& right)
{
	vector<string> ret;

	// add 1 to leave a space between pictures
	string::size_type width1 = width(left) + 1;

	// indices to look at elements from left and right respactively
	vector<string>::size_type i = 0, j = 0;

	// continue until we've seen all rows from both pictures
	while (i != left.size() || j != right.size())
	{
		// construct new string to hold characters from both pictures
		string s;

		// copy a row from the left-hand side, if there is one
		if (i != left.size())
			s = left[i++]; // assign left[i] to s, and then increment i

		// pad to full width
		s += string(width1 - s.size(), ' ');

		// copy a row from the right-hand side, if there is one
		if (j != right.size())
			s += right[j++];

		// add s to the picture we're creating
		ret.push_back(s);
	}
	return ret;
}

int main()
{
	string s;            // line
    vector<string> p;    // paragraph
 
 	cout << "Please enter a paragraph." << endl;

    // each line will be an object in the vector p
    while (getline(cin, s))
        p.push_back(s);

    cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    cout << "Here is the paragraph that you provided." << endl;
    cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    vec_output(p);

    cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    cout << "Here is the framed paragraph." << endl;
    cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    vec_output(frame(p));

    cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    cout << "Here are the original and framed paragraph, concatnated vertically." << endl;
    cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    vec_output(vcat(p, frame(p)));

    cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    cout << "Here are the original and framed paragraph, concatnated horizontally." << endl;
    cout << "~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" << endl;
    vec_output(hcat(p, frame(p)));

    return 0;
}
```
