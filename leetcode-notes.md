## 1. Contains Duplicate

### ✅ Approach

- Use a `Set` to track numbers we've seen.
- Iterate through the array:
  - If the number already exists in the Set, return `true` (duplicate found).
  - Otherwise, add it to the Set.
- If loop finishes without finding duplicates, return `false`.

### 🔍 Why this works:
- A `Set` only stores unique values.
- `Set.has()` gives O(1) average time complexity.
- So this approach is efficient and concise.

### 🧮 Complexity
- **Time**: O(n) — one pass through the array.
- **Space**: O(n) — in worst case, all unique values stored in the Set.

### 🧑‍💻 JavaScript Code
```js
var containsDuplicate = function(nums) {
   let set = new Set();

   for (let i of nums) {
     if (set.has(i)) return true;
     set.add(i);
   }

   return false;
};


## 2. Group Anagrams
### ✅ Approach

Use an object ({}) to group words by their letter frequency.

For each string:

-Create an array of size 26 initialized to 0 (representing a–z).

-Increment counts for each character in the string.

-Use the array as a key (converted to a string using join(',')).

-Push the word into the corresponding group.

-Finally, return the values of the object.

## 🔍 Why this works:
Anagrams have the same frequency of characters.

By using a character count signature as the key, all anagrams map to the same key.

Avoids sorting each word (which is slower).

## 🧮 Complexity
Time: O(N * K), where N = number of strings, K = max length of a string.

Space: O(N * K) — storing grouped anagrams and character count arrays.

## 🧑‍💻 JavaScript Code

class Solution {
  /**
   * @param {string[]} strs
   * @return {string[][]}
   */
  groupAnagrams(strs) {
    const res = {};
    for (let s of strs) {
      const count = new Array(26).fill(0);
      for (let c of s) {
        count[c.charCodeAt(0) - 'a'.charCodeAt(0)] += 1;
      }
      const key = count.join(',');
      if (!res[key]) {
        res[key] = [];
      }
      res[key].push(s);
    }
    return Object.values(res);
  }
} 

3. Valid Palindrome

✅ Approach
Use two pointers (l from start, r from end) to compare characters.

Skip non-alphanumeric characters using RegExp check (/[a-zA-Z0-9]/).

Normalize characters with .toLowerCase() before comparison.

If any mismatch is found, return false; otherwise, return true.

🔍 Why this works:
Palindromes should read the same forward and backward, ignoring punctuation, spaces, and case.

This approach efficiently skips irrelevant characters and compares only valid ones.

It avoids creating any new strings or arrays — it's in-place and minimal.

🧮 Complexity
Time: O(n) — traverses the string once from both ends.

Space: O(1) — no extra storage used.

🧑‍💻 JavaScript Code

var isPalindrome = function(s) {
    let l = 0; 
    let r = s.length - 1;

    while (l < r) {
        while (l < r && !/[a-zA-Z0-9]/.test(s[l])) l++;
        while (l < r && !/[a-zA-Z0-9]/.test(s[r])) r--;

        if (s[l].toLowerCase() !== s[r].toLowerCase()) {
            return false;
        }

        l++;
        r--;
    }

    return true;
};


4. Valid Parentheses
✅ Approach
Use a stack (res[]) to track open brackets.

Create a map obj to match closing → opening brackets.

Loop through each character:

If it’s a closing bracket, check if the top of the stack matches its corresponding opening.

If yes, pop() the opening from the stack.

If not, return false (mismatch).

If it’s an opening bracket, push it onto the stack.

After processing all characters, return true only if the stack is empty (all brackets matched).

🔍 Why this works:
Stack ensures last opened is first closed — exactly how valid parentheses work.

The map allows constant-time lookups to check for matching pairs.

Unmatched or unbalanced parentheses are detected immediately.

🧮 Complexity
Time: O(n) — each character is processed once.

Space: O(n) — in worst case, all opening brackets are pushed to the stack.

🧑‍💻 JavaScript Code

var isValid = function(s) {
    let obj = {
        ')': '(',
        '}': '{',
        ']': '['
    };

    let res = [];

    for (let i of s) {
        if (obj[i]) {
            if (res.length > 0 && res[res.length - 1] === obj[i]) {
                res.pop();
            } else {
                return false;
            }
        } else {
            res.push(i);
        }
    }

    return res.length === 0;
};


5.  Intersection of Two Arrays
This project contains a simple JavaScript function that returns the intersection of two arrays — that is, the elements common to both arrays, without duplicates.

📌 Problem Statement
Given two integer arrays nums1 and nums2, return an array of their intersection.
Each element in the result must be unique, and you may return the result in any order.

✅ Example

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4] or [4,9]

🔍 Approach
Convert both input arrays to Sets to eliminate duplicates.

Iterate through one set and check if each element exists in the other set.

If yes, push it to the result array.

Return the result.

This approach ensures time-efficient lookup using the Set.has() method.

🧠 Code Explanation

var intersection = function(nums1, nums2) {
    let set1 = new Set(nums1);      // Remove duplicates from nums1
    let set2 = new Set(nums2);      // Remove duplicates from nums2
    let res = [];

    for (let i of set1) {           // Loop through elements of set1
        if (set2.has(i)) {          // Check if element exists in set2
            res.push(i);            // Add common element to result
        }
    }

    return res;                     // Return intersection array
};

🕒 Time & Space Complexity
Time Complexity: O(n + m), where n and m are lengths of nums1 and nums2

Space Complexity: O(n + m), for the two sets used to remove duplicates

📄 License
This code is free to use for learning and educational purposes.


6.Two Sum II - Input Array Is Sorted
This project provides a solution to the Two Sum II problem, where you're given a sorted array and a target value, and you must find the indices of the two numbers that add up to the target.

📌 Problem Statement
Given a 1-indexed array of integers numbers that is sorted in non-decreasing order, and a target integer target, return the indices of the two numbers such that they add up to target.

You must use only constant extra space and must not modify the input array.

✅ Example

Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
// Explanation: 2 + 7 = 9, and their indices (1-based) are [1,2]

Input: numbers = [1,2,3,4,4,9,56,90], target = 8
Output: [4,5]

💡 Approach
This uses the Two-Pointer Technique since the input array is already sorted:

Initialize two pointers:

l (left) at the start of the array

r (right) at the end of the array

While l < r:

Calculate the sum of numbers[l] + numbers[r]

If the sum is less than the target, move l to the right (increase l)

If the sum is greater than the target, move r to the left (decrease r)

If the sum equals the target, return [l + 1, r + 1] (1-based indices)

🧠 Code Explanation

var twoSum = function(numbers, target) {
    let l = 0;                  // Left pointer
    let r = numbers.length - 1; // Right pointer

    while (l < r) {
        let sum = numbers[l] + numbers[r];
        if (sum < target) {
            l++;                // Move left pointer to increase sum
        } else if (sum > target) {
            r--;                // Move right pointer to decrease sum
        } else {
            return [l + 1, r + 1]; // Return 1-based indices
        }
    }
};

🕒 Time & Space Complexity

Time Complexity: O(n) — Each element is visited at most once.
Space Complexity: O(1) — No extra space used apart from variables.

📄 License
This code is free to use for practice, learning, and educational purposes.


7 Remove Element – LeetCode Solution

---

## 🧩 Problem Description

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` **in-place** and return the new length of the array.

