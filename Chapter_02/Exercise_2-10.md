# Exercise 2-10

## Problem
Explain each of the uses of `std::` in the following program:
``` Cpp
int main()
{
  int k = 0;
  while (k != n) {     // invariant: we have written k asterisks so far
    using std::cout;
    cout << "*";
    ++k;
  }
  std::cout << std::endl; // std:: is required here 
  return 0;    
}
```

## Solution

### Code
