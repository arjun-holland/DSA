# PROBLEM
<img width="1101" height="852" alt="image" src="https://github.com/user-attachments/assets/0fd562d7-4907-4db4-8720-50b51c90bb6f" />
<img width="1104" height="479" alt="image" src="https://github.com/user-attachments/assets/6c69c9c7-677e-40ac-9c29-49274cf2b595" />

# INTUITIOON
```
We observe that Alice wins only when the total number of flowers x+y is odd.
This happens in two cases: x odd & y even, or x even & y odd.
We count odds and evens in both ranges [1,n] and [1,m],
then compute the winning pairs as ⌈n/2⌉⋅⌊m/2⌋+⌊n/2⌋⋅⌈m/2⌉.
```

# CODE
```
typedef long long ll;

class Solution {
public:
    long long flowerGame(int n, int m) {
        ll n_e = n/2;
        ll n_o = n - n_e;

        ll m_e = m/2;
        ll m_o = m - m_e;

        return (n_e * m_o) + (n_o * m_e);   //e + o => o

    }
};
```
