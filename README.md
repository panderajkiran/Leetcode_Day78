# Leetcode_Day78
# Day 78: Subarray Product Less Than K

**LeetCode Problem:** 713. Subarray Product Less Than K  
**Difficulty:** Medium  
**Topic:** Arrays, Sliding Window, Two Pointers  
**Language:** Java

---

## 📌 Problem Statement

Given an integer array `nums` and an integer `k`, find the number of contiguous subarrays whose product of elements is strictly less than `k`.

A subarray is a continuous part of an array.

**Important:** The product must be strictly less than `k`, not equal to it.

---

## 💡 Approach: Sliding Window

I solved this problem using the sliding window technique with two pointers.

Instead of checking every possible subarray, I maintain a window whose product is less than `k`.

### Steps

1. If `k <= 1`, return `0` because all array elements are positive integers.
2. Initialize `left = 0`, `prod = 1`, and `count = 0`.
3. Move the `right` pointer through the array and multiply each element into `prod`.
4. If `prod >= k`, shrink the window by dividing out elements from the left until the product becomes less than `k`.
5. For each valid window, add `right - left + 1` to the count.
6. Return the total count.

### Why `right - left + 1`?

When the current window is valid, every subarray ending at `right` and starting anywhere from `left` to `right` is also valid.

Therefore, the number of valid subarrays ending at the current position is:

`right - left + 1`

This allows us to count multiple subarrays in constant time.

---

## 💻 Java Solution

```java
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        if (k <= 1) {
            return 0;
        }

        int left = 0;
        int prod = 1;
        int count = 0;

        for (int right = 0; right < nums.length; right++) {
            prod *= nums[right];

            while (prod >= k) {
                prod /= nums[left];
                left++;
            }

            count += right - left + 1;
        }

        return count;
    }
}
```

---

## 🧪 Example

**Input:**

```text
nums = [10, 5, 2, 6]
k = 100
```

**Output:**

```text
8
```

**Explanation:**

The valid subarrays are:

- `[10]`
- `[5]`
- `[2]`
- `[6]`
- `[10, 5]`
- `[5, 2]`
- `[2, 6]`
- `[5, 2, 6]`

There are `8` subarrays whose products are strictly less than `100`.

---

## ⏱️ Complexity Analysis

- **Time Complexity:** O(n), because each element enters and leaves the sliding window at most once.
- **Space Complexity:** O(1), because only a constant number of extra variables are used.

---

## 📚 What I Learned

- How to use the sliding window technique for subarray problems.
- How two pointers help maintain a valid range.
- Why `right - left + 1` efficiently counts all valid subarrays ending at the current position.
- How shrinking a window helps satisfy a condition.
- How to improve on a brute-force solution by avoiding repeated calculations.

---

## 🎯 Takeaway

Today's problem taught me that sometimes we don't need to examine every possibility individually.

By maintaining a valid window and understanding how many subarrays it contains, we can solve the problem much more efficiently.

**Day 78 complete — learning to solve problems smarter, one window at a time!**
