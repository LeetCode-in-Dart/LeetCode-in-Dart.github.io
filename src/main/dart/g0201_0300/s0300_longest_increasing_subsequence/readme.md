[![](https://img.shields.io/github/stars/LeetCode-in-Dart/LeetCode-in-Dart?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Dart/LeetCode-in-Dart)
[![](https://img.shields.io/github/forks/LeetCode-in-Dart/LeetCode-in-Dart?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Dart/LeetCode-in-Dart/fork)

## 300\. Longest Increasing Subsequence

Medium

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`.

**Example 1:**

**Input:** nums = [10,9,2,5,3,7,101,18]

**Output:** 4

**Explanation:** The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

**Example 2:**

**Input:** nums = [0,1,0,3,2,3]

**Output:** 4

**Example 3:**

**Input:** nums = [7,7,7,7,7,7,7]

**Output:** 1

**Constraints:**

*   `1 <= nums.length <= 2500`
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

**Follow up:** Can you come up with an algorithm that runs in `O(n log(n))` time complexity?

## Solution

```dart
class Solution {
  int lengthOfLIS(List<int> nums) {
    if (nums == null || nums.isEmpty) {
      return 0;
    }

    List<int> dp = List.filled(nums.length + 1, 0);
    // Prefill the dp table with a maximum value.
    for (int i = 1; i < dp.length; i++) {
      dp[i] = 1 << 31 - 1;
    }

    int left = 1;
    int right = 1;

    for (int curr in nums){
      int start = left;
      int end = right;

      // Binary search, find the position to update in dp
      while (start + 1 < end) {
        int mid = start + (end - start) ~/ 2;
        if (dp[mid] > curr) {
          end = mid;
        } else {
          start = mid;
        }
      }

      // Update the dp table
      if (dp[start] > curr) {
        dp[start] = curr;
      } else if (curr > dp[start] && curr < dp[end]) {
        dp[end] = curr;
      } else if (curr > dp[end]) {
        dp[++end] = curr;
        right++;
      }
    }

    return right;
  }
}
```