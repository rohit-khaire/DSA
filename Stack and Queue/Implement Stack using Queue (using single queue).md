# Implement Stack using Queue (using single queue)

[LeetCode](https://leetcode.com/problems/implement-stack-using-queues/)

Implement Stack using Queue

For the LeetCode problem "Implement Stack using Queues", there are only two standard approaches:

| Approach                     | Push | Pop  | Top  |
| ---------------------------- | ---- | ---- | ---- |
| Current (rotate during push) | O(n) | O(1) | O(1) |
| Rotate during pop            | O(1) | O(n) | O(n) |

You cannot make all operations O(1) using only queues because a queue naturally provides FIFO order while a stack requires LIFO order.

So your approach is already the optimal single-queue solution


> Rotate the queue after every push so that the most recently inserted element always stays at the front, making pop() and top() O(1).


```cpp
class MyStack {
queue<int> q; 
public:
    MyStack() {
        
    }
    
    void push(int x) {
        int n = q.size();
        q.push(x);
        for(int i=0;i<n;i++){
            q.push(q.front());
            q.pop();
        }
    }
    
    int pop() {
        if(q.empty()) return -1;
        int f = q.front();
        q.pop();
        return f;
    }
    
    int top() {
        if(q.empty()) return -1;
        return q.front();
    }
    
    bool empty() {
        return q.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```


**Time Complexity:** `push = O(n)`, `pop = O(1)`, `top = O(1)`, `empty = O(1)`

**Space Complexity:** `O(n)` (single queue storing all elements).
