# Find the Missing Number

## 📝 Problem

Given an array `nums` containing `n` distinct numbers taken from the range `[0, n]`, return the only number in the range that is missing from the array.

### Example 1

```text
Input: nums = [3, 0, 1]
Output: 2
```

**Explanation:**  
There are 3 numbers, so the complete range is `[0, 3]`, or:

```text
0, 1, 2, 3
```

The number `2` is missing.

### Example 2

```text
Input: nums = [0, 1]
Output: 2
```

---

## 💡 Approaches

I solved this problem using three different approaches.

---

### Approach 1: Sorting

First, sort the array in ascending order. Then compare each number with the previous number. If the difference is greater than `1`, the missing number lies between them.

If `0` is missing, return `0`. If no gap is found, the missing number must be `n`.

```js
function missingNumberSorting(nums) {
  const sortedNumbers = [...nums].sort((a, b) => a - b);
  const len = sortedNumbers.length;

  if (sortedNumbers[0] !== 0) return 0;

  for (let i = 1; i < len; i++) {
    if (sortedNumbers[i] - sortedNumbers[i - 1] > 1) {
      return sortedNumbers[i - 1] + 1;
    }
  }

  return len;
}
```

**Time Complexity:** `O(n log n)`  
**Space Complexity:** Depends on the sorting implementation.

---

### Approach 2: Mathematical Sum

For numbers from `0` to `n`, the expected sum can be calculated using:

```text
n × (n + 1) / 2
```

Then calculate the sum of the numbers actually present in the array.

The difference between the expected sum and the actual sum is the missing number.

```js
function missingNumberSum(nums) {
  const n = nums.length;
  const expectedSum = (n * (n + 1)) / 2;

  let actualSum = 0;

  for (const num of nums) {
    actualSum += num;
  }

  return expectedSum - actualSum;
}
```

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(1)`

---

### Approach 3: XOR / Bit Manipulation

XOR has two useful properties:

```text
a ^ a = 0
a ^ 0 = a
```

If all numbers from `0` to `n` are XORed with all numbers in the array, every number that appears in both groups cancels out.

The only value remaining is the missing number.

```js
function missingNumberXOR(nums) {
  let missing = nums.length;

  for (let i = 0; i < nums.length; i++) {
    missing ^= i ^ nums[i];
  }

  return missing;
}
```

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(1)`

---

## 📊 Complexity Comparison

| Approach               | Time Complexity | Space Complexity  |
| ---------------------- | --------------- | ----------------- |
| Sorting                | `O(n log n)`    | Sorting dependent |
| Mathematical Sum       | `O(n)`          | `O(1)`            |
| XOR / Bit Manipulation | `O(n)`          | `O(1)`            |

---

## 🎯 What I Learned

This problem demonstrates that the same problem can be solved in multiple ways with different trade-offs.

The sorting approach is intuitive but requires `O(n log n)` time.

The mathematical approach improves the solution to `O(n)` time and `O(1)` extra space by comparing the expected sum with the actual sum.

The XOR approach also achieves `O(n)` time and `O(1)` space while demonstrating how bit manipulation can be used to cancel duplicate values.

---

## 🏷️ Topics

`Array` `Math` `Sorting` `Bit Manipulation`
