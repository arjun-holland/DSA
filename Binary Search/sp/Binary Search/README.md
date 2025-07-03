# 🔍 Binary Search

---

## 📌 What is Binary Search?

Binary Search is an efficient searching algorithm that finds the position of a target element in a **sorted array or list**.  
It works by repeatedly dividing the search interval in half, which makes it much faster than a linear search for large datasets.

---

## 🚀 Why Use Binary Search?

- ⚡ **Fast**: Time complexity is **O(log n)** — faster than linear search (**O(n)**).
- ✅ **Efficient**: Uses minimal space (constant space in iterative form).
- 📈 **Scalable**: Ideal for large datasets.
- 🧠 **Important**: Frequently asked in coding interviews and used in system-level algorithms.

---

## 🧠 How Binary Search Works

```text
1. Start with the entire sorted array.
2. Find the middle element.
3. Compare the middle element with the target:
   🔸 If equal → return index.
   🔸 If target < middle → search left half.
   🔸 If target > middle → search right half.
4. Repeat steps 2–3 until found or interval is empty.
```

## 🧮 Time and Space Complexity Of Binary Search

| Case         | Time Complexity | Space Complexity |
| ------------ | --------------- | ---------------- |
| Best Case    | O(1)            | O(1)             |
| Average Case | O(log n)        | O(1)             |
| Worst Case   | O(log n)        | O(1)             |


## 🧑‍💻 Implementation (C++)
🔸 Iterative Version
```
int binarySearch(const vector<int>& arr, int target) {
    int low = 0, high = arr.size() - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            low = mid + 1;   // the target must be present afetr mid value
        else
            high = mid - 1;     // the target must be present before mid value
    }

    return -1; // Not found
}
```

## 🔹 Recursive Version
```
int binarySearchRecursive(const vector<int>& arr, int low, int high, int target) {
    if (low > high) return -1;

    int mid = low + (high - low) / 2;

    if (arr[mid] == target)
        return mid;
    else if (arr[mid] < target)
        return binarySearchRecursive(arr, mid + 1, high, target);
    else
        return binarySearchRecursive(arr, low, mid - 1, target);
}
```

## 📎 Requirements
- The array must be sorted before applying Binary Search.
- Can work on both ascending or descending arrays (with adjusted logic).

## 📚 Applications
- Searching in sorted datasets
- Efficiently solving problems in competitive programming
- Used in libraries like std::binary_search() in C++
- Applied in databases, OS kernels, and networking

## 📌 Tip
You can also use the built-in function in C++ STL:
```
#include <algorithm>
bool found = binary_search(arr.begin(), arr.end(), target);
```
---
# upper_bound() and lower_bound()

| Function        | Meaning                                 | Returns        |
| --------------- | --------------------------------------- | -------------- |
| `lower_bound()` | First position where value **≥ target** | Iterator/index |
| `upper_bound()` | First position where value **> target** | Iterator/index |
```
Input:
vector<int> nums = {1, 3, 3, 5, 8, 8, 10};
int target = 8;
🔍 Visual Index View:
Index:     0   1   2   3   4   5   6
Values:    1   3   3   5   8   8   10
                          ↑   ↑
                        LB=4 UB=6
lower_bound(nums.begin(), nums.end(), 8)
Finds first index where value ≥ 8 → returns index 4

upper_bound(nums.begin(), nums.end(), 8)
Finds first index where value > 8 → returns index 6
```


