# leet-day47

# Minimum Number of Operations to Make Array Non-Decreasing

## Problem Description

You are given an array `nums` of integers. In one operation, you can replace any element of the array with any two elements that sum to it. The goal is to find the minimum number of operations required to make the array sorted in non-decreasing order.

Write a function `minimumReplacement` that takes an array `nums` as input and returns the minimum number of operations needed.

## Example

### Input
```
nums = [3, 9, 3]
```

### Output
```
2
```

### Explanation
Here are the steps to sort the array in non-decreasing order:
1. Replace the 9 with 3 and 6 so the array becomes [3, 3, 6, 3].
2. Replace the 6 with 3 and 3 so the array becomes [3, 3, 3, 3, 3].
There are 2 steps to sort the array in non-decreasing order. Therefore, the output is 2.

## Approach

The given problem can be solved using a greedy approach. The key idea is to iterate through the array in reverse order, and for each element, try to break it into pieces so that the smaller piece is as large as possible but not larger than the previous element. This ensures that the array becomes non-decreasing.

1. Initialize a variable `prev` with the last element of the array.
2. Initialize a variable `ans` to keep track of the minimum number of operations.
3. Iterate through the array in reverse order from the second last element to the first:
   a. If the current element is greater than `prev`, calculate the total number of times it needs to be divided (denoted by `total_divide`) to make it less than or equal to `prev`. Update `prev` to the division result and add `total_divide` to `ans`.
   b. If the current element is not greater than `prev`, update `prev` to the current element.
4. Return the final value of `ans`.

## Complexity Analysis

- Time Complexity: The algorithm iterates through the array once in reverse order, which takes O(n) time, where n is the number of elements in the array.
- Space Complexity: The algorithm uses a constant amount of extra space for storing variables, so the space complexity is O(1).

## Implementation

```cpp
class Solution {
public:
    long long minimumReplacement(vector<int>& nums) {
        int n = nums.size();
        int prev = nums[n - 1];
        long long int ans = 0;

        int i = n - 2;
        while(i >= 0){
            if(nums[i] > prev){
                long long int total_divide = (nums[i] - 1)/prev;
                prev = nums[i]/(total_divide + 1);
                ans += total_divide;
            }
            else{
                prev = nums[i];
            }
            i--;
        }
        return ans;
    }
};
```

## Conclusion

The "Minimum Number of Operations to Make Array Non-Decreasing" problem can be efficiently solved using a greedy approach. By iterating through the array in reverse order and carefully breaking elements into pieces, we can determine the minimum number of operations needed to make the array sorted in non-decreasing order. The provided solution demonstrates a way to implement this approach in C++.
