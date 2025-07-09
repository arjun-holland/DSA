## 📘 What Is a Divisor?

A **divisor** (or factor) of a number `n` is any number that divides `n` without leaving a remainder.

Example for `n = 12`:
Divisors of 12 = {1, 2, 3, 4, 6, 12}

## Code
```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

vector<ll> getDivisors(ll n) {
    vector<ll> divisors;

    for (ll i = 1; i * i <= n; ++i) {  // T.C : O(sqrt N)
        if (n % i == 0) { 
            divisors.push_back(i);
            if (i != n / i) {
                divisors.push_back(n / i);
            }
        }
    }
    sort(divisors.begin(), divisors.end()); // Ensure ascending order
    return divisors;
}

int main() {
    ll n = 12;
    vector<ll> divisors = getDivisors(n);
    for (ll d : divisors) {
        cout << d << " ";
    }
    cout << "\n";
    return 0;
}
 T.C : O(sqrt N)
```

