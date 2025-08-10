# Problem
<img width="1231" height="909" alt="image" src="https://github.com/user-attachments/assets/677ec475-8cfc-41ef-a4a0-5247306d66a8" />
<img width="1181" height="907" alt="image" src="https://github.com/user-attachments/assets/04c0b683-802c-454f-97d5-95737a60c0b2" />
<img width="1192" height="806" alt="image" src="https://github.com/user-attachments/assets/54774b67-8aed-4def-9c7b-58ba55aa9523" />


# Intuition
<img width="596" height="275" alt="image" src="https://github.com/user-attachments/assets/cf6b00ff-1848-43fe-93a7-00895d5de37a" />

```
    -> b[i] xor b[j] = b[k] xor b[l]
        =>        x  =  x
        =>        x xor x  = 0 {xor between same elements is 0}
        => b[i] xor b[j]  xor b[k] xor b[l] = 0
    -> b[i] xor b[l] = b[j] xor b[k]
        =>        x  =  x
        =>        x xor x  = 0 {xor between same elements is 0}
        => b[i] xor b[l]  xor b[j] xor b[k] = 0
so we deont need to check two equations we need to check one equation to know we can form a rectangle or not that is  => b[i] xor b[j]  xor b[k] xor b[l] = 0
```

```
                          unordered pair => (i, j) = (j, i) => so not countable in ans
                          
                          Ordered pair => (i, j) != (j, i) => so countable in ans
```


## Brute Force : (n ^ 4)
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        vector<int> a(n);
        for (int &x : a) cin >> x;

        long long ans = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (j == i) continue;
                for (int k = 0; k < n; k++) {
                    if (k == i || k == j) continue;
                    for (int l = 0; l < n; l++) {
                        if (l == i || l == j || l == k) continue;
                        if ((a[i] ^ a[j] ^ a[k] ^ a[l]) == 0) {
                            ans++;
                        }
                    }
                }
            }
        }
        cout << ans << "\n";
    }
    return 0;
}
```

## Optimal 1 : O(n^3)
<img width="730" height="388" alt="image" src="https://github.com/user-attachments/assets/db00d3c5-580d-474f-81c6-ac7145e458bd" />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int T;
    if (!(cin >> T)) return 0;
    while (T--) {
        int n;
        cin >> n;
        vector<int> a(n);
        for (int i = 0; i < n; ++i) cin >> a[i];

        long long ans = 0;

        // For every ordered pair (i, j), i != j
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                if (j == i) continue;

                // build frequency map of possible l indices (all indices except i and j)
                unordered_map<int,int> mp;
    
                for (int idx = 0; idx < n; ++idx) {
                    if (idx == i || idx == j) continue;
                    mp[a[idx]]++;
                }

                // Now iterate k (k != i, k != j)
                for (int k = 0; k < n; ++k) {
                    if (k == i || k == j) continue;

                    // remove k from candidate l's (l must be distinct from k)
                    auto itk = mp.find(a[k]);
                    if (itk != mp.end()) {
                        (itk->second)--;
                        if (itk->second == 0) mp.erase(itk);
                    }

                    int target = a[i] ^ a[j] ^ a[k];    // we need a[l] == target
                    auto it = mp.find(target);
                    if (it != mp.end()) ans += it->second;

                    // restore k back into mp for next iteration
                    mp[a[k]]++;

                }      // end for k
            }       // end for j
        }       // end for i

        cout << ans << '\n';
    }
    return 0;
}
```


## Optimal 1 : hashmap : O(n^2)

```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);

    int T; cin >> T;

    while (T--) {
        int N;
        cin >> N;
        vector<int> A(N);
        for (int i = 0; i < N; i++) {
            cin >> A[i];
        }

        ll c = 0; // count of unordered quadruples

        // freq map for XOR of unordered (k,l) pairs, where k < l
        unordered_map<int, int> freq;

        // STEP 1: Store all pairs (k,l) with k >= 2 and k < l
        for (int k = 2; k < N; k++) {
            for (int l = k + 1; l < N; l++) {
                freq[A[k] ^ A[l]]++;
            }
        }

        // STEP 2: Iterate j from 1 to N-3
        for (int j = 1; j <= N - 3; j++) {
            // Match (i, j) with existing (k, l) pairs
            for (int i = 0; i < j; i++) {
                int d = A[i] ^ A[j];
                if (freq.count(d)) {
                    c += freq[d];
                }
            }

            // Remove all (j+1, l) pairs because k must be > j
            for (int l = j + 2; l < N; l++) {
                int d = A[j + 1] ^ A[l];
                if (--freq[d] == 0) {
                    freq.erase(d);
                }
            }
        }

        // Multiply unordered quadruples by 24 to get ordered count
        cout << c * 24 << "\n";
    }
}
```

