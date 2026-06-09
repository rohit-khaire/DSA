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











| Operation        | Your Solution (Transfer on Every Push) | Optimal Solution (Lazy Transfer Using 2 Stacks) |
| ---------------- | -------------------------------------- | ----------------------------------------------- |
| `push(x)`        | **O(n)**                               | **O(1)**                                        |
| `pop()`          | **O(1)**                               | **O(1) amortized**                              |
| `peek()`         | **O(1)**                               | **O(1) amortized**                              |
| `empty()`        | **O(1)**                               | **O(1)**                                        |
| Space Complexity | **O(n)**                               | **O(n)**                                        |
