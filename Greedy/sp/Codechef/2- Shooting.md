# Problem 
![image](https://github.com/user-attachments/assets/8037076f-803a-4ab3-8587-4a8214c55eb7)

---
![image](https://github.com/user-attachments/assets/422d1eb6-0759-4017-878b-2b0ea8874bd6)

---

# Brute Force Intuition
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int T;cin >> T;
    while (T--) {
        int n, m;
        cin >> n >> m;
        // Indexing from 1 to m
        vector<int> b(m + 1);
        vector<int> a(m + 1, 0);       // aarsi presence
        vector<int> k(m + 1, 0);       // krypto presence
        vector<int> aarsi(m + 1, 0);   // aarsi cost
        vector<int> krypto(m + 1, 0);  // krypto cost

        // Input row (n == 1)
        for (int i = 1; i <= m; i++) {
            cin >> b[i];
            if (b[i] == 1) a[i] = 1;
            else if (b[i] == 2) k[i] = 1;
            else if (b[i] == 3) {
                a[i] = 1;k[i] = 1;
            }
        }

        // Compute aarsi cost to bring all to index `line`
        for (int line = 1; line <= m; line++) {
            int cost = 0;
            for (int i = 1; i <= m; i++) {
                if (a[i] == 1) {
                    cost += abs(line - i);
                }
            }
            aarsi[line] = cost;
        }

        // Compute krypto cost to bring all to index `line`
        for (int line = 1; line <= m; line++) {
            int cost = 0;
            for (int i = 1; i <= m; i++) {
                if (k[i] == 1) {
                    cost += abs(line - i);
                }
            }
            krypto[line] = cost;
        }

        // Output absolute difference for each line
        for (int i = 1; i <= m; i++) {
            cout << abs(aarsi[i] - krypto[i]) << " ";
        }
        cout << "\n";
    }
    return 0;
}
TC - O(M*M) 
```

# Intuition
![image](https://github.com/user-attachments/assets/6c0ea480-4346-4809-993b-0f0fa466d065)

![image](https://github.com/user-attachments/assets/cd248b03-1070-4e4e-b1a4-1aaa6e024415)

![image](https://github.com/user-attachments/assets/058a9ab5-905d-4d48-9385-aceb79e808ae)

sum of positions on right side[i] = total sum of [i] positions - sum of positions on left side[i]
# Code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int T;cin >> T;
    while (T--) {
        int n, m;
        cin >> n >> m;
        vector<int> b(m + 1); // Input row (1-based index)

        // Markers for Aarsi and Krypto presence
        vector<int> a(m + 1, 0);  // a[i] = 1 if Aarsi shot at i
        vector<int> k(m + 1, 0);  // k[i] = 1 if Krypto shot at i

        // To store total cost of bringing all shots to position i
        vector<long long> aarsi_cost(m + 1, 0);
        vector<long long> krypto_cost(m + 1, 0);

        // Step 1: Parse input and mark Aarsi and Krypto positions
        for (int i = 1; i <= m; i++) {
            cin >> b[i];

            if (b[i] == 1) {a[i] = 1; }  // Aarsi only
            else if (b[i] == 2) {k[i] = 1; }  // Krypto only
            else if (b[i] == 3) {
                a[i] = 1; // Both
                k[i] = 1;
            }
        }

        // Step 2: Pre-compute total Aarsi shots and sum of their positions
        long long total_a_count = 0, total_a_sum = 0;
        for (int i = 1; i <= m; i++) {
            if (a[i] == 1) {
                total_a_count++;
                total_a_sum += i;
            }
        }

        // Step 3: Compute Aarsi cost at each index using prefix sum trick
        long long a_count = 0, a_sum = 0;
        for (int i = 1; i <= m; i++) {
            if (a[i] == 1) {    // Update prefix if Aarsi shot at i
                a_count++;
                a_sum += i;
            }
            long long left = a_count * i - a_sum;   // Left cost = bringing all Aarsi before i to i
            long long right = (total_a_sum - a_sum) - i * (total_a_count - a_count); // Right cost = bringing all Aarsi after i to i
            aarsi_cost[i] = left + right;   // Total cost to bring all Aarsi to index i
        }

        // Step 4: Pre-compute total Krypto shots and sum of their positions
        long long total_k_count = 0, total_k_sum = 0;
        for (int i = 1; i <= m; i++) {
            if (k[i] == 1) {
                total_k_count++;
                total_k_sum += i;
            }
        }

        // Step 5: Compute Krypto cost at each index using prefix sum trick
        long long k_count = 0, k_sum = 0;
        for (int i = 1; i <= m; i++) {
            if (k[i] == 1) {   // Update prefix if Krypto shot at i
                k_count++;
                k_sum += i;
            }
            long long left = k_count * i - k_sum;  // Left cost = bringing all Krypto before i to i
            long long right = (total_k_sum - k_sum) - i * (total_k_count - k_count);  // Right cost = bringing all Krypto after i to i
            krypto_cost[i] = left + right;  // Total cost to bring all Krypto to index i
        }

        // Step 6: Output absolute difference of Aarsi and Krypto costs for each bullseye
        for (int i = 1; i <= m; i++) {
            cout << abs(aarsi_cost[i] - krypto_cost[i]) << " ";
        }
        cout << "\n";
    }
    return 0;
}
```
# ⏱ Time Complexity
```
Per test case:
  O(M) to scan and mark aarsi/krypto
  O(M) to compute aarsi cost
  O(M) to compute krypto cost
  So per test case: O(M)
  Total across T test cases ≤ 3×10⁵ → ✅ Fully fits the problem constraint
```
