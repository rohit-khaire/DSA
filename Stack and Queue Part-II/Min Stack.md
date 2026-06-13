# Min Stack

[LeetCode](https://leetcode.com/problems/min-stack/description/)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class:
- MinStack() initializes the stack object.
- void push(int value) pushes the element value onto the stack.
- void pop() removes the element on the top of the stack.
- int top() gets the top element of the stack.
- int getMin() retrieves the minimum element in the stack.
You must implement a solution with O(1) time complexity for each function.

## Brute Force

Store pair in stack {value,minimum_tillNow}

A stack of pairs is used, where each pair contains the element itself and the minimum element at the time the element was pushed onto the stack.

The MinStack class is initialized with an empty stack.

- Push Operation:
  - When a new element is pushed, it is compared with the current minimum.
  - The new element and the updated minimum are stored as a pair and pushed onto the stack.
- Pop Operation:
  - The top element (which is a pair) is removed from the stack.
- Top Operation:
  - The top element of the stack is accessed to get the actual value (first component) stored in the pair.
- GetMin Operation:
  - The second value of the pair at the top of the stack, which represents the minimum element at that point, is accessed.
 
Time Complexity: O(1) for all operations (push, pop, top, getMin) as they involve constant time operations on the stack.

Space Complexity: O(2n) where n is the number of elements in the stack, as we store pairs of values (element and minimum) in the stack.

# OPTIMAL 

After modification, your mini is your top value

If your ele is smaller than mini, it means you have modified



