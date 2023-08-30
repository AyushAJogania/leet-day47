# leet-day47

# Edit Distance Problem

## Problem Statement

Given two strings `word1` and `word2`, you need to determine the minimum number of operations required to convert `word1` to `word2`. You are allowed to perform the following three operations on a word:

1. Insert a character
2. Delete a character
3. Replace a character

Return the minimum number of operations needed.

## Example

**Input:**
```
word1 = "horse", word2 = "ros"
```

**Output:**
```
3
```

**Explanation:**
1. Convert "horse" to "rorse" by replacing 'h' with 'r'.
2. Convert "rorse" to "rose" by removing 'r'.
3. Convert "rose" to "ros" by removing 'e'.

Hence, the minimum number of operations is 3.

## Approach

This problem can be efficiently solved using dynamic programming. We can create a 2D DP matrix `dp`, where `dp[i][j]` represents the minimum number of operations required to convert the first `i` characters of `word1` to the first `j` characters of `word2`.

The base cases are when either of the words is empty. In that case, the number of operations required would be equal to the length of the other word.

For the general cases, we have three possibilities:
1. If the current characters of both words match, we don't need any operation, so `dp[i][j] = dp[i-1][j-1]`.
2. If the characters don't match, we have three options: insert, delete, or replace. So, `dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])`.

## Complexity Analysis

- Time complexity: O(m * n), where `m` is the length of `word1` and `n` is the length of `word2`.
- Space complexity: O(m * n) for the DP matrix.

## Implementation

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = word1.size();
        int n = word2.size();

        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

        for (int i = 0; i <= m; ++i) {
            for (int j = 0; j <= n; ++j) {
                if (i == 0) {
                    dp[i][j] = j;
                } else if (j == 0) {
                    dp[i][j] = i;
                } else if (word1[i - 1] == word2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + min(dp[i - 1][j], min(dp[i][j - 1], dp[i - 1][j - 1]));
                }
            }
        }

        return dp[m][n];
    }
};
```

## Conclusion

The "Edit Distance" problem can be efficiently solved using dynamic programming. By carefully considering the base cases and possible operations, we can determine the minimum number of operations required to convert one word into another. This solution is highly optimized and efficient for solving the problem on LeetCode.