<img width="1183" height="700" alt="image" src="https://github.com/user-attachments/assets/f948f138-b888-4995-bc3a-0ecaa52e9217" />
<img width="955" height="580" alt="image" src="https://github.com/user-attachments/assets/e7ea91cc-d339-46c0-80ab-ab5928edb048" />
<img width="1149" height="459" alt="image" src="https://github.com/user-attachments/assets/4091e7ae-73ed-47af-908d-b9aa58ffbf2b" />


```
the optimal 1 code is not accepted as  Hashmap takes a little bit more time compared to array to store frequency

Here our intuition is correct then we got that the datastructure takes more time --> change the datastructure
```


## Optimal Code 2 : static array  : O(n^2)

```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

// Preallocated frequency array (faster than unordered_map)
// Index = XOR value, Value = how many (k, l) pairs give that XOR.
// 5,000,000 is chosen to be large enough for the max possible XOR in constraints.
static int freq[5000000 + 5];

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);

    int T; // number of test cases
    cin >> T;

    while (T--) {
        int N; // array size
        cin >> N;
        vector<int> A(N);
        for (int i = 0; i < N; i++) {
            cin >> A[i];
        }

        ll c = 0; // counts the number of unordered quadruples (i, j, k, l) that satisfy the condition

        /*
         --------------------------------------------
         STEP 1: Build freq[] for all possible (k, l) pairs
                 where k >= 2 and k < l.
         
         Why start from k = 2?
         - We will later match (i, j) where j < k.
           So at the beginning, we put all pairs starting at index 2 or later.
         --------------------------------------------
        */
        for (int k = 2; k < N; k++) {
            for (int l = k + 1; l < N; l++) {
                // Store how many (k, l) pairs give this XOR value
                freq[A[k] ^ A[l]]++;
            }
        }

        /*
         --------------------------------------------
         STEP 2: Iterate over possible j (second index of first pair)
                 from j = 1 to N - 3. (N is length  -> n-1 is last element (gives it to l) and n-2 is second last element(gives it to k) so j is upto n-3)
         
         For each j:
           - First, match all (i, j) pairs with available (k, l) pairs.
           - Then, remove all pairs starting at k = j+1 so they won't be used
             in future iterations.
         --------------------------------------------
        */
        for (int j = 1; j <= N - 3; j++) {
            // (A[i] ^ A[j]) must match XOR of some (k, l) in freq[]. i runs from 0 to j-1 so i < j < k < l.
            for (int i = 0; i < j; i++) {
                c += freq[A[i] ^ A[j]];
            }

            // Remove all (j+1, l) pairs from freq[] (as j = j + 1 => 2 in next iteration so all the xors which can use 2 will have to be removed) so that future (i, j') pairs don't accidentally use them.
            for (int l = j + 2; l < N; l++) {
                freq[A[j + 1] ^ A[l]]--;
            }
        }

        /*
         --------------------------------------------
         STEP 3: Clear freq[] for the next test case.

         We only clear entries that were actually used:
         - All (i, j) with i < j contribute to freq[] at some point.
         - This is O(N^2) but avoids clearing entire 5M array each time.
         --------------------------------------------
        */
        for (int i = 0; i < N; i++) {
            for (int j = i + 1; j < N; j++) {
                freq[A[i] ^ A[j]] = 0;
            }
        }

        /*
         --------------------------------------------
         STEP 4: Multiply by 24 to get ordered quadruples.
         
         Why 24?
         - The loops count only *unordered index positions* i < j < k < l
           that satisfy the XOR condition.
         - Each such set of 4 distinct indices can be arranged in 4! = 24 ways.
         --------------------------------------------
        */
        cout << c * 24 << "\n";
    }
}

```

 ## Run Code
 https://www.codechef.com/problems/XSQR
