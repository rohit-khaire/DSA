# Postorder Traversal

[LeetCode](

**Main Issue Here:** Here you get confused when returning to above nodes. For Example,

```

   5
 /  \
1    8

```

When returning to 5, we get confused on Can we process the 5 Now? Because I don't know, whether right is processed or not

We get confused on we are returning from left or right? (from 1 or from 8?)

As we can print root(5) only after right is processed

We have 3 approaches to solve this:
1. Recursion
2. Using 1 stack (store last visited node in a variable)
3. Using 2 Stacks, we store node in s2 and left and right in s1, then we perform same for s1.top() (Loop it), Atlast we get root-right-left in s2, and on popping we get left-right-root


