# Exercise 3-4

## Problem
Wrtie a program to report the length of the longest and shortest `string` in its input.

## Solution

### Code
```Cpp
#include <iostream>
#include <vector>
#include <string>

using std::cin;
using std::cout;
using std::endl;
using std::string;
using std::vector;

int main()
{
	cout << "Please enter all of the words, followed by Control+D: ";
    vector<string> words;
    string word;

    while (cin >> word)
        words.push_back(word);

    typedef vector<double>::size_type vec_sz;
    vec_sz size_of_words = words.size();

    unsigned int shortestString, longestString;

    // if no words were entered
    if (size_of_words == 0)
    {
        cout << "No words were entered. Program Terminated." << endl;
        return 1;
    }
    else if (size_of_words == 1)
    {
    	shortestString = longestString = words[0].size();
    	cout << "The shortest string has length " << shortestString << endl;
    	cout << "The longest string has length " << longestString << endl;
    	return 0;
    }
    else
    {
    	 // initialize the first element (index 0) to be the longest and shortest string
    	shortestString = longestString = words[0].size();

    	// index starts at 1 because vector with index 0 has already been initialized
    	for (vec_sz index = 1; index != size_of_words; ++index)
    	{
    		if (words[index].size() > longestString)
    			longestString = words[index].size();

    		if (words[index].size() < shortestString)
    			shortestString = words[index].size();
    	}
    	cout << "The shortest string has length " << shortestString << endl;
    	cout << "The longest string has length " << longestString << endl;
    }

    return 0;
}
```
