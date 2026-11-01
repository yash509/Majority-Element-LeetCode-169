# Majority Element - Boyer-Moore Voting Algorithm

## Problem Statement
Given an array `nums` of size `n`, return the **majority element**.

The majority element is the element that appears more than `⌊n / 2⌋` times.  
You may assume that the majority element **always exists** in the array.

### Examples

**Example 1:**

Input: nums = [3,2,3]
Output: 3

**Example 2:**

Input: nums = [2,2,1,1,1,2,2]
Output: 2


---

## Approach: Boyer-Moore Voting Algorithm

This is an efficient linear-time and constant-space solution.

### Intuition
- We maintain a `candidate` and a `count`.
- Whenever `count` becomes zero, we pick the current element as the new candidate.
- If the current element matches the candidate → increment `count`
- Else → decrement `count`

Because the majority element appears more than `n/2` times, it can never be completely cancelled out. Hence, the final candidate is guaranteed to be the majority element.

### Dry Run (Example)

**Input:** `[2, 2, 1, 1, 1, 2, 2]`

| Step | Num | Count (before) | Action                        | Candidate | Count (after) |
|------|-----|----------------|-------------------------------|-----------|---------------|
| 1    | 2   | 0              | Set candidate = 2             | 2         | 1             |
| 2    | 2   | 1              | Match → count++               | 2         | 2             |
| 3    | 1   | 2              | Mismatch → count--            | 2         | 1             |
| 4    | 1   | 1              | Mismatch → count--            | 2         | 0             |
| 5    | 1   | 0              | Set candidate = 1             | 1         | 1             |
| 6    | 2   | 1              | Mismatch → count--            | 1         | 0             |
| 7    | 2   | 0              | Set candidate = 2             | 2         | 1             |

**Result:** `2`

---

## Complexity Analysis
- **Time Complexity:** O(n) — Single pass through the array
- **Space Complexity:** O(1) — Only two extra variables used

---

## Code (C++)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int candidate = 0;
        int count = 0;
        
        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }
        
        return candidate;
    }
};




