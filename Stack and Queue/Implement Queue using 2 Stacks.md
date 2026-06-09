# Implement Queue using 2 Stacks

[LeetCode](https://leetcode.com/problems/implement-queue-using-stacks/description/)

## Using 2 stacks 

While pushing, handle everything so that everything else operations can be directly used easily

```cpp
class MyQueue {
    stack<int> s1,s2;
public:
    MyQueue() {
        
    }
    
    void push(int x) {
        while(!s1.empty()){
            s2.push(s1.top());
            s1.pop();
        }
        s1.push(x);
        while(!s2.empty()){
            s1.push(s2.top());
            s2.pop();
        }
    }
    
    int pop() {
        if(s1.empty()) return -1;
        int top=s1.top();
        s1.pop();
        return top;
    }
    
    int peek() {
        if(s1.empty()) return -1;
        return s1.top();
    }
    
    bool empty() {
        return s1.empty();
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```

TC=O(N) for push, TC=O(N)


# OPTIMAL (Expected) using Two Stacks in and out

Used 2 stacks input (in) and output(out)

While pushing, directly push to input stack

while viewing top and poping, transfer all eles of input stack to output stack, now we got 1st element on top of output stack

Our queue is empty when both the stacks are Empty



```cpp
class MyQueue {
    stack<int> in,out;
public:
    MyQueue() {
        
    }
    
    void push(int x) {
        in.push(x);  //O(1)
    }
    
    int pop() {
        if(in.empty() && out.empty()) return -1;
        if(out.empty()){
            while(!in.empty()){
                out.push(in.top());  //O(N)
                in.pop();
            }
        }
        int p = out.top(); //or O(1)
        out.pop();
        return p;

    }
    
    int peek() {
        if(in.empty() && out.empty()) return -1;
        if(out.empty()){
            while(!in.empty()){
                out.push(in.top());
                in.pop();
            }
        }
        return out.top();
    }
    
    bool empty() {
        return in.empty() && out.empty();
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```



This is the standard optimal solution expected in coding interviews for "Implement Queue using Stacks."

**Amortized Time Complexity** means:

> Even if some individual operations are expensive, the **average cost per operation over a sequence of operations** is small.

---

### Example with Your Queue

Suppose:

```cpp
push(1);
push(2);
push(3);
push(4);

pop();
pop();
pop();
pop();
```

#### Cost of Pushes

```text
push(1) → O(1)
push(2) → O(1)
push(3) → O(1)
push(4) → O(1)
```

Total = **4 operations**

---

#### First Pop

Since `out` is empty:

```cpp
while(!in.empty()){
    out.push(in.top());
    in.pop();
}
```

Moves 4 elements.

```text
pop() → O(4)
```

Then removes one element.

---

#### Remaining Pops

```text
pop() → O(1)
pop() → O(1)
pop() → O(1)
```

No transfer needed.

---

### Total Cost

```text
4 pushes = 4
1 expensive pop = 4
3 cheap pops = 3

Total work = 11
Total operations = 8
```

Average cost:

[
\frac{11}{8}
]

which is a constant.

So we say:

```text
Amortized Cost = O(1)
```

---

## Intuition

Think of each element paying for its own transfer.

For an element like `3`:

```text
push into in     → 1 operation
move to out      → 1 operation
pop from out     → 1 operation
```

That element is touched only a constant number of times.

Since every element is moved from `in` to `out` **at most once**, the total extra work over `n` elements is only `O(n)`.

Therefore:

[
\frac{O(n)}{n}=O(1)
]

per operation on average.

---

## Difference Between Worst Case and Amortized

| Complexity Type | Meaning                                                          |
| --------------- | ---------------------------------------------------------------- |
| Worst Case      | Cost of a single operation in the worst situation                |
| Average Case    | Average over different inputs                                    |
| Amortized       | Average over a sequence of operations on the same data structure |

For your queue:

| Operation | Worst Case | Amortized |
| --------- | ---------- | --------- |
| push      | O(1)       | O(1)      |
| pop       | O(n)       | O(1)      |
| peek      | O(n)       | O(1)      |

because the expensive transfer can happen only occasionally.

### Interview One-Liner

> Amortized O(1) means that although some `pop()` or `peek()` operations may take O(n) time due to stack transfer, each element is transferred at most once, so over a sequence of operations the average cost per operation is O(1).




| Operation        | Your Solution (Transfer on Every Push) | Optimal Solution (Lazy Transfer Using 2 Stacks) |
| ---------------- | -------------------------------------- | ----------------------------------------------- |
| `push(x)`        | **O(n)**                               | **O(1)**                                        |
| `pop()`          | **O(1)**                               | **O(1) amortized**                              |
| `peek()`         | **O(1)**                               | **O(1) amortized**                              |
| `empty()`        | **O(1)**                               | **O(1)**                                        |
| Space Complexity | **O(n)**                               | **O(n)**                                        |
