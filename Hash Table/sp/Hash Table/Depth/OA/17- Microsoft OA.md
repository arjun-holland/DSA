# Problem
<img width="679" height="196" alt="image" src="https://github.com/user-attachments/assets/f369fe1b-739b-44b3-9a1f-71f0a00673a4" />

# Intuition
## Brute Force : O(n^2)
```
--> n
--> b[n+1]

--> x, y
--> answer = INT_MAX.
for(int i=1; i<=n; i++){
    j = i 
    sum = 0
    c = 0 
    while(j >= 1 && c < x){
        sum = sum + b[j]
        c++
        j = j - y 
    }
    if(c==x){
        answer = min(answer,sum)
    }
}
print(sum)
```
## Optimal : with Hashing + prefix array : O(n)
<img width="626" height="650" alt="image" src="https://github.com/user-attachments/assets/b26a9aa1-17a5-452c-9ec1-fe8ba71fff4b" />
<img width="962" height="398" alt="image" src="https://github.com/user-attachments/assets/31a1875c-42b0-4b7b-844e-d54527df7abe" />

<img width="1600" height="725" alt="image" src="https://github.com/user-attachments/assets/1629766f-bd7c-4e12-8c10-9ea63af682f3" />

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main() {
    ll n;
    cin >> n;

    vector<ll> b(n + 1); // 1-indexed array
    for (ll i = 1; i <= n; i++) {
        cin >> b[i];
    }

    ll x, y;
    cin >> x >> y;

    // prefix[i] = sum of elements b[i], b[i-y], b[i-2y], ...
    vector<ll> prefix(n + 1, 0);
    for (ll i = 1; i <= n; i++) {
        if (i - y >= 1)
            prefix[i] = b[i] + prefix[i - y];
        else
            prefix[i] = b[i];
    }

    ll answer = LLONG_MAX;

    // Try taking x elements ending at position i
    for (ll i = 1; i <= n; i++) {
        ll startIndex = i - (x - 1) * y; // first element's index : total x , we are taking ele at i'th index already so we need only (x-1) elements
        if (startIndex >= 1) {
            ll sumX = prefix[i];
            if (startIndex - y >= 1)   // Remove elements before startIndex
                sumX -= prefix[startIndex - y];
            answer = min(answer, sumX);
            cout << "Sum ending at " << i << " = " << sumX << "\n";
        }
    }

    cout << "Minimum sum = " << answer << "\n";
    return 0;
}
```
## When we have exactly 2*x elements : its possible to take the exactly x elements 
<img width="725" height="652" alt="image" src="https://github.com/user-attachments/assets/317ee7de-03ac-41cc-b1ac-40cf095dae5c" />


# Run Code :
https://ideone.com/iPZzmR
