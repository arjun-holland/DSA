# Problem
<img width="449" height="679" alt="image" src="https://github.com/user-attachments/assets/e8ce5c25-3b55-4f72-935d-b5ca547ed299" />
<img width="453" height="745" alt="image" src="https://github.com/user-attachments/assets/ee8a16d1-4965-4a02-bc7c-c08781a0a814" />

# Intuition
The question also says we need to find the length of the subsequences whose ele is same which can be also asked as,
<img width="1163" height="354" alt="image" src="https://github.com/user-attachments/assets/c6645ec3-92e6-48ee-8abf-b1cbc74d5c63" />
Understanding.....
<img width="1600" height="865" alt="image" src="https://github.com/user-attachments/assets/ce4840c8-4fb3-44bd-bdca-f202976f9519" />

```
As range is present we can use the Difference Array technique
    Now the point is constrinats
      |  |
      |  |___ <= 10^5 then use array
      |
      |________ <= 10^9 then use the Map
 
```
Example:

```
n = 3
a = [4, 6, 8]
k = 2

So:
4 → can become [2, 6]
6 → can become [4, 8]
8 → can become [6, 10]

Number line:
     2   3   4   5   6   7   8   9  10
     |   |   |   |   |   |   |   |   |
 4: [________________]
 6:          [_______________]
 8:                  [_______________]

Overlaps:
- 6: covered by all 3 → ✅ as 6 is present in [2,6], [4,8], [6,10]
- 4, 5, 6: covered by 2  
- 7, 8: covered by 2

So:
Maximum overlap = 3
That happens at 6, because all 3 ranges touch it.

```
<img width="1176" height="664" alt="image" src="https://github.com/user-attachments/assets/9b4c9a24-71ab-41d2-b6d2-ffefb127c5c1" />

# Code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; 
    cin >> n;
    
    vector<int> a(n);
    for(int i = 0; i < n; i++) cin >> a[i];
    
    int k;
    cin >> k;
    
    // Use map to simulate prefix sum updates over sparse range
    map<int, int> freq;

    for(int i = 0; i < n; i++) {
        int l = a[i] - k;
        int r = a[i] + k;

        freq[l] += 1;
        freq[r + 1] -= 1;
    }

    int curr = 0, ans = 0;
    for (auto& [point, delta] : freq) {
        curr += delta;
        ans = max(ans, curr);
    }

    cout << ans << endl;
}
```
