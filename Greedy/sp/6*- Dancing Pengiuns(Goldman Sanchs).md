# Problem 
![image](https://github.com/user-attachments/assets/04c1a4f1-5619-4f35-ab01-5c242e96bd86)
![image](https://github.com/user-attachments/assets/78cc48d9-86e9-424d-a972-97b30e274da0)
![image](https://github.com/user-attachments/assets/4ed453c1-35cf-4ffa-828b-56ed77265044)
![image](https://github.com/user-attachments/assets/87833823-9cbb-4e71-ae89-8ae7a7bb9bb7)
![image](https://github.com/user-attachments/assets/d6872f06-c268-4e3a-b598-dbe24481fdf2)
![image](https://github.com/user-attachments/assets/2d2341a3-068e-484f-acf5-5d4d47e56190)

---
# Intuition
```
Males M = {p1m,p2m} 
      where p1m = {+ve values} :  indicates needs taller females than his 
            p2m = {-ve values} :  indicates needs shorter females than his

Males F = {p1f,p2f} 
      where p1f = {+ve values} : indicates needs taller males than her 
            p2f = {-ve values} : indicates needs shorter males than her
```
![image](https://github.com/user-attachments/assets/febd48cb-b9be-43b1-8953-0f959b63d085)

---

# code
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    ll n;
    cin >> n;

    // p1m = males who want a taller partner (positive)
    // p2m = males who want a shorter partner (negative)
    vector<ll> p1m, p2m;
    ll c = 0; // counter for valid pairs

    // Read male heights and classify by preference
    for (ll i = 1; i <= n; i++) {
        ll y;
        cin >> y;
        if (y < 0) {
            p2m.push_back(abs(y)); // wants shorter partner
        } else {
            p1m.push_back(y); // wants taller partner
        }
    }

    // p1f = females who want a taller partner (positive)
    // p2f = females who want a shorter partner (negative)
    vector<ll> p1f, p2f;

    // Read female heights and classify by preference
    for (ll i = 1; i <= n; i++) {
        ll y;
        cin >> y;
        if (y < 0) {
            p2f.push_back(abs(y)); // wants shorter partner
        } else {
            p1f.push_back(y); // wants taller partner
        }
    }

    // Sort all preference groups to enable two-pointer matching
    if (!p2m.empty()) sort(p2m.begin(), p2m.end());
    if (!p1m.empty()) sort(p1m.begin(), p1m.end());
    if (!p2f.empty()) sort(p2f.begin(), p2f.end());
    if (!p1f.empty()) sort(p1f.begin(), p1f.end());

    // Match males who want shorter partners (p2m) with females who want taller partners (p1f)
    ll i = 0, j = 0;
    while (i < p1f.size() && j < p2m.size()) {
        if (p2m[j] > p1f[i]) {
            c++; // valid pair: male is taller
            i++;
            j++;
        } else {
            j++; // try next male
        }
    }

    // Match females who want shorter partners (p2f) with males who want taller partners (p1m)
    i = 0;
    j = 0;
    while (i < p1m.size() && j < p2f.size()) {
        if (p2f[j] > p1m[i]) {
            c++; // valid pair: female is taller
            i++;
            j++;
        } else {
            j++; // try next female
        }
    }

    // Output total number of valid dance pairs
    cout << c;

    return 0;
}

```
