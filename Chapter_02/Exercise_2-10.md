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
- A `namespace` is a collection of related names.
- `std` is the namespace that the standard library uses to contain all of the names that it defines. Why is this useful?
  - One of the variables that the standard library defines is `endl`.
  - In the off chance that we declared the variable `endl` in our program as well, the namespace would ensure that the two would not conflict. 
  - If we want to use the variable that we declared, we simply use `endl`. While if we want to use the `endl` declared by the standard library, we use `std::endl`.

Inside the while loop, `using std::cout;` tells the program that `cout` inside this loop specifically refers to the standard library definition `std::cout`. This is why in the following line, `cout` is used without `std::` in front of it.

The line `std::cout << std::endl;` tells the program that we are using `cout` and `endl` from the standard library. Note that `using std::cout;` that we defined inside the loop does not apply here because it is outside the scope.
