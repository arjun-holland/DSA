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


# intuition

## Gnerally
<img width="800" height="453" alt="image" src="https://github.com/user-attachments/assets/351df747-cf17-4696-9323-6022c349f563" />

## Observation
<img width="998" height="467" alt="image" src="https://github.com/user-attachments/assets/5ca9355e-5290-495a-a87a-549fece2f657" />
```
suffix_mex[] is a monotonic function (increasing or decreasing function)
                        |
                        |
       that means GREEDY can be applied on this
                        |
                        |
       that means Two pointers can be applied on this
```
<img width="932" height="460" alt="image" src="https://github.com/user-attachments/assets/ba18dbf2-cf6d-424e-948e-58664e508074" />
<img width="982" height="490" alt="image" src="https://github.com/user-attachments/assets/0d79e9e9-e4ba-45ff-9e3d-e0b36a78c177" />
<img width="982" height="472" alt="image" src="https://github.com/user-attachments/assets/247f022b-4d60-4a33-98ad-4f0eae977ba3" />
<img width="970" height="460" alt="image" src="https://github.com/user-attachments/assets/d618d8c4-9b2a-428d-aa34-477efccfc29d" />
<img width="949" height="463" alt="image" src="https://github.com/user-attachments/assets/b55d1690-8337-47e3-bcc8-a1bd09d5c252" />
<img width="881" height="449" alt="image" src="https://github.com/user-attachments/assets/68dcf474-63a4-435a-b030-d9d561da35f2" />
<img width="909" height="463" alt="image" src="https://github.com/user-attachments/assets/9dbffaf4-b296-4fcd-bcca-97b0065ac40b" />
<img width="909" height="464" alt="image" src="https://github.com/user-attachments/assets/ed60f7cd-98c1-4336-8262-94674f6ff703" />


# Optimal Code
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

vector<int> optimized_mex_partition(vector<int>& a) {
    int n = a.size();

    // Step 1: Compute suffix MEX array
    // suffix[i] = MEX of the subarray a[i..n-1]
    vector<int> suffix(n);
    set<int> seen;                   // To keep track of elements seen so far from the end
    int curr_mex = 0;

    for (int i = n - 1; i >= 0; --i) {
        seen.insert(a[i]);           // Add current element to the set
        while (seen.count(curr_mex)) // Find the current smallest missing number
            curr_mex++;
        suffix[i] = curr_mex;        // Store current MEX
    }
    
    // Step 2: Compute suffix1 array
    // suffix1[i] tells us the length of the segment starting at i that has MEX equal to suffix[i]
    vector<int> freq(2 * n + 5, 0);   // Frequency array to count occurrences
    vector<int> suffix1(n);
    int j = n - 1;

    freq[a[n - 1]]++;                // Start from the last element
    suffix1[n - 1] = n - 1;          // By default, segment starts and ends at the last element
    //ans[i] = j such that suffix[i] = mex[a[i],....,a[j]] 

    for (int i = n - 2; i >= 0; i--) {
        freq[a[i]]++;                // Include current element in the frequency count

        if (suffix[i] != suffix[i + 1]) {
            // If MEX changes, start a new segment
            suffix1[i] = suffix1[i + 1];
        } else {
            // If MEX doesn't change, try to shorten the segment
            int u = 0;
            while (u == 0 && j >= i) {
                freq[a[j]]--;           // Remove element from the end
                if (freq[a[j]] == 0) {
                    // If removing a[j] would change the MEX, stop and restore it
                    u = 1;
                    freq[a[j]]++;
                } else {
                    j--;
                }
            }
            suffix1[i] = j;
        }
    }

    // Step 3: Compute segment lengths
    // Convert from endpoint index to actual length of each segment
    for (int i = n - 1; i >= 0; i--) {
        suffix1[i] = abs(i - suffix1[i]) + 1;
    }

    // Step 4: Build the result: the list of MEX values of each segment
    vector<int> result;
    int i = 0;
    while (i < n) {
        result.push_back(suffix[i]);  // Add the MEX of current segment
        i += suffix1[i];              // Move to the next segment
    }

    return result;
}

int main() {
    int n;
    cin >> n;
    vector<int> a(n);
    for (auto &x : a) cin >> x;

    vector<int> res = optimized_mex_partition(a);
    for (int x : res) cout << x << " ";
    cout << "\n";
    return 0;
}
```

## JDoodle Link for optimla code
You can run the original code online here:  
https://www.jdoodle.com/ga/o3CXDXkSLg%2FqT7HJpXANuQ%3D%3D
