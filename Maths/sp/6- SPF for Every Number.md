# 🔢 Smallest Prime Factor (SPF) for Every Number from 1 to 10⁶
## 📘 What Is the Smallest Prime Factor (SPF)?
For any integer n, the smallest prime factor is the smallest prime number that divides n.
```
      Example:
          SPF(2) = 2
          SPF(6) = 2 (since 2 is the smallest prime that divides 6)
          SPF(49) = 7 (since 7 × 7 = 49)
```
## 🚀 Why Precompute SPF?
Precomputing SPF is powerful for:
Fast prime factorization of multiple numbers
- Solving problems involving:
- Prime factor counts
- Coprimes
- GCD/LCM simplifications
Optimizing many number theory algorithms

## ⚙️ Time Complexity
O(n log log n) — similar to Sieve of Eratosthenes

## 🛠️ C++ Code to Precompute SPF for [1 ... 10⁶]
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

const ll MAXN = 1000000;
vector<ll> spf(MAXN + 1); // spf[i] will store the smallest prime factor of i

// Precomputes SPF for all numbers up to MAXN
void computeSPF() {
    // Initially assume each number is its own smallest prime factor
    for (ll i = 2; i <= MAXN; i++) {
        spf[i] = i;
    }

    // Sieve-like logic to fill SPF array
    for (ll i = 2; i * i <= MAXN; i++) {
        if (spf[i] == i) {         // i is prime : as the spf[i] = i then only we chnage all its multiples spf[j] = i
            for (ll j = i * i; j <= MAXN; j += i) {
                if (spf[j] == j) {
                    spf[j] = i;         // Set smallest prime factor
                }
            }
        }
    }
}

int main() {
    computeSPF(); // Fill the spf array

    // Print the smallest prime factors for numbers 2 to 20
    for (ll i = 2; i <= 20; i++) {
        cout << "Smallest prime factor of " << i << " is " << spf[i] << "\n";
    }
    return 0;
}
```
## 🧪 Sample Output
Smallest prime factor of 2 is 2
Smallest prime factor of 3 is 3
Smallest prime factor of 4 is 2
Smallest prime factor of 5 is 5
Smallest prime factor of 6 is 2
Smallest prime factor of 7 is 7
...
🧠 How It Works
Step	Purpose
spf[i] = i	Assume each number is initially prime
if (spf[i] == i)	Confirms i is actually a prime
for (j = i*i to MAXN)	Mark all multiples of i with i as smallest
if (spf[j] == j)	Only update the first (smallest) factor
