# Implement Pow(x,n) | X raised to the power N

[LeetCode](https://leetcode.com/problems/powx-n/description/)

PS: Implement the power function pow(x, n) , which calculates the x raised to n i.e. x^n

```
OPTIMAL: 

When even n : power(x*x,n/2)

When odd n: n*power(x,n-1)
```


## Brute Force

Initialize the result variable: ans=1. This serves as the base case where any number raised to the power of 0 is 1.

Check if the exponent n is less than 0:

* If true, invert x by setting x = 1/x and make n positive by setting n = -n. This transformation allows handling of negative exponents.

Use a loop to iterate from 0 to n (converted to an integer). In each iteration, multiply ans by x. This effectively computes x raised to the power of n.

Return the result stored in ans, which now contains the value of x^n.

**TC = O(N)**

**SC = O(1)**

## Optimal Solution ( Using Recursion )

If n == 0 , return 1 , as anything raise to 0 is 1

If n==1 , return x , This is the base condition

If n is Even = power(x*x, n/2 ) => 3^10 = (3^2)^5 = (3*3)^5 

If n is Odd = x*power(x,n-1) => 3^7= 3* 3^6



Define a helper function that handles the recursive calculation of the power. <br>
Base Case 1: If the exponent n is 0, return 1 because any number raised to the power of 0 is 1. <br>
Base Case 2: If the exponent n is 1, return the base x, since any number raised to the power of 1 is itself. <br><br>
If the exponent n is even: <br>
* Recursively calculate the power by squaring the base and halving the exponent/2: ``power(x, n) = power(x * x, n / 2)`` <br>

If the exponent n is odd:

* If true, recursively calculate the power by multiplying the base with the result of the power function for n - 1:

``power(x, n) = x * power(x, n - 1)``

Handle negative exponents:

If the exponent is negative, calculate the power for the positive exponent and take the reciprocal of the result.

x^(-n) = 1/ x^n

<img width="403" height="343" alt="image" src="https://github.com/user-attachments/assets/f7e4ed10-bb7a-42f9-817e-2c459f68d58d" />

## Code

```
class Solution {
private:
    // Function to calculate power
    // of 'x' raised to 'n'
    double power(double x, long n) {
        // Base case: anything raised to 0 is 1
        if (n == 0) return 1.0;

        // Base case: anything raised to 1 is itself
        if (n == 1) return x;

        // If 'n' is even
        if (n % 2 == 0) {
            // Recursive call: x * x, n / 2
            return power(x * x, n / 2);
        }
        // If 'n' is odd
        // Recursive call: x * power(x, n-1)
        return x * power(x, n - 1);
    }

public:
    // Function to calculate x raised to n
    double myPow(double x, int n) {
        // Store the value of n in a separate variable
        int num = n;

        // If n is negative
        if (num < 0) {
            // Calculate the power of -n and take reciprocal
            return (1.0 / power(x, -1 * num));
        }
        // If n is non-negative
        return power(x, num);
    }
};
```

**TC = O(log n)**

**SC = O(log n)**
