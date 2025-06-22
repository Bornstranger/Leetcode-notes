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
