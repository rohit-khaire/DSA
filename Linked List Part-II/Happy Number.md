# Happy Number

**The key insight is that Happy Number is actually a cycle-detection problem disguised as a math problem.**

A happy number is a number defined by the following process:

- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
- Those numbers for which this process ends in 1 are happy.

return true if happy.

<img width="175" height="164" alt="image" src="https://github.com/user-attachments/assets/8b228201-cfb3-4ae9-9d7d-35354fd1a14e" />


[LeetCode](https://leetcode.com/problems/happy-number/description/)


# OPTIMAL SOLUTION using Floyds Cycle Detection

**Since numbers rapidly shrink below 810, the runtime is effectively constant**


## Step 1: Observe the process

For a number `n`, repeatedly do:

```text
n = sum of squares of its digits
```

Example:

```text
19
→ 1² + 9² = 82
→ 8² + 2² = 68
→ 6² + 8² = 100
→ 1² + 0² + 0² = 1
Everything after this is 1->1->1
```

Since it reaches `1`, it is happy.

---

## Step 2: What happens if it is NOT happy?

Take `2`:

```text
2
→ 4
→ 16
→ 37
→ 58
→ 89
→ 145
→ 42
→ 20
→ 4
```

Notice:

```text
4 → 16 → 37 → 58 → ... → 4
```

We've come back to `4`.

Now the sequence will repeat forever:

```text
4 → 16 → 37 → 58 → ...
```

This is a **cycle**.

---

## Step 3: Why must a cycle exist?

For any large number, the sum of squared digits becomes much smaller.

Example:

```text
999999999
→ 9² × 9
→ 729
```

Even huge numbers quickly shrink.

After a few transformations, every number falls into a small range.

Once you're in a finite range:

* Either you reach `1`
* Or you revisit a previous value

### Happy Number Case

```text
1 → 1 → 1 → 1 ...
```

Both pointers eventually meet at:

```text
1
```

Return:

```cpp
true
```

---

### Unhappy Number Case

For `2`:

```text
4 → 16 → 37 → 58 → 89 → 145 → 42 → 20
↑                                   ↓
└───────────────────────────────────┘
```

Slow and fast enter the cycle and meet somewhere inside it.

Example:

```text
slow = 42
fast = 42
```

Since they met and value is not `1`:

```cpp
return false;
```

---

## The Core Logic in One Sentence

Treat each number as a node and the "sum of squares of digits" operation as the next pointer; then use Floyd's cycle detection:

* If the cycle is at `1` → Happy Number.
* If the cycle is somewhere else → Not Happy Number.







## Algoritm

* Have a function to calculate the next Number as sum of squares of digits. (getNumber func)

Now we point :
* slow=n
* fast = getNext(n)

Now we start a loop while fast is not equals to 1 and slow is not equals to fast

We repeatedly calculate next number of slow and assign it to slow

For fast we calculate next of next Number and assign it to fast

So slow moves 1 step and fast moves by 2 steps

At last if 1 is found, then fast will be pointing to it 

If we didn't find 1 in this cycle then slow becomes equal to fast and loop is stopped



```cpp
class Solution {
public:
    int getNext(int n){
        int totalsum=0;
        while (n>0){
            int d=n%10;
            totalsum+=d*d;
            n/=10;
        }
        return totalsum;
    }
    bool isHappy(int n) {
        int slow=n;
        int fast=getNext(n);

        while(fast!=1 && slow!=fast){
            slow=getNext(slow);
            fast=getNext(getNext(fast));
        }
        return fast==1;
    }
};
```

- Time Complexity (TC): O(log n) - each getNext() call processes all digits of n, and the sequence quickly shrinks to a small range.
- Space Complexity (SC): O(1) - only a few variables (slow, fast, sum, etc.) are used, regardless of input size.
