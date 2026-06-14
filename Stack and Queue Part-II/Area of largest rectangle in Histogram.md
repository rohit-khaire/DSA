# Area of largest rectangle in Histogram

[LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/)

: Given an array of integers heights representing the histogram's bar height where the width of each bar is 1 return the area of the largest rectangle in histogram. .

# OPTIMAL Approach 1 using 2 Extra Arrays

We will be having 2 Extra Arrays: 

1. Previous Smaller Element (PSE): If none then -1 
2. Next Smaller Element (NSE): If none then N (outside index of Array)

Why we need PSE and NSE? 

These are the indices till where we can expand our rectangle, as on these indices our height becomes smaller which stop us from expanding further

For current index, we search that using this height, how much we can expand in Left and in Right, so that we can Area=height*width

Main Formula:

```
height = heights[i];
width  = NSE[i] - PSE[i] - 1;

area = height * width;
```


Example:

heights = [2,1,5,6,2,3]

<br>

| i | H | PSE | NSE | Width | Area |
| - | - | --- | --- | ----- | ---- |
| 0 | 2 | -1  | 1   | 1     | 2    |
| 1 | 1 | -1  | 6   | 6     | 6    |
| 2 | 5 | 1   | 4   | 2     | 10   |
| 3 | 6 | 2   | 4   | 1     | 6    |
| 4 | 2 | 1   | 6   | 4     | 8    |
| 5 | 3 | 4   | 6   | 1     | 3    |


**Maximum: 10**

--------------------------

We can get PSE and NSE by using Monotonic Stack

For PSE: Start from 0 to N-1, 

Use a monotonic increasing stack.

```cpp
while(!st.empty() && heights[st.top()] >= heights[i])
    st.pop();
```

After popping:

```cpp
if(st.empty()) pse[i] = -1;
else pse[i] = st.top();
```

Then:

```cpp
st.push(i);
```

------------

How we get NSE?

Travserse from N-1 to 0

```cpp
while(!st.empty() && heights[st.top()] >= heights[i])
    st.pop();
```

...


--------------------

Think of it Like:

```md
For every bar:

Get first smaller on LEFT, PSE[i]
Get first smaller on RIGHT, NSE[i]

Those two smaller bars act as WALLS.

Rectangle can expand only between those walls.

width = rightWall - leftWall + 1

area = height × width

Store maximum area
```


**Time Complexity: O(3N). To get PSE , get NSE, Single loop at the end using O(N)**

**Space Complexity: O(3N) where 3 is for the stack, left small array and a right small array**

-------------------------------------------

# OPTIMAL Approach 2 - without having NSE, just using Single Stack

Think like:

When we are moving from left to right (0 to N-1)

We maintain a increasing order in the Stack

If we face smaller element (arr[i]<arr[i-1]), we can say that for previous element, i is the bar which is smaller than i-1

Which means i-1 bar cannot expand till i th bar, it can go till only i-1 th bar

So our Right Boundary is i-1 th bar, and Left Boundary is stack's top, if stack's top is empty then it means that our rectangle can expand till 0th index so we use Left Boundary as -1

We calculate area while popping, that while(s.top() < arr[i]) I will pop and calculate Area for that Height

Whatever we are popping from the Stack, as we were having a Increasing order 12345 in the Stack(we Store indices)

So, popping 5th index means value at 5th index is greater than ith index, which means value at 5th index cannot expand further

Example, values: 23456

Popping 6, means ith bar is Right Boundary for 6 and for left boundary we can see the stack, which is 5, 5 is the PSE(closest smaller in left) of 6

SO our Area as, Width is between Left and Right Boundary, our height is Popped value 


## The Magic Observation

When a bar gets popped:

height = popped bar

Current index automatically gives:

NSE

Stack top automatically gives:

PSE

Thus:

width = NSE - PSE - 1;

same formula as previous solution!

Hence we maintain a Increasing order in The Stack, when we face smaller element than stack top, we start to Pop

## Visual Memory Trick

Imagine each bar is trying to expand forever to the right.

2 1 5 6

All are happy.

Then:

2

arrives.

Now:

5 6

cannot expand anymore.

The new smaller bar acts like a WALL.

5 6 | 2

Everything taller than 2 dies here.

Pop them one by one.

Calculate their final rectangle.

<br><br>

Edge Case:

Consider:

[1,2,3,4]

No smaller element ever appears.

Nothing gets popped.

Answer never computed.

So after array ends:

1 2 3 4

pretend a bar of height:

0

arrives.

1 2 3 4 0

Now everybody gets popped.

Areas get calculated.

This is why you'll see:

for(int i=0;i<=n;i++)

and

currHeight = (i==n)?0:heights[i];




# 3 line Summary

```rainbow
1. Maintain a monotonic increasing stack of indices.
2. When a smaller bar appears, pop taller bars because their NSE is found.
3. For popped bar: NSE = current index, PSE = stack top after pop, area = height × (NSE-PSE-1).
```

This is why many experienced programmers think of the stack as a "bars waiting for their first smaller element on the right." The moment that smaller element appears, the bar's story is finished, and its area is computed



