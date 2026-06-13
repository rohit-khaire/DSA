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






<br>

----------------

# Min Stack

[LeetCode](https://leetcode.com/problems/min-stack/)

# OPTIMAL Approach 1 - Using 2 stacks or single stack of pair<int,int>

```cpp
class MinStack {
public:
    stack<pair<int, int>> st;
    MinStack() {
        
    }
    
    void push(int val) {
        if (!st.empty()) {
            st.push({val, min(val, st.top().second)});
        } else {
            st.push({val, val});
        }
    }
    
    void pop() {
        st.pop();
    }
    
    int top() {
        return st.top().first;
    }
    
    int getMin() {
        return st.top().second;
    }
};
```

TC=O(1) and SC=(2N) as stack stores {value,minimumTillNow}

# OPTIMAL Approach - Using Single stack and one Mini variable and Formula

**Formula: Encoded = 2*newMin - oldMin**

```cpp
class MinStack {
    stack<long long> s;
    long long mini;
public:
    MinStack() {
        mini=INT_MAX;
    }
    //2*value - Mini = newVal
    void push(int value) {
        if(s.empty()){
            mini=value;
            s.push(value);
            return;
        }
        if(value<mini){ //mini changes
            // int newValue = (2*value)-mini; //-6+2 = -4 and new mini -3
            s.push((2LL*value)-mini); //coded
            mini = value;
            
        }else{
            s.push(value); //mini not changes
        }
    }
    
    void pop() {
        if(s.empty()) return;
        long long mayEncoded = s.top();
        s.pop();
        if(mayEncoded<mini){//Means mayEncoded was coded
            //get previous mini
            //2*newMini - prevMini = encoded
            //2*newMini - encoded = prevMini , need=-2 and have mini=-3 and mayEncoded=-4
            mini = 2*mini - mayEncoded;
        }
        //else mini remains as it is
    }
    
    int top() {
        if(s.empty()) return -1;
        if(s.top()<mini){
            //Means it is encoded
            //So it means our mini is the top, as it was changing the mini hence we coded it
            return mini;
        }
        return s.top();
    }
    
    int getMin() {
        if(s.empty()) return -1;
        return mini;
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(value);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

TC=O(1) and SC=(N) as single stack is used

