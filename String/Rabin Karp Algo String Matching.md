# Rabin Karp Algorithm - String Matching

[LeetCode](

# Approach

Get the Text(T) and Pattern(P)(To be found in Text)

Now calculate the Hash Value for P (a+b+c=1+2+3=5)

Get the length of Pattern = M

Now we will calculate the Hash of Window Size M in Text (T)

If our Hash from T == Hash of P => Then we match character by character (T's window and P)

If that T's part != Pattern but both has Equal Hash Values, then that's a Supreious Hit

If Hash Values of T's part(of window size M) and of Pattern (P) doesn't match, means we have to move window further

> Note: We need to calculate Hash Values of Text Window in OPTIMAL Way O(1), If you calculate Hash Value for a 0th window, then for 1st window do not calculate the whole hash value again

Just remove the expired element's value(subtract) and Add new element's value to get the HASH in Optimal Time


<img width="725" height="264" alt="image" src="https://github.com/user-attachments/assets/1d04876d-c6b1-4b6a-8963-7b259dc59c3d" />

d=BASE (NO. of possible characters ABC.. are 26 for ASCII 256)


Good. Stop watching more videos for now.

Most confusion in Rabin-Karp comes because different people start from different levels:

* College Theory → `a=1,b=2,c=3`, hash = sum
* Competitive Programming → Polynomial Rolling Hash
* Research/Advanced → Double Hashing, Random Bases, Large Primes

Let's build **one complete mental model** and stick to it.

---

# Step 0: What Problem Are We Solving?

Given:

```text
Text    = "ababcabc"
Pattern = "abc"
```

Need to find all occurrences of `"abc"`.

Brute Force:

```text
abc vs aba
abc vs bab
abc vs abc
...
```

Complexity:

```text
O(N*M)
```

Rabin-Karp says:

> Convert strings into numbers and compare numbers first.

---

# Step 1: What Is A Hash?

A hash is simply a fingerprint.

Example:

```text
abc -> 731
xyz -> 16900
```

Now instead of:

```text
abc == aba ?
```

we do:

```text
731 == 704 ?
```

Much faster.

---

# Step 2: Why Not Use Sum?

Your theory notes used:

```text
a=1
b=2
c=3

abc = 1+2+3 = 6
```

Problem:

```text
abc = 6
aad = 6
bbe = 6
```

Too many collisions.

---

# Step 3: Better Idea

Treat string like a number.

Example:

Decimal:

```text
123

=
1×10²
+
2×10¹
+
3×10⁰
```

Similarly:

```text
abc

=
1×26²
+
2×26¹
+
3×26⁰
```

This is called:

## Polynomial Hash

---

# Step 4: Where BASE Comes From?

Suppose alphabet:

```text
a-z
```

Total:

```text
26 characters
```

Therefore:

```text
BASE = 26
```

because every position can have 26 possibilities.

---

Visual:

```text
abc

=
1×26²
+
2×26¹
+
3×26⁰
```

---

For ASCII:

```text
256 characters
```

People use:

```text
BASE = 256
```

---

For lowercase English:

```text
BASE = 26
```

or

```text
31
```

or

```text
53
```

---

# Why 31?

YouTube people often use:

```cpp
BASE = 31
```

because:

```text
31 > 26
```

and mathematically gives fewer collisions.

Nothing magical.

Just a good choice.

---

# Step 5: Where Does d Come From?

In textbook notation:

```cpp
d
```

means:

```text
Number of possible characters
```

which is exactly:

```text
BASE
```

So:

```text
d = BASE
```

---

Example:

```text
Alphabet a-z

d = 26
BASE = 26
```

Same thing.

---

# Step 6: Where Does q Come From?

Now imagine:

```text
Hash("aaaaaaaaaaaaaaaaaaa")
```

Value becomes gigantic.

---

Example:

```text
26^50
```

Huge.

Cannot fit in integer.

---

Therefore:

```cpp
hash %= q;
```

---

Choose:

```cpp
q = 1000000007
```

or

```cpp
q = 1000000009
```

Large prime.

---

Purpose:

✅ Prevent overflow

✅ Reduce collisions

---

# Important

### BASE and q are completely different

BASE:

```text
Used to build the number
```

Example:

```text
abc

=
1×26²
+
2×26¹
+
3
```

BASE = 26

---

q:

```text
Used to keep answer small
```

Example:

```cpp
hash %= 1000000007
```

---

# Step 7: Final Hash Formula

Character value:

```cpp
value = ch-'a'+1
```

Hash:

```cpp
hash = (hash*BASE + value)%q;
```

---

Let's compute:

```text
abc
```

Take:

```text
BASE=26
q=101
```

---

Start:

```text
hash=0
```

a:

```text
(0*26+1)%101

=1
```

---

b:

```text
(1*26+2)%101

=28
```

---

c:

```text
(28*26+3)%101

=731%101

=24
```

Final:

```text
Hash("abc") = 24
```

---

# Why This Formula Works

Observe:

```text
hash = hash*26 + value
```

Expands into:

```text
a×26²
+b×26¹
+c×26⁰
```

Exactly what we wanted.

---

# Step 8: Window Sliding

Current:

```text
abc
```

Need:

```text
bcd
```

without recomputing.

---

Hash of:

```text
abc

=
a×26²
+b×26
+c
```

---

Remove:

```text
a×26²
```

Remaining:

```text
b×26+c
```

---

Shift left:

```text
(b×26+c)×26
```

becomes:

```text
b×26²+c×26
```

---

Add:

```text
d
```

Result:

```text
b×26²+c×26+d
```

which is exactly:

```text
bcd
```

---

# The Famous Formula

Textbook image:

```cpp
hash(next)
=
(d*(hash(curr)-leading*h)+trailing)%q
```

where:

```cpp
h=d^(m-1)
```

---

Now replace symbols:

```cpp
BASE = 26

h = BASE^(m-1)
```

Then:

```cpp
newHash =
(
BASE
*
(
oldHash
-
leadingChar*h
)
+
newChar
)%q;
```

That's it.

No magic.

---

# What You Should Remember For Interviews

Only remember this table:

| Symbol  | Meaning                                    |
| ------- | ------------------------------------------ |
| BASE    | Number used to build hash (26,31,256 etc.) |
| d       | Same as BASE in textbooks                  |
| q       | Prime modulus to prevent overflow          |
| h       | BASE^(m-1) % q                             |
| oldHash | Current window hash                        |
| newHash | Next window hash                           |

---

# The Simplest Modern Implementation

```cpp
const long long BASE = 31;
const long long MOD  = 1e9+7;
```

Hash creation:

```cpp
hash = (hash*BASE + value)%MOD;
```

Rolling hash:

```cpp
newHash =
(
(
oldHash
-
leading*power
)%MOD
+MOD
)%MOD;

newHash =
(newHash*BASE + trailing)%MOD;
```

where:

```cpp
power = BASE^(m-1)%MOD;
```

---

This is the version I would recommend you memorize forever:

```text
BASE = 31
MOD  = 1e9+7

hash = hash*BASE + value

rolling:
remove old char
shift left (×BASE)
add new char
```

Everything else (d, q, h, 256, 101, etc.) is just different notation for the same idea. Once you understand "remove → shift → add", Rabin-Karp becomes very easy to derive during interviews instead of memorizing formulas.


<br><br><br><br><br><br>
686. Repeated String Match

Given two strings a and b, return the minimum number of times you should repeat string a so that string b is a substring of it. If it is impossible for b​​​​​​ to be a substring of a after repeating it, return -1.

Notice: string "abc" repeated 0 times is "", repeated 1 time is "abc" and repeated 2 times is "abcabc".

# Approach 1 using Naive String Matching

- int repeatedStringMatch(string a,string b)
  - if a==b, return count as 1
  - Initialize source=a and count=1
  - add a in source while source.size() < b.size() , to search b in source
  - Now our source.size() >= b.size()
  - match source and b
    - if b is found in source, then return count
    - Find b in source+a , if found then return count+1
  - return -1, as no b can be found in repeated a

<br><br>

- for string matching, using Naive String Match
- bool searchPattern(string text, string pattern) // Pattern is to be search inside text
  - if text and pattern are equal, then return true
  - get size of text(n) and size of pattern(m)
  - We start our sliding window, and match pattern each time

**TC=O(n*m) for pattern finding**

```cpp
class Solution {
public:
    bool searchPattern(string text,string pattern){
        if(text==pattern) return true;
        int n=text.size();
        int m=pattern.size();
        for(int i=0;i<=n-m;i++){
            for(int j=0;j<m;j++){
                if(text[i+j]!=pattern[j]) break;
                if(j==m-1 && text[i+j]==pattern[j]) return true;
            }
        }
        return false;
    }
    int repeatedStringMatch(string a, string b) {
        if(a==b) return 1;
        string source=a;
        int count=1;
        // To find b in source
        while(source.size()<b.size()){
            source+=a;
            count++;
        }
        // Now source.size() is either ==b.size() or >b.size()
        // if(source==b){
        //     // b substring is equals to source
        //     return count; // required no. of times a is required
        // }
        if(searchPattern(source,b)) return count;
        if(searchPattern(source+a,b)) return count+1; //search b in source+a
        return -1;
    }
};
```
TC=O(n+m) for string construction + O((m+n)*m) for first string search,m comparison each + O((m+2n)*m)



# Approach using Rabin Karp for string matching

