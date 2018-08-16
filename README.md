---
description: 'Medium - Dynamic Programming, Binary Search Tree, Tree'
---

# 96. Unique Binary Search Trees

Given n, how many structurally unique BST's \(binary search trees\) that store values 1 ... n?

Example:

Input: 3  
Output: 5  
Explanation:  
Given n = 3, there are a total of 5 unique BST's:

```text
  1         3     3      2      1  
   \       /     /      / \      \  
    3     2     1      1   3      2  
   /     /       \                 \  
  2     1         2                 3
```

{% hint style="info" %}
Every value from 1 to n can be the root, than values smaller than it goes to its left subtree and bigger goes to right subtree, this goes recursively to its subtrees.

For BST every value is different, thus for any tree with n nodes, the number of structurally unique BST is same, suppose G\(n\).

For each selected root, \# of diff BSTs should be the multiplex of G\(\#nodes in its left subtree\) \* G\(\#nodes in its right subtree\)

The total number of BSTs should be SUM\(G\(0\) \* G\(n - 1\) + G\(1\) \* G\(n - 2\) + ... + G\(n - 1\) \* G\(0\)\), it's easy to see that to get G\(n\), we need to know G\(0\) ... G\(n - 1\) beforehand.

Thus this can be solved using DP, with base case G\(0\) = 1 \(null\). G\(1\) = 1\(single node as root\).
{% endhint %}

```java
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2; i < n + 1; i ++) {
            for(int j = 1; j <= i; j ++) {
                dp[i] += dp[j - 1] * dp[i - j];
            }
        }
        return dp[n];
    }
}
```

