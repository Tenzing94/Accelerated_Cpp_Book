# Exercise 3-1

## Problem
Suppose we wish to find the median of a collection of values. Assume that we have read some of the values so far, and that we have no idea how many values remain to be read. Prove that we cannot afford to discard any of the values that we have read.

_Hint_: One proof strategy is to assume that we can discard a value, and then find values for the unread - and therefore unknown - part of our collection that would cause the median to be the values that we discarded.
## Solution

### Proof by Contradiction

Assumption: A vector holds an unknown amount of values. Removing value(s) from the vector should not affect the median of the values. This means that the median of the values with some value(s) removed should equal the median of the values without any removed.

This sounds tricky. Let us get a better picture with an example.
- Lets say we have a vector with the following values `1,2,3,4,5`. The median is `3`
- Lets remove the first two values `1, 2` and add two new values `6,7,8`. The vector now looks like this `3,4,5,6,7,8`.
- The median is now `(5+6)/2 = 5.5`.

As you can see, removing values will most likely change the median. Hence, our assumption is false.



