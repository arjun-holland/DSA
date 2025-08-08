```
When we need to cound all the pairs(i,j) in a Group of n items
                              |
                              |
                              |
  that means we have to select the 2 items from the n items
           where 2 items indicated the pair
                              |
                              |
                              |
  we have to use the combinatorics formula, nCr
          where r = 2 , nC2
```

<img width="773" height="133" alt="image" src="https://github.com/user-attachments/assets/e642bbbb-cad4-4f9e-8071-9ab464f01862" />

<img width="740" height="393" alt="image" src="https://github.com/user-attachments/assets/37eff08f-83f2-4c3a-9783-44864b6d0073" />
<img width="553" height="461" alt="image" src="https://github.com/user-attachments/assets/0d16e45d-69ec-42bc-a634-ab7843fb0c20" />


# Code
```
#include <iostream>

inline long long nC2(long long n) {
    // Handles cases where n < 2 automatically
    return (n >= 2) ? (n * (n - 1)) / 2 : 0;
}

int main() {
    std::cout << nC2(5) << "\n";  // 5 choose 2 = 10
    std::cout << nC2(2) << "\n";  // 1
    std::cout << nC2(1) << "\n";  // 0
    return 0;
}

```

# How to use it in problems
## 1. Counting equal element pairs
```
unordered_map<int, long long> freq;
for (int x : arr) freq[x]++;

long long totalPairs = 0;
for (auto &p : freq) {
    totalPairs += nC2(p.second);
}
```

## 2. Two-sum frequency approach
```
unordered_map<int, long long> freq;
for (int x : arr) freq[x]++;

long long totalPairs = 0;
for (auto &p : freq) {
    int x = p.first, y = target - x;
    if (freq.count(y)) {
        if (x == y) totalPairs += nC2(freq[x]);
        else totalPairs += freq[x] * freq[y];
    }
}
totalPairs /= 2; // because we counted each pair twice
```

### 3. Pairs by group (e.g., same remainder mod m)
```
vector<long long> bucket(m, 0);
for (int x : arr) bucket[x % m]++;

long long totalPairs = 0;
for (long long count : bucket) {
    totalPairs += nC2(count);
}

The Problem : We want to count how many unordered pairs (i, j) have the same remainder when divided by m.

For example:
arr = {2, 4, 6, 7, 9}
m = 4
Step 1 — Group numbers by remainder: remainder = number % m
          | Number | Remainder (mod 4) |
          | ------ | ----------------- |
          | 2      | 2                 |
          | 4      | 0                 |
          | 6      | 2                 |
          | 7      | 3                 |
          | 9      | 1                 |
So the bucket counts are:
remainder 0 → {4}       → count = 1
remainder 1 → {9}       → count = 1
remainder 2 → {2, 6}    → count = 2
remainder 3 → {7}       → count = 1

Step 2 — Count pairs inside each bucket
Why?
Because if two numbers have the same remainder, their difference is divisible by m.

Number of unordered pairs inside a group of size count is:

            nC2 = count⋅(count−1) / 2

Applying to each bucket:
Remainder 0 → count = 1 → nC2(1) = 0
Remainder 1 → count = 1 → nC2(1) = 0
Remainder 2 → count = 2 → nC2(2) = 1 → pair: (2, 6)
Remainder 3 → count = 1 → nC2(1) = 0
Total pairs = 0 + 0 + 1 + 0 = 1

Final Answer: Only one valid pair: (2, 6) because both have remainder 2 when divided by 4.
```

​

 
