# ✅ Problem:
You’re given an array b of size N.Each b[i] is the happiness you get by selecting that element.
You must select K elements to maximize total happiness.

# ✅ Greedy Logic:
Select the K largest elements — this gives the maximum possible sum.
Why greedy is correct? Because selecting the top K biggest values always yields the highest total — both locally and globally optimal.It's 
not possible for the selectiinig the K min numbers or min ,max numbers

# 💻 C++ Code:
```
#include <iostream>
#include <vector>
#include <algorithm>  // for sort()
using namespace std;

int maxHappiness(vector<int>& b, int k) {
    sort(b.begin(), b.end(), greater<int>());     // Sort the array in descending order

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
    int result = maxHappiness(b, k);
    cout << "Maximum happiness: " << result << endl;
    return 0;
}
```

# 🧠 Greedy Verification:
- Greedy Choice: Always take the next highest happiness value.
- Future Impact: No future choice can improve upon taking the current best.
- ✔️ Greedy choice property and optimal substructure hold → ✅ Greedy is optimal.
