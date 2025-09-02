# PROBLEM
<img width="642" height="759" alt="image" src="https://github.com/user-attachments/assets/b832b3fc-6a76-4ada-9420-641596c9c227" />

<img width="1048" height="612" alt="image" src="https://github.com/user-attachments/assets/713972e5-1aba-4bc7-b64a-d9e1d6d3219a" />
<img width="1022" height="145" alt="image" src="https://github.com/user-attachments/assets/4a189e52-ba59-4938-aa71-db5421619d20" />
<img width="1035" height="452" alt="image" src="https://github.com/user-attachments/assets/90a92db7-9894-4c04-a5c5-c7242bfc4278" />
<img width="982" height="502" alt="image" src="https://github.com/user-attachments/assets/53a7bb53-256a-4f0c-a923-cb26fbde10ab" />
<img width="1019" height="471" alt="image" src="https://github.com/user-attachments/assets/3b3f66ec-9c7c-4322-a362-fe43fb41b5b2" />

---

# INTUITION
## GET BRUTE FORCE FROM THE Aug-2025 FOLDER
<img width="1215" height="592" alt="image" src="https://github.com/user-attachments/assets/f3a1159e-e452-41fd-a49a-8c9155f11aad" />
<img width="1262" height="598" alt="image" src="https://github.com/user-attachments/assets/131a60d7-e5d9-4616-af83-bd330edb7b21" />
<img width="825" height="408" alt="image" src="https://github.com/user-attachments/assets/3cbba1bc-dffb-48a6-9e52-ce85f9fd615e" />

```
Total elements between arr[i1] and arr[j1]     →  arr[j1] - arr[i1] + 1
Number of val elements in this range           →  j1 - i1 + 1
Therefore, number of non-val elements          →  (arr[j1] - arr[i1] + 1) - (j1 - i1 + 1)
                                               =  (arr[j1] - arr[i1]) - (j1 - i1)
```

# Optimal : SLIDING WINDOWS : CODE 
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

# OPTIMAL :TWO POINETRS : CODE

```
We we get that `Subarray Valid : Property[i...j] <= k` in problemns then
we need to use the Two pointers technique to solve that problem in O(n) time complexity

Apply to current problem
In this problem We are knowing the I and J indices such that I <= J and in that indices
we want the count of how many elements which are not equal to that particular element And
that count <= K if it does then only the subarray is valid otherwise it's not

here as we want the longest subarray,
    we increment j when Property[i...j] <= k is valid
otherwise
    we increment i
```

```
#include <iostream>
#include <vector>
using namespace std;

typedef long long ll;

int main() {
    ll n, k;
    cin >> n >> k;

    vector<ll> b(n + 1);
    for (ll i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // Store positions (indices) of each unique number
    vector<vector<ll>> G(100001);  // G[val] = list of indices where val occurs
    for (ll i = 1; i <= n; i++) {
        G[b[i]].push_back(i);
    }

    ll answer = 0;

    // Try each value as the "target" value we want to make a contiguous block of
    for (ll current = 1; current <= 100000; current++) {
        auto &indices = G[current];
        if (indices.empty()) continue;

        // Two pointers: sliding window over positions of current value
        ll i = 0;  // left pointer
        for (ll j = 0; j < (ll)indices.size(); j++) {
            // Calculate number of non-current elements between indices[i] and indices[j]
            ll nonCurrent = (indices[j] - indices[i]) - (j - i);  // Total length - count of current value

            // If non-current elements exceed k, shrink window from the left
            while (nonCurrent > k) {
                i++;  // Move left pointer
                nonCurrent = (indices[j] - indices[i]) - (j - i);
            }

            // Now the window [i...j] is valid → update answer
            answer = max(answer, j - i + 1);
        }
    }

    cout << answer << "\n";
    return 0;
}

```


# TIME COMPLEXITY ANALYSIS
<img width="1029" height="507" alt="image" src="https://github.com/user-attachments/assets/b447ef16-c7d7-4b2b-a1a8-d1efc2661f4c" />

<img width="880" height="337" alt="image" src="https://github.com/user-attachments/assets/52d9619e-df1a-4ec7-ac3a-815626be0a76" />
<img width="1017" height="197" alt="image" src="https://github.com/user-attachments/assets/caabd1f5-5818-4dab-96bd-de6490775346" />
<img width="1009" height="700" alt="image" src="https://github.com/user-attachments/assets/90d8fb95-e9d3-41e7-a8e8-1645a8b64f35" />
