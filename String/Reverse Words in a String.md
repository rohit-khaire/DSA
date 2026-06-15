# Reverse Words in a String

[LeetCode](https://leetcode.com/problems/reverse-words-in-a-string/)

Input: s = "the sky is blue"

Output: "blue is sky the"

String can contain a-z,A-Z,0-9, and multiples Spaces

Problem Statement: Given an input string, containing upper-case and lower-case letters, digits, and spaces( ' ' ). A word is defined as a sequence of non-space characters. The words in s are separated by at least one space. Return a string with the words in reverse order, concatenated by a single space.


# Brute Force

Traverse the string from Left to Right. Add each word in a List. Now reverse the List. Make a string as result from this reversed List, appending one space between each word.

- Initialize an empty list to store words.
- Traverse the string character by character.
- Identify consecutive non-space characters as a word.
- Ignore extra spaces and leading/trailing spaces while collecting words.
- Append each identified word to the list.
- Reverse the list of words.
- Join the reversed list into a single string using a single space.
- Return the resulting string.

TC=O(N) for traversing the string and creating the List of words + O(N) to reverse the List + O(No. of words) to create string from Reversed List

SC = O(N) to store List of Words + O(N) to store string result

# OPTIMAL Approach

- Start from Right to Left (N-1 to 0)
- Skip all the spaces(by moving to Left) to get End of Word
- If No end found(i==-1), means string is over, so stop the process and return the result String
- If we end is found then mark it's position (end=i)
- Now complete the word by finding space in Left, move to left till we get a Space
- When we get Space, our word is from i+1 to end, can access it using s.substr(startingIndex,lengthOfWord)
- If result is Not Empty, then add one space to separate the previous word from new word
- Concatenate new Word to the result
- When we reach -1, our string is completely traversed, now we can return the result

```cpp
class Solution {
public:
    string reverseWords(string str) {
        if(str.size()==0 || str.size() == 1) return str;
        int i= str.size()-1;
        string res = "";
        while(i>=0){
            while(i>=0 && str[i]==' '){//Skip the spaces and find end of new word
                i--;
            }
            //Now i points to End of Word or -1
            if(i==-1) break; //Means extra spaces at front were present
            int end=i; //Found end of a word
            while(i>=0 && str[i]!=' '){
                i--;
            }
            //Now i is on space=> (space)Rohit(<-end pointing t) or it points to -1
            //                       4   56789  <=Index
            if(!res.empty()){
                res+=" "; //Add space after each word
            }
            
            res+=str.substr(i+1,end-i);
        }
        return res;
    }
};
```

TC=O(N) and SC=O(1),Ignoring the output string
