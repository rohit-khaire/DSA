# Unique BST

[Leetcode](https://leetcode.com/problems/unique-binary-search-trees/)

[YT Visualization](https://youtube.com/shorts/QJTbwVhNTHw?si=EAd_olr2t2JLz7xC) 


# Approach - Using loop we get No. of Nodes and for that Number of nodes we calculate possible no. of BSTs

Let dp[i] = Number of unique BSTs that can be formed using i nodes.

Choose every node as the root.

If root is chosen:

Left subtree has root - 1 nodes.

Right subtree has nodes - root nodes.

Total BSTs for this root:

dp[left] * dp[right]

Sum this for every possible root. So that we can get d[i] as Sum of BSTs possible using i nodes (where each node is used as root and then calculation for no. of BSTs possible) 


> Each time we point NoOfNodes=2 to N, and then for each NoOfNodes we make roots

```cpp
class Solution {
public:
    int numTrees(int n) {
        vector<int> dp(n+1,0);
        dp[0]=1;
        dp[1]=1; //Means with Number of Nodes as 1, we can have 1 Unique BST
        for(int nodes=2;nodes<=n;nodes++){
            for(int root=1;root<=nodes;root++){ //when I have no. of nodes, I check possible Unique bsts by making each node as root
                int left = root-1; //left | root | right 
                int right = nodes-root;
                dp[nodes]+= dp[left]*dp[right];
            }
        }
        return dp[n];
    }
};
```

TC:O(N^2) and SC:O(N)
