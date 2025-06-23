<!-- ## 1. Contains Duplicate

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
js
Copy
Edit
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

-->