# Problem
<img width="608" height="373" alt="image" src="https://github.com/user-attachments/assets/9a9295ff-9f87-4eb9-93aa-5fbbed389c86" />
<img width="604" height="330" alt="image" src="https://github.com/user-attachments/assets/bc021d89-6fc4-43e0-972c-1e0c180926b9" />
<img width="588" height="546" alt="image" src="https://github.com/user-attachments/assets/0d2911e2-f94a-462f-9f1a-7820a21456f1" />

# Intuition
| x  | Optimal Grouping | Total Ops | Why                            | 
| -- | ---------------- | --------- | ------------------------------ |
| 1  | ❌ Not possible   | -1        | Cannot remove 1 alone          |
| 2  | 2                | 1         | One group of 2                 |
| 3  | 3                | 1         | One group of 3                 |
| 4  | 2 + 2            | 2         | Two groups of 2                |
| 5  | 3 + 2            | 2         | One group of 3, one group of 2 |
| 6  | 3 + 3            | 2         | Two groups of 3                |
| 7  | 3 + 2 + 2        | 3         | Three operations needed        |
| 8  | 3 + 3 + 2        | 3         | Best: two 3s and one 2         |
| 9  | 3 + 3 + 3        | 3         | Three groups of 3              |
| 10 | 3 + 3 + 2 + 2    | 4         | Best way to split              |

```
✅ Pattern
The minimum number of operations for any x ≥ 2 is: min_ops(x) = x / 3 + (x % 3 != 0)
if x = 4, 4/3 => 1
          (4%3 != 0)=>1
means we can form two operatins min in each we take 2 elements
```
# Code
```
#include <iostream>
#include <unordered_map>
#include <vector>
#include <algorithm>

using namespace std;

int minOperationsToDestroyArray(vector<int>& arr) {
    unordered_map<int, int> freqMap;
    for (int num : arr) {
        freqMap[num]++;
    }

    int minOperations = 0;
    for (auto& entry : freqMap) {
        int freq = entry.second;
        if (freq == 1) {
            return -1; // According to Tariquddin’s law
        } else {
            // According to Tanmai’s Law
            minOperations += freq / 3 + (freq % 3 != 0);
        }
    }
    return minOperations;
}

int main() {
    vector<int> arr = {1, 5, 5, 1, 1, 8, 8, 10, 10};
    int minOps = minOperationsToDestroyArray(arr);
    if (minOps == -1) {
        cout << "It's not possible to destroy the array" << endl;
    } else {
        cout << "Minimum number of operations to destroy the array-> " << minOps << endl;
    }
    return 0;
}

```
