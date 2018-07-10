# Exercise 3-3

## Problem
Write a program to count how many times each distinct word appears in its input.

## Solution

### Code
```Cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

using std::cin;
using std::cout;
using std::endl;
using std::sort;
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

    // if no words were entered
    if (size_of_words == 0)
    {
        cout << "No words were entered. Program Terminated." << endl;
        return 1;
    }

    // sort the words
    sort(words.begin(), words.end());

    // print out the sorted words
    cout << "--------------------------------------------------------" << endl;
    cout << "Here are the words that you provided, in ascending order: ";
    for (vec_sz i = 0; i != size_of_words; ++i)
        cout << " " << words[i];
    cout << endl;
    cout << "--------------------------------------------------------" << endl;

    int wordCount = 1;
    for (vec_sz i = 0; i != size_of_words; ++i)
    {
        // checking that [i + 1] is still inside the vector
        if (i + 1 < size_of_words)
        {
            if (words[i] == words[i + 1])
            {
                ++wordCount;
            } 
            else 
            {
                cout << words[i] << " count: " << wordCount << endl;
                wordCount = 1; // reset the word count
            }
        } 
        else 
        {
            // this is for the last element of the vector
            cout << words[i] << " count: " << wordCount << endl;
        }
    }
    return 0;
}
```
