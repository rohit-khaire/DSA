# Assign Cookies 

[Leetcode](https://leetcode.com/problems/assign-cookies/)

We got 2 arrays, one with bhuk (greed) of child, he needs minimum that much size of cookie, otherwise he don't eat. A child can eat cookie of size >=g[i]

We need to satisfy greed of maximum childrens as possible. Some children might not get any cookie if there is no available cookie for him or size of available cookie is small.

Make sure to while giving cookie to child, cookie's size is nearest as possible to greed, so that other child's greed can be fulfilled (if possible)


# Approach - Sort both arrays and start assigning cookies to child

- Sort greed array
- Sort cookie size array
- Now we have greed and cookie sizes in increasing order
- Now start assigning cookie(right array) to each child(left wali array)
- We start a loop which stops if we are outside of any of the array
  - if current cookie size is >= greed of child, we just assign it to that child and move further
  - else we move only cookie pointer ahead
- we return cuurent value of i, which was pointing to greed,as that's the number of satisfied children

```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        //g is greed factor(min size of cookie that child will be content with)
        //s is size of cookie
        //If s[j] >= g[i], we can assign the cookie j to the child i
        sort(g.begin(),g.end());
        sort(s.begin(),s.end());
        int i=0,j=0;
        while(i<g.size() && j<s.size()){
            if(g[i]<=s[j]){ //child can eat cookie of size equals to or greater to child's greed
                i++;
                j++;
            }
            else{
                j++;
            }
        }
        return i;
    }
};
```
