# 📘 What It Does:
Efficiently generates all prime numbers between a given range [L, R] using a two-step method:
- Generate all primes from 1 to R using the Sieve of Eratosthenes
- Use binary search (lower_bound) to extract only the primes ≥ L
![image](https://github.com/user-attachments/assets/29db59f3-a873-43cd-a430-afc51b1bb2e6)

# Example
Input: L = 1, R = 100
Output:
2 3 5 7 11 13 17 19 23 29 31 ...

# 👨‍💻 C++ Code: Generate Primes in a Range
```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;
#define all(v) v.begin(), v.end()

// Basic sieve up to n
vector<ll> sieve(ll n) {
    vector<bool> prime(n + 1, true);
    prime[0] = prime[1] = false;
    for (ll p = 2; p * p <= n; p++) {
        if (prime[p]) {
            for (ll i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    vector<ll> primes;
    for (ll i = 0; i <= n; i++) {
        if (prime[i]) primes.push_back(i);
    }
    return primes;
}

// Extract only primes within [start, end]
vector<ll> sieveRange(ll start, ll end) {
    vector<ll> primes = sieve(end);
    auto it = lower_bound(all(primes), start);
    return vector<ll>(it, primes.end());
}

int main() {
    ll l = 1, r = 100;
    vector<ll> primeFlags(1000070, 0);

    // Get primes in range [l, r]
    vector<ll> ans = sieveRange(l, r);

    // Print primes and optionally flag them
    for (ll p : ans) {
        primeFlags[p] = 1;
        cout << p << "\n";
    }
    return 0;
}

```
# Sieve()
```
// Function to generate all prime numbers from 1 to n
vector<ll> sieve(ll n) {
    // Create a boolean array "prime[0..n]" and initialize all entries as true.
    // A value in prime[i] will be false if i is not a prime, true otherwise.
    vector<bool> prime(n + 1, true);

    // 0 and 1 are not prime numbers
    prime[0] = false;
    prime[1] = false;

    // Loop from 2 to sqrt(n)
    for (ll p = 2; p * p <= n; p++) {   
        if (prime[p]) {           // If prime[p] is still true, then it is a prime
            // Mark all multiples of p as not prime (i.e., false)
            // Start marking from p*p because smaller multiples would already be marked by smaller primes
            for (ll i = p * p; i <= n; i += p) {
                prime[i] = false;
            }
        }
    }

    // Collect all prime numbers into a vector to return
    vector<ll> primes;
    for (ll i = 0; i <= n; i++) {
        if (prime[i]) {
            primes.push_back(i);  // i is a prime number
        }
    }
    return primes;
}

```

| Feature            | Description                     |
| ------------------ | ------------------------------- |
| `sieve(n)`         | Classic Sieve of Eratosthenes   |
| `sieveRange(l, r)` | Efficient prime range filtering |
| `lower_bound`      | Fast access to the range start  |
| `O(n log log n)`   | Overall performance             |
| `primeFlags[i]`    | Array to flag if `i` is prime   |
