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

### Second Program (x.x/xx) - //
