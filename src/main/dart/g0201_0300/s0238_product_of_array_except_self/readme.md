[![](https://img.shields.io/github/stars/LeetCode-in-Dart/LeetCode-in-Dart?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Dart/LeetCode-in-Dart)
[![](https://img.shields.io/github/forks/LeetCode-in-Dart/LeetCode-in-Dart?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Dart/LeetCode-in-Dart/fork)

## 238\. Product of Array Except Self

Medium

Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

**Input:** nums = [1,2,3,4]

**Output:** [24,12,8,6]

**Example 2:**

**Input:** nums = [-1,1,0,-3,3]

**Output:** [0,0,9,0,0]

**Constraints:**

*   <code>2 <= nums.length <= 10<sup>5</sup></code>
*   `-30 <= nums[i] <= 30`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

**Follow up:** Can you solve the problem in `O(1) `extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)

## Solution

```dart
class Solution {
  List<int> productExceptSelf(List<int> nums) {
    int product = 1;
    List<int> ans = List.filled(nums.length, 0);

    // Calculate total product of all elements
    for (int num in nums) {
      product *= num;
    }

    // Fill in the result array
    for (int i = 0; i < nums.length; i++) {
      if (nums[i] != 0) {
        ans[i] = product ~/ nums[i]; // Integer division
      } else {
        int p = 1;
        for (int j = 0; j < nums.length; j++) {
          if (j != i) {
            p *= nums[j];
          }
        }
        ans[i] = p;
      }
    }

    return ans;
  }
}
```