Do not allocate extra space for another array — you must do this by modifying the input array in-place with **O(1)** extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.


---

## 💡 Example

Input: nums = [3, 2, 2, 3], val = 3  
Output: 2, nums = [2, 2, _, _]

Explanation: Your function should return length = 2, and the first two elements of nums should be 2.
It doesn't matter what you leave beyond the returned length.

✅ Constraints
0 <= nums.length <= 100

0 <= nums[i] <= 50

0 <= val <= 100

🚀 Solutions

✅ JavaScript
var removeElement = function(nums, val) {
    let k = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== val) {
            nums[k] = nums[i];
            k++;
        }
    }
    return k;
};

✅ Python

def removeElement(self, nums, val):
    k = 0
    for i in nums:
        if i != val:
            nums[k] = i
            k += 1
    return k

🧠 Explanation
k is a pointer to place valid elements (not equal to val).

If nums[i] !== val, the element is copied to index k, and k is incremented.

After the loop, k is the number of elements not equal to val.

🛡️ Key Takeaways
    In-place removal using the two-pointer technique
    O(n) time complexity
    O(1) space complexity

------------------------------------------------------------
8 Remove Duplicates from Sorted Array – LeetCode Solution

🧩 Problem Description

Given a **sorted array** `nums`, remove the duplicates **in-place** such that each element appears only **once** and return the new length.

Do **not** allocate extra space for another array.  
You must do this by modifying the input array **in-place** with **O(1)** extra memory.

## 💡 Example
```txt
Input: nums = [1, 1, 2]
Output: 2, nums = [1, 2, _]
Explanation: Your function should return 2, and the first two elements of nums should be 1 and 2.
It does not matter what values are left beyond the returned length.
````
✅ Constraints
1 <= nums.length <= 3 * 10^4

-100 <= nums[i] <= 100

nums is sorted in non-decreasing order

🚀 Solutions

✅ JavaScript (In-Place)

var removeDuplicates = function(nums) {
    if (nums.length === 0) return 0;

    let k = 1; // Points to the place to insert unique elements

    for (let i = 1; i < nums.length; i++) {
        if (nums[i] !== nums[i - 1]) {
            nums[k] = nums[i];
            k++;
        }
    }

    return k;
};

✅ Python (In-Place)

def removeDuplicates(self, nums):
    if not nums:
        return 0

    k = 1
    for i in range(1, len(nums)):
        if nums[i] != nums[i - 1]:
            nums[k] = nums[i]
            k += 1
    return k

🧠 How It Works
The array is already sorted.

You scan the array with a loop starting from index 1.

Each time you find a new unique number (i.e., different from the previous), you write it to index k.

k keeps track of the position to place the next unique value.

Return k as the new length of the array.

🛡️ Key Takeaways
    Efficient two-pointer approach
    Time Complexity: O(n)
    Space Complexity: O(1) (in-place)
    Original array is modified; no extra memory is used.

