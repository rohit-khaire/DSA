# Next Permutaion

arr[]= [3 1 2]<br>
1 2 3<br>
1 3 2<br>
2 1 3<br>
2 3 1<br>
3 1 2<br>
3 2 1<br>

Ans= [3 2 1] as it comes after [3 1 2]

For [3 2 1] , Ans= [1 2 3]

All the permutaions are in Ascending Order, and these are Total n!

Like in our case n=3, 3!=6

After last number, you can index to first number

## Brute Force

1. Generate all permuations in Sorted order (Using Recursion)

2. Linear Search for Input

3. Next Index Permutaion is Answer

Approx TC for it would be around {N! * N}

Which is High

C++ user can use STL library directly and use next_permutation func:
<img width="470" height="97" alt="image" src="https://github.com/user-attachments/assets/c6b390a8-6474-4ab9-954e-df815a892068" />

But this is pre-built, if using C++ then highly recommended



## Optimal

1. Find the Break Point ( The point on which Ele is smaller than the next Ele ) { a[i] < a[i+1] }

Like in 2 1 5 4 3

Start with last ele : 3, Nothing to do {3}

Then: 4, {4,3} => We can get 43 which is equal to last ele of main no. and 34 which is smaller than last ele of main no.

We want bigger no., but remember that bigger number will prove that it's after 2 1 5 4 3, <br>
But would not prove that it's exactly after 2 1 5 4 3 number, like it can be after 2 numbers from main number <br>
And we need exactly the next number of 2 1 5 4 3

Then: 5, {5,4,3} => All the combinations from these are smaller than 543 like 534,453,435,etc.

Then: 1, {1,5,4,3} => **a[i] < a[i+1]**, 1<5 

We can form number greater than 1543 like 5431,3451,3415,4315,4351,etc.

But we need exact next permutaion of 1543

<img width="302" height="106" alt="image" src="https://github.com/user-attachments/assets/05c9bc51-4d3a-421b-bd5e-ac3cd2906d32" />

So now 21|543

Now 2 remains as it is as it's before 1, 

Everything before break point remains as it is

**2** and now next number we can choose from 1 5 4 3

We can get 21, 25, 24, 23 so we need greater than 21 but most closest to 21 which is 23

So we get **23** and remaining are 1 5 4

Our aim is to keep the number shortest now, so we can create shoertest number by having **Increasing Order**

**23** {1 5 4}

**23145**



## **Summary:**

**21543**

1. Try to find longest prefix match ( Start from last and get break point, a[i]<a[i+1] ) {21 | 543}

It's like a dip:

```
    | (break point) 
  1/   \5   
        \4   
          \3  

```

If no dip (break point found), it means that the given no. is the last no. in the permutation

At that moment, just reverse the number to get the first no. and that's answer

Like {54321}, It's last so ans is {12345}

3. After longest prefix match (2 in our case), put(swap) someone who is closest and greater to that 1st number (1 in our case) from right side set

2_ => greater and closest to 1 from {5,4,3} = 3

23 and {1,5,4}

3. Now put right side list in Sorted order to form smallest no. as possible

which is 145

Answer: **23145**




