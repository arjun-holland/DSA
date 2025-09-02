# PROBLEM
<img width="642" height="759" alt="image" src="https://github.com/user-attachments/assets/b832b3fc-6a76-4ada-9420-641596c9c227" />

<img width="1048" height="612" alt="image" src="https://github.com/user-attachments/assets/713972e5-1aba-4bc7-b64a-d9e1d6d3219a" />
<img width="1022" height="145" alt="image" src="https://github.com/user-attachments/assets/4a189e52-ba59-4938-aa71-db5421619d20" />
<img width="1035" height="452" alt="image" src="https://github.com/user-attachments/assets/90a92db7-9894-4c04-a5c5-c7242bfc4278" />
<img width="982" height="502" alt="image" src="https://github.com/user-attachments/assets/53a7bb53-256a-4f0c-a923-cb26fbde10ab" />
<img width="1019" height="471" alt="image" src="https://github.com/user-attachments/assets/3b3f66ec-9c7c-4322-a362-fe43fb41b5b2" />

---

# BRUTE FORCE : INTUITION
<img width="876" height="363" alt="image" src="https://github.com/user-attachments/assets/b1c7ef0e-3447-45d3-8072-413602543b28" />
<img width="1219" height="444" alt="image" src="https://github.com/user-attachments/assets/1708ff38-9f27-45db-9d6c-ba1e548703f6" />
<img width="1215" height="592" alt="image" src="https://github.com/user-attachments/assets/f3a1159e-e452-41fd-a49a-8c9155f11aad" />
<img width="1262" height="598" alt="image" src="https://github.com/user-attachments/assets/131a60d7-e5d9-4616-af83-bd330edb7b21" />

<img width="825" height="408" alt="image" src="https://github.com/user-attachments/assets/3cbba1bc-dffb-48a6-9e52-ce85f9fd615e" />

# BRUTE FORCE : CODE 1
```
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

typedef long long ll;

const int MAX = 100005;

int main() {
    ll n, k;
    cin >> n >> k;  // Input: size of array and max elements to remove

    vector<ll> b(n + 1);  // 1-based indexing
    vector<ll> G[MAX];    // Adjacency list: G[value] = list of positions

    // Read input array
    for (ll i = 1; i <= n; i++) {  //This is a simple O(n) operation.
        cin >> b[i];
        G[b[i]].push_back(i);  // Store index i for value b[i]
    }

    ll answer = 0;
 
    // Try for every possible value from 1 to MAX
    for (ll val = 1; val < MAX; val++) {//But most values in that range do not appear in the input array.
        ll sz = G[val].size();
        if (sz > 0) {
            vector<ll> indices = G[val];  // Positions where value == val

            // Try all pairs of indices (i1, j1) to form subarrays
            for (ll i1 = 0; i1 < indices.size(); i1++) {   //O(n^2)
                for (ll j1 = i1; j1 < indices.size(); j1++) {
                    ll start = indices[i1];    // Start index in original array
                    ll end = indices[j1];      // End index in original array

                    ll totalSegmentLength = end - start + 1; // total elements in segment
                    ll countOfVal = j1 - i1 + 1;             // how many `val` in this segment

                    ll removalsNeeded = totalSegmentLength - countOfVal;

                    // If we can remove enough non-val elements to make it contiguous
                    if (removalsNeeded <= k) {
                        answer = max(answer, countOfVal);
                    }
                }
            }
        }
    }

    cout << answer << endl;  // Output: maximum length of valid subarray
    return 0;
}
//TC:O(n^2)
//SC:O(n)
```


# BRUTE FORCE : CODE 2
```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    ll n, k;
    cin >> n >> k;

    // Input array (1-based indexing for convenience)
    vector<ll> b(n + 1);
    for (ll i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // Group the indices of each value in the array
    // G[x] will store all positions (indices) where the value x appears
    vector<vector<ll>> G(100001);     //same as unordered_map<int,vector<int>>
    for (ll i = 1; i <= n; i++) {
        G[b[i]].push_back(i);
    }

    ll answer = 0;

    // Try to maximize for each distinct value (1 to 100000)
    for (ll val = 1; val <= 100000; val++) {
        auto &arr = G[val];  // Get list of indices where value == val
        if (arr.empty()) continue;  // Skip if this value doesn't exist

        ll i1 = 0;

        // Use a sliding window over the indices of value `val`
        for (ll j1 = 0; j1 < (ll)arr.size(); j1++) {
            // While the number of non-val elements between arr[i1] and arr[j1] is more than k, move left pointer
            //
            // Formula:
            // arr[j1] - arr[i1] + 1 → total elements in this window of original array
            // (j1 - i1 + 1) → number of val elements in this window
            // Difference = number of elements to remove = total - val_count
            //
            // Simplified as:
            // (arr[j1] - arr[i1]) - (j1 - i1) > k  ⟹ need to shrink window
            while (i1 <= j1 && (arr[j1] - arr[i1] - (j1 - i1)) > k) {
                i1++;
            }

            // Update answer with the size of the current valid window
            answer = max(answer, j1 - i1 + 1);
        }
    }

    // Output the maximum length of subarray with all equal elements after removing ≤ k elements
    cout << answer << "\n";
    return 0;
}
//TC:O(n^2)
//SC:O(n)

```
