
<img width="978" height="672" alt="image" src="https://github.com/user-attachments/assets/b130659e-3012-4a48-bd28-e79557bbdb72" />

<img width="862" height="92" alt="image" src="https://github.com/user-attachments/assets/19fe1cac-a70f-44b3-9c59-f3e2f570ed7c" />

<img width="826" height="482" alt="image" src="https://github.com/user-attachments/assets/c123c7a3-6492-4811-bb4d-15c6da916002" />


# CODE
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

// --------------------- Utility Functions ---------------------

// Insert an element
void insertElement(multiset<ll> &s, ll x) {
    s.insert(x);
}

// Remove an element (if exists)
void removeElement(multiset<ll> &s, ll x) {
    auto it = s.find(x);
    if (it != s.end()) s.erase(it);
}

// Get the biggest element
ll biggest(multiset<ll> &s) {
    if (s.empty()) return -1; // no elements
    return *s.rbegin();       // last element
}

// Get the smallest element
ll smallest(multiset<ll> &s) {
    if (s.empty()) return -1;
    return *s.begin();        // first element
}

// Get the value just bigger than x
ll bigger(multiset<ll> &s, ll x) {
    if (s.empty()) return -2; // set empty
    auto it = s.upper_bound(x); 
    if (it == s.end()) return -1; // no bigger element
    return *it;
}

// Get the value just smaller than x
ll smaller(multiset<ll> &s, ll x) {
    if (s.empty()) return -2; // set empty

    auto it = s.lower_bound(x); // first >= x

    if (it == s.begin()) return -1; // no smaller element

    --it; 
    return *it;
}

// Check if element exists
bool findElement(multiset<ll> &s, ll x) {
    return s.find(x) != s.end();
}

// --------------------- Main ---------------------

int main() {
    multiset<ll> s;

    // Insert elements
    insertElement(s, 2);
    insertElement(s, 4);
    insertElement(s, 6);
    insertElement(s, 8);

    cout << "Smallest: " << smallest(s) << "\n"; // 2
    cout << "Biggest: " << biggest(s) << "\n";   // 8

    cout << "Bigger than 4: " << bigger(s, 4) << "\n";   // 6
    cout << "Smaller than 4: " << smaller(s, 4) << "\n"; // 2

    cout << "Find 6? " << (findElement(s, 6) ? "Yes" : "No") << "\n"; // Yes

    removeElement(s, 6);
    cout << "Find 6 after removal? " 
         << (findElement(s, 6) ? "Yes" : "No") << "\n"; // No

    return 0;
}
```
