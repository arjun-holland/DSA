# 🔍 Prime Factorization of a Number

## 📘 What Is Prime Factorization?

Every number greater than 1 can be **uniquely** represented as a product of **prime numbers raised to some power**.

### General Form:
y = p1^e1 * p2^e2 * p3^e3 * ...


Where:
- `p1, p2, ..., pk` are **prime numbers**
- `e1, e2, ..., ek` are **their powers**
- This is called the **Prime Factorization** of `y`

---

## 🧠 Why Is This Useful?

- To count **number of divisors**
- To find **GCD/LCM** of numbers
- In problems involving:
  - Totient function
  - Modular arithmetic
  - Multiplicative functions
  - Prime queries

---

## 🛠️ C++ Code to Get Prime Factors (With Frequency)

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

// Returns a map of prime factors and their exponents
unordered_map<ll, ll> primeFactors(ll n) {
    unordered_map<ll, ll> factors;

    // Handle 2 separately (even prime)
    while (n % 2 == 0) {
        factors[2]++;
        n /= 2;
    }

    // Handle odd primes
    for (ll i = 3; i * i <= n; i += 2) {
        while (n % i == 0) {
            factors[i]++;
            n /= i;
        }
    }

    // If n is a prime > 2
    if (n > 2) {
        factors[n]++;
    }

    return factors;
}

int main() {
    ll n = 18;
    unordered_map<ll, ll> pf = primeFactors(n);

    cout << "Prime Factorization of " << n << ":\n";
    for (auto &p : pf) {
        cout << p.first << "^" << p.second << "\n";
    }

    return 0;
}
```
# ✅ Summary
| After loop | Meaning                         | What to do           |
| ---------- | ------------------------------- | -------------------- |
| `n == 1`   | All factors handled             | Do nothing           |
| `n == 2`   | Already handled earlier         | Do nothing           |
| `n > 2`    | It's a **prime not caught** yet | Add `factors[n]++` ✅ |


# 🧪 Example
For n = 18:
Output:
2^1
3^2
That means:
18 = 2^1 * 3^2

# 🧠 Number of Divisors From Prime Factorization
If:

n = p1^e1 * p2^e2 * ... * pk^ek
Then:

Total number of divisors = (e1 + 1)(e2 + 1)...(ek + 1)
Example: 18 = 2^1 * 3^2 → (1+1)(2+1) = 2 × 3 = 6 divisors

# 🧮 Time Complexity
O(√n) — checks all primes up to √n

Optimized for small to mid-range inputs
