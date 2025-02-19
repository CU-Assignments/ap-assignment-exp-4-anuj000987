# experiment-no.-4-22BCS_IOT-701B
https://leetcode.com/problems/longest-nice-substring/description/
https://leetcode.com/problems/maximum-subarray/description/
Experiment no. 4
# README

## Overview
This repository contains Java implementations of two well-known problems:
1. **Maximum Subarray (Kadane's Algorithm)**: Finds the contiguous subarray with the largest sum.
2. **Longest Nice Substring**: Finds the longest substring where every letter appears in both uppercase and lowercase.

## Solutions

### 1. Maximum Subarray
**Problem Statement:**
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Solution Approach:**
- We use **Kadane's Algorithm**, which maintains a running sum and updates the maximum sum found so far.
- At each step, we decide whether to extend the current subarray or start a new one.
- **Time Complexity:** `O(n)` (Linear Time Complexity)

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int maxSum = nums[0];  // Store the maximum sum found
        int currentSum = nums[0];  // Running sum of the subarray

        for (int i = 1; i < nums.length; i++) {
            // Either continue the current subarray or start a new one
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }

        return maxSum;
    }

    // Main function for testing
    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.maxSubArray(new int[]{-2,1,-3,4,-1,2,1,-5,4})); // Output: 6
        System.out.println(sol.maxSubArray(new int[]{1}));                     // Output: 1
        System.out.println(sol.maxSubArray(new int[]{5,4,-1,7,8}));            // Output: 23
    }
}
```

---

### 2. Longest Nice Substring
**Problem Statement:**
A string is "nice" if for every letter of the alphabet it contains, it appears in both uppercase and lowercase. Given a string `s`, return the longest nice substring of `s`. If there are multiple answers, return any. If no such substring exists, return an empty string.

**Solution Approach:**
- If the string is too short (`length < 2`), return `""`.
- Iterate through the string and find a character that does not have its uppercase/lowercase counterpart.
- Recursively check both substrings after splitting at that character and return the longest nice substring.
- **Time Complexity:** `O(n^2)` (Recursive calls for each partitioning)

```java
class Solution {
    public String longestNiceSubstring(String s) {
        if (s.length() < 2) return "";

        // Check if the string is nice
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (s.indexOf(Character.toUpperCase(c)) != -1 && s.indexOf(Character.toLowerCase(c)) != -1) {
                continue;
            }

            // If c is an unpaired letter, split at i and check both parts
            String left = longestNiceSubstring(s.substring(0, i));
            String right = longestNiceSubstring(s.substring(i + 1));

            return left.length() >= right.length() ? left : right;
        }

        return s;  // If no unpaired characters are found, the whole string is nice
    }

    // Main function for testing
    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.longestNiceSubstring("YazaAay"));  // Output: "aAa"
        System.out.println(sol.longestNiceSubstring("Bb"));       // Output: "Bb"
        System.out.println(sol.longestNiceSubstring("c"));        // Output: ""
    }
}
```

---

## Running the Code
To execute the solutions, follow these steps:
1. Copy and paste the respective class into a Java environment (e.g., an IDE like IntelliJ or Eclipse, or a text editor with `javac`).
2. Compile and run the Java file using:
   ```sh
   javac Solution.java
   java Solution
   ```
3. Observe the output in the console.

---

## Complexity Analysis
| Problem | Time Complexity | Space Complexity |
|---------|----------------|------------------|
| Maximum Subarray | `O(n)` | `O(1)` |
| Longest Nice Substring | `O(n^2)` | `O(n)` (recursive calls) |

---

## Author
This repository was created as a demonstration of Java algorithms for solving common array and string problems.

