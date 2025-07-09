# Problem 
![image](https://github.com/user-attachments/assets/c73a5763-d4ae-4e67-9bc3-258fc17b5d03)
![image](https://github.com/user-attachments/assets/eb99ddeb-da16-489e-a35c-79b6c4b80bdb)


# 📘 Divisors Array (Easy Version)

This project solves the **Divisors Array** problem using efficient **prime factorization** with **SPF (Smallest Prime Factor)** and merges factorizations of numbers with the factorial of `M`.

---

## 🚀 Problem Summary

You're given:
- An array `A` of size `N`
- A number `M`

You must:
1. Construct a new array `B` where:
B[i] = A[i] * M!
2. For each `B[i]`, compute the number of **positive divisors**, denoted `F(B[i])`.
3. Print `F(B[i]) % (10^9 + 7)` for each index.

---

## 🧠 Mathematical Insight

If you know the **prime factorization** of a number:
x = p1^e1 × p2^e2 × ... × pk^ek
Then the number of divisors of `x` is:F(x) = (e1+1)(e2+1)...(ek+1)

To solve this efficiently:
- Precompute **SPF (Smallest Prime Factor)** up to `10^6`
- Build **prime factor map of M!** once
- For each element `A[i]`, get its prime factorization
- Merge with the M! prime factor map
- Compute the divisor count using the formula above

---

## ⏱️ Time Complexity

O(N * log Ai) + O(M log M) + O(MAXN * log log MAXN)

- SPF Preprocessing: `O(MAXN * log log MAXN)`
- Factorizing each number using SPF: `O(log Ai)`
- Merging factor maps: `O(#primes) ≈ 10–20 per number`
- Efficient for `N ≤ 1e5` and `M ≤ 100`

---

## 📦 Sample Input


- SPF Preprocessing: `O(MAXN * log log MAXN)`
- Factorizing each number using SPF: `O(log Ai)`
- Merging factor maps: `O(#primes) ≈ 10–20 per number`
- Efficient for `N ≤ 1e5` and `M ≤ 100`

---

## 📦 Sample Input

3 3 
1 2 3

### Explanation:

- M! = 3! = 6  
- B = [1×6, 2×6, 3×6] = [6, 12, 18]  
- Divisors:
  - F(6) = 4
  - F(12) = 6
  - F(18) = 6

### ✅ Sample Output:
4 6 6


---

## 🧰 Full C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const ll MAXN = 1000000;
const ll MOD = 1e9 + 7;

vector<ll> spf(MAXN + 1);  // Smallest Prime Factor

// Step 1: Precompute SPF using modified sieve
void computeSPF() {
    for (ll i = 2; i <= MAXN; i++) spf[i] = i;
    for (ll i = 2; i * i <= MAXN; i++) {
        if (spf[i] == i) {
            for (ll j = i * i; j <= MAXN; j += i) {
                if (spf[j] == j) spf[j] = i;
            }
        }
    }
}

// Step 2: Prime factorization using SPF
unordered_map<ll, ll> factorize(ll val) {
    unordered_map<ll, ll> factors;
    while (val != 1) {
        ll p = spf[val];
        factors[p]++;
        val /= p;
    }
    return factors;
}

int main() {
    ll n, m;
    cin >> n >> m;

    computeSPF();  // Step 1

    // Step 3: Compute prime factorization of M!
    unordered_map<ll, ll> mfact;
    for (ll i = 2; i <= m; i++) {
        unordered_map<ll, ll> f = factorize(i);
        for (auto &it : f) {
            mfact[it.first] += it.second;
        }
    }

    // Step 4: Process each A[i]
    for (ll i = 1; i <= n; i++) {
        ll a;
        cin >> a;

        // Get factorization of A[i]
        unordered_map<ll, ll> afact = factorize(a);

        // Merge with M! factorization
        for (auto &it : mfact) {
            afact[it.first] += it.second;
        }

        // Step 5: Compute number of divisors
        ll res = 1;
        for (auto &it : afact) {
            res = (res * (it.second + 1)) % MOD;
        }

        cout << res << " ";
    }

    cout << "\n";
    return 0;
}

