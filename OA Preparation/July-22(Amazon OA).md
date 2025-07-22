# Preffix-Suffix-Greedy-Observation Version
## Problem
<img width="893" height="591" alt="image" src="https://github.com/user-attachments/assets/d44eea0a-1206-4bd6-85cb-72b781606b71" />

----

<img width="843" height="486" alt="image" src="https://github.com/user-attachments/assets/5dfd8c22-2c5f-47e1-a178-8f0e70dc4380" />

<img width="719" height="778" alt="image" src="https://github.com/user-attachments/assets/6e58c3aa-9778-40c5-bf2a-ed7d32f86bd7" />

<img width="756" height="414" alt="image" src="https://github.com/user-attachments/assets/3e3eb75f-c2fd-42ed-8f98-6ba29457984a" />

----
## Code : BRUTE FORCE O(N^2)
```
#include <bits/stdc++.h>
using namespace std;

// -----------------------------------------------------------------
// Function to compute the MEX (Minimum Excluded Value) of an array
// MEX is the smallest non-negative integer not present in the array
// Example: [0, 1, 3] → MEX = 2
// -----------------------------------------------------------------
int compute_mex(const vector<int>& arr) {
    unordered_set<int> st(arr.begin(), arr.end());

    // Try all integers from 0 to size of array
    for (int i = 0; i < arr.size(); ++i) {
        if (!st.count(i)) return i;  // First missing integer is MEX
    }
    return arr.size();  // All values 0..n-1 are present
}


// Main solve function to build the lexicographically largest result array
vector<int> solve(vector<int> a) {
    vector<int> result;  // To store the final result array

    // Repeat until array is empty
    while (!a.empty()) {
        // Step 1: Compute the MEX of the current full array
        int total_mex = compute_mex(a);

        // Step 2: Scan the array from the start and track seen elements
        unordered_set<int> seen;
        int prefix_mex = 0;  // MEX of current prefix being scanned

        for (int i = 0; i < a.size(); ++i) {
            seen.insert(a[i]);

            // Update prefix MEX (smallest number not in 'seen')
            while (seen.count(prefix_mex)) {
                prefix_mex++;
            }

            // When prefix MEX matches total MEX of array, we cut here
            if (prefix_mex == total_mex) {
                // Step 3: Add MEX to result
                result.push_back(total_mex);

                // Step 4: Remove this prefix (first i+1 elements)
                vector<int> remaining;
                for (int j = i + 1; j < a.size(); ++j) {
                    remaining.push_back(a[j]);
                }

                // Update the working array for next iteration
                a = remaining;

                // Done with this iteration
                break;
            }
        }
    }
    return result;
}


int main() {
    int n;
    cin >> n;

    vector<int> a(n);
    for (auto &x : a) {
        cin >> x;
    }

    vector<int> res = solve(a);

    // Output the result array
    for (int x : res) {
        cout << x << " ";
    }
    cout << "\n";

    return 0;
}
```

## 🔗 JDoodle Link

You can run the original code online here:  
[JDoodle Online Compiler](https://www.jdoodle.com/ga/2seu5K8zO%2BREj6u1yvPWKw%3D%3D)
