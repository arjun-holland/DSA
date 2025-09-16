# PROBLEM
<img width="942" height="613" alt="image" src="https://github.com/user-attachments/assets/f76d9e4b-a24c-4884-9b52-a835cf3a1a0c" />

# INTUITION
<img width="934" height="253" alt="image" src="https://github.com/user-attachments/assets/98ac7745-f4dc-46e4-9cf0-3665369ea7df" />

## BRUTE FORCE :-> O(N^2) -> Iterate all the subarrays (i,j) 

---

## OPTIMAL : O(n log n) -> Binary search
```
       Let us say index “l” is fixed; 
-> sum(l…..r) - sum(1 …..l-1) <= t
-> sum(l…..r) <= [t + sum(1…..l-1)] -> constant 
-> All this works when “l” is constant -> fix your “l” -> and now try to find the longest valid subarray starting at index “l”

-> do this process for each index “l” 
-> At each index “l” -> try [l,l] if it works try [l,l+1] , then try [l,l+2] …. Until it hits a point of breaking and
   point just before breaking the maximum longest [l…..r] which is valid longest subarray 

==> OBSERVATION : 
-> Linear search can be optimized using binary search because the function looks like -> TTTTTTTTTTTTTTFFFFFFFFFFFFFFFF
-> You have to find last occurrence of T 
```

```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

/*
Find largets subarray(l.....r) such that : sum(l...r) ≤ t + prefix[l−1]
TC : O(N log N) (loop over l × binary search on r).
*/

ll n, t;
vector<ll> a, prefix;


ll binary_search(ll l, ll target) {
    ll start = l, end = n;
    ll rp = -1; // stores the farthest valid r

    while (start <= end) {
        ll mid = (start + end) / 2;

        // Calculate sum(l...mid) using prefix sums
        ll sum_lr = prefix[mid] - prefix[l - 1];

        if (sum_lr <= target) {
            rp = mid;          // this mid is valid
            start = mid + 1;   // try extending further to the right
        } else {
            end = mid - 1;     // shrink search space (too large sum)
        }
    }
    return rp; // farthest valid r for this l
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    // Input size of array (n) and threshold t
    cin >> n >> t;

    // Array is 1-indexed for convenience with prefix sums
    a.resize(n + 1);
    prefix.assign(n + 1, 0);

    // Build prefix sum array
    // prefix[i] = sum of first i elements (a[1] + ... + a[i])
    for (ll i = 1; i <= n; i++) {
        cin >> a[i];
        prefix[i] = prefix[i - 1] + a[i];
    }

    ll answer = 0; // stores maximum length of valid subarray

    // Fix left index l and find the farthest r
    for (ll l = 1; l <= n; l++) {
        // Allowed maximum sum(l...r) = t + prefix[l-1]
        ll target = t + prefix[l - 1];

        // Binary search to find farthest valid r for this l
        ll best_r = binary_search(l, target);

        if (best_r != -1) {  // length of subarray [l...best_r]
            answer = max(answer, best_r - l + 1);
        }
    }

    // Output the longest valid subarray length
    cout << answer << "\n";
    return 0;
}

```


---

## OPTIMAL : O(n) -> Two Pointers Because of as the elements in Prefix array are increasiung
```
Two Pointers : prefix sums are non-decreasing
Because of the monotonic nature( elements are increasing / decreasing ) of the problem -> you can apply two pointers to it and solve in O(2*N==N) time; 
      Two ptr logic -> 
      Let us say -> sum(l…..r) <= [t + sum(1…..l-1)]
      So now you try for r+1 
      Let -> sum(l…..r+1) <= [t + sum(1…..l-1)]
      So now you try for r+2 but you fail ->
      ->  sum(l…..r+2) > [t + sum(1…..l-1)]

-> So its decided that for this l -> r+1 is the best choice hence [l….r+1] is longest possible subarray starting at index l 
-> now you can do l+1 and start checking for largest subarray starting at index l+1 
-> one is guaranteed -> [l…..r+1] is valid hence [l+1…..r+1] will also be valid {as elemnts are incresing nature}
-> l can be incremented -> 
      sum(l……r+1) <= [t + sum(1…..l-1)] -> valid; 
      sum(l+1…..r+1) <= sum(l…..r+1) <= [t + sum(1…..l-1)] <= [t+sum(1…….l)]
      -> Hence mathematically proved -> sum(l+1……r+1)<=[t+sum(1…….l)]
```

```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    ll n, t;
    cin >> n >> t;

    // Input array (1-indexed for easier prefix sum handling)
    vector<ll> a(n + 1);
    // prefix[i] = sum of first i elements
    vector<ll> prefix(n + 1, 0);

    for (ll i = 1; i <= n; i++) {
        cin >> a[i];
        prefix[i] = prefix[i - 1] + a[i];
    }

    ll answer = 0;
    ll l = 1, r = 1; // window is [l...r], start with both pointers at 1

    // Loop over all possible starting indices l
    for (l = 1; l <= n; l++) {
        // Derived from: sum(l...r) <= t + prefix[l-1]
        ll target = t + prefix[l - 1];

        // Expand r forward as long as sum(l...r) <= target
        // Note: sum(l...r) = prefix[r] - prefix[l-1]

        while (r <= n && prefix[r] <= target) {
            r++;    // move right pointer to include more elements
        }

        r--;   // the last increment went 1 step too far, so backtrack

        // Now [l...r] is the longest valid subarray starting at l
        answer = max(answer, r - l + 1);

        // Important: when l increases in the next iteration, we DO NOT reset r back, because prefix sums are non-decreasing
        // → the previous r is still a valid starting point for the new l
    }

    // Print the maximum length found
    cout << answer << "\n";
    return 0;
}
//TC : O(N)
```

<img width="746" height="192" alt="image" src="https://github.com/user-attachments/assets/581c7749-f2ff-4ae4-b19b-98f085757673" />
