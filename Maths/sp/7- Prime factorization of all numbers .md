# 🔢 Prime Factorization of All Numbers in an Array Using SPF (Smallest Prime Factor)

This program performs efficient **prime factorization** of each number in an input array using a **precomputed SPF array** (Smallest Prime Factor),
built via a modified **Sieve of Eratosthenes**.

---

## 🚀 Features

- Computes the **smallest prime factor** for all numbers from `1` to `10⁶`
- Factorizes each element of the input array in **O(log n)** time
- Uses **unordered_map** to count prime powers (exponents)
- Efficient for processing **multiple factorizations** quickly

---

## 📘 What is SPF?
- SPF (Smallest Prime Factor) of a number `n` is the **smallest prime** that divides it.
- Once you have the SPF of all numbers, you can factor any number `x` by:
- Keep dividing x by spf[x] until x becomes 1

---

## 📦 Input & Output

### 📥 Input:
First line: n (number of elements)
Next n lines: one number per line

### 📤 Output:
For each number, print its prime factorization in the format: <prime> <exponent>


---

## 🛠️ Full C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

const ll MAXN = 1000000;
vector<ll> spf(MAXN + 1);           // spf[i] will store the smallest prime factor of i

// Step 1: Compute the SPF for all numbers using sieve
void computeSPF() {
    for (ll i = 2; i <= MAXN; i++) {
        spf[i] = i;
    }
    for (ll i = 2; i * i <= MAXN; i++) {
        if (spf[i] == i) {
            for (ll j = i * i; j <= MAXN; j += i) {
                if (spf[j] == j) {
                    spf[j] = i;
                }
            }
        }
    }
}

// Step 2: Use SPF to factorize a number in O(log n)
unordered_map<ll, ll> factorize(ll x) {
    unordered_map<ll, ll> factors;
    while (x != 1) {
        ll p = spf[x];
        factors[p]++;
        x /= p;
    }
    return factors;
}

int main() {
    ll n;cin >> n;
    computeSPF();  // Step 1: Precompute smallest prime factors

    ll arr[n + 1];
    for (ll i = 1; i <= n; i++) {
        cin >> arr[i];
        unordered_map<ll, ll> factors = factorize(arr[i]);
        
        cout << "Prime factors of " << arr[i] << ":\n";
        for (auto& it : factors) {
            cout << it.first << "^" << it.second << "\n";
        }
        cout << "-------------------\n";
    }
    return 0;
}
```

## 🧪 Example
Input:
3
18
29
60

Output:
Prime factors of 18:
2^1
3^2
-------------------
Prime factors of 29:
29^1
-------------------
Prime factors of 60:
2^2
3^1
5^1
-------------------
# 📈 Time & Space Complexity
- Task	Complexity
- SPF Precomputation	O(n log log n)
- Single Number Factorization	O(log n) per query
- Total Factorizations	O(n log n)
