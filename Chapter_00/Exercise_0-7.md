# Exercise 0-7

## Problem
What about this one?
```Cpp
#include <iostream>
int main()
{
    /* This is a comment that extends over several lines
       because it uses /* and */ as its starting and ending delimiters */
       std::cout << "Does this work?" << std::endl;
       return 0;
}
```

## Solution
No. This is not a valid program.

Anything in between `/*  */` is a comment. In the code above, the second `/*` is part of the comment. 

`as its starting and ending delimiters */` is not part of the comment.
