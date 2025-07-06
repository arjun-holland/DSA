# ✅ Problem:
You’re given an array b of size N.Each b[i] is the happiness you get by selecting that element.
You must select K elements to miminize the total happiness.

# ✅ Greedy Logic:
Select the K largest elements — this gives the miminize possible sum.
Why greedy is correct? Because selecting the top K smallest values always yields the smallest total — both locally and globally optimal.It's 
not possible for the selectinig the K max numbers or min,max numbers

# 💻 C++ Code:
```
#include <iostream>
#include <vector>
#include <algorithm>  // for sort()
using namespace std;

int minHappiness(vector<int>& b, int k) {
    sort(b.begin(), b.end());     // Sort the array in ascending order

    int sum = 0;
    for (int i = 0; i < k; ++i) {   // Take the first k elements
        sum += b[i];
    }
    return sum;
}

int main() {
    int n, k;
    cout << "Enter size of array (N): ";
    cin >> n;
    vector<int> b(n);
    cout << "Enter the happiness values:\n";
    for (int i = 0; i < n; ++i) {
        cin >> b[i];
    }
    cout << "Enter number of elements to select (K): ";
    cin >> k;
    int result = minHappiness(b, k);
    cout << "Miminize happiness: " << result << endl;
    return 0;
}
```

# 🧠 Greedy Verification:
- Greedy Choice: Always take the next smallest happiness value.
- Future Impact: No future choice can improve upon taking the current best.
- ✔️ Greedy choice property and optimal substructure hold → ✅ Greedy is optimal.
