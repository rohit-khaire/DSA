# Maximize Sum of Squares of Digits

[Leetcode](https://leetcode.com/problems/maximize-sum-of-squares-of-digits/description/)

Let's understand LeetCode 3723. Maximize Sum of Squares of Digits in the easiest way possible, so you can remember the logic and write the code yourself during an interview.

The key is to understand what we are maximizing and why before looking at the code.

## 1. Understand the question in simple words

You are given two numbers:

- `num` = how many digits your answer must contain.
- `sum` = the total sum of those digits.

You need to create a number that satisfies both conditions and maximizes the sum of the squares of its digits. If multiple answers have the same score, choose the largest number.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://leetcode.com\&sz=32)

LeetCode



For example:

`num = 2, sum = 3`

Possible numbers:

| Number | Digit sum | Score (sum of squares) |
| ------ | --------- | ---------------------- |
| 12     | 1 + 2 = 3 | 1 + 4 = 5              |
| 21     | 2 + 1 = 3 | 4 + 1 = 5              |
| 30     | 3 + 0 = 3 | 9 + 0 = 9              |

The answer is `"30"` because its score is the highest.

Think: We have 2 digit positions and a total sum of 3. Should we distribute the sum as `1 + 2`, or keep it together as `3 + 0`?

Keeping it together gives a higher score!

## 2. The main logic — remember this!

Put as many 9s as possible at the beginning, then put the remaining sum, and fill the rest with zeros.

Why?

- `9² = 81` — a very high contribution to the score.
- `8² = 64`, `7² = 49`, and so on.
- Concentrating the sum into larger digits maximizes the sum of squares.
- Putting larger digits first also gives the largest number when scores tie.

That's the entire greedy approach.

## 3. Dry run with an example

Suppose:

```
num = 3
sum = 20
```

We need exactly 3 digits whose sum is 20.

STEP 1 — Place the largest digit

# 9

20 − 9 = 11

# 9

11 − 9 = 2

# 2

2 − 2 = 0

STEP 2 — Combine the digits

# 992

Digit sum = 9 + 9 + 2 = 20 ✓

We used two 9s, then the remaining 2. There are no positions left to fill with zeros.

Answer: `"992"`.

## 4. Convert the logic into C++ code

Here is the optimal LeetCode solution.

```

class Solution {
public:
    string maxSumOfSquares(int num, int sum) {
        if (num * 9 < sum) {
            return "";
        }

        string ans = "";

        for (int i = 0; i < num; i++) {
            int digit = min(9, sum);

            ans += char('0' + digit);
            sum -= digit;
        }

        return ans;
    }
};

```

## 5. Understand every line

Line 1: Check if an answer is possible

```
if (num * 9 < sum) return "";
```

Every digit can be at most 9.

If `num = 2`, the maximum possible digit sum is `9 + 9 = 18`.

Therefore, if `sum = 20`, there is no valid answer, and we return an empty string.

Line 2: Create the answer

```
string ans = "";
```

We will add each digit to this string.

Why a string? Because the answer can contain up to 200,000 digits, which cannot fit into an ordinary integer or `long long`.

Line 3: Visit every digit position

```
for (int i = 0; i < num; i++)
```

If `num = 3`, the loop runs exactly 3 times because our answer needs exactly 3 digits.

Line 4: Choose the largest possible digit

```
int digit = min(9, sum);
```

This is the most important line!

- If `sum = 20`, choose `9`.
- If `sum = 11`, choose `9`.
- If `sum = 2`, choose `2`.
- If `sum = 0`, choose `0`.

In other words, choose 9 whenever possible; otherwise, choose whatever remains.

Line 5: Add the digit

```
ans += char('0' + digit);
```

C++ converts the digit into its character representation so that we can append it to the string.

For example, if `digit = 9`, we append the character `'9'`.

Line 6: Reduce the remaining sum

```
sum -= digit;
```

If the remaining sum is 20 and we choose 9, the new sum becomes 11.

We repeat this process until all digit positions are filled.

## 6. Test your understanding

Try tracing the code mentally for each input.

## Practice question

1 of 5

# num = 3, sum = 20

What string will the algorithm return?

Show answerNext question

## 7. Complexity

- Time: O(num) - we process each digit once.
- Space: O(num) - the answer string contains `num` digits.

## Final revision — memorize these 4 steps

The 9 → Subtract → Repeat → Return pattern

1. Check if `sum > 9 * num`; if yes, return `""`.
2. Choose `min(9, sum)` as the next digit.
3. Append the digit and subtract it from `sum`.
4. Repeat exactly `num` times and return the string.

Interview explanation: “I use a greedy approach. To maximize the sum of squared digits, I place the largest possible digit, 9, first. I subtract that digit from the remaining sum and repeat for each position. If the required sum exceeds `9 * num`, no valid number exists. This gives an optimal solution in linear time.”

One important thing: don't try to calculate the squares in your code. You only need to construct the optimal number; maximizing the squared sum is achieved automatically by this greedy strategy.
