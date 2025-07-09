# Problem
![image](https://github.com/user-attachments/assets/6f151d42-1231-4186-a5ba-599ae44a0aa9)

---
![image](https://github.com/user-attachments/assets/961f3ab6-5606-4906-8521-5c41ca4bc868)

---
![image](https://github.com/user-attachments/assets/e29a700f-b8c7-4bc4-887c-e38344516793)

---

# Brute Force Way
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    // Read the size of the array
    ll n;cin >> n;
    // Read the array elements
    vector<ll> b(n);
    for (ll i = 0; i < n; i++) { cin >> b[i];}
    // Read the number of queries
    ll q;cin >> q;

    // For each target value
    while (q--) {  //O(q)
        ll target;cin >> target;
        ll operations = 0;
        // Calculate the total operations needed to make all elements equal to the target
        for (ll i = 0; i < n; i++) {   //O(n)
            operations += abs(b[i] - target);
        }
        cout << operations << endl;  // Output the result for this query
    }
    return 0;
}
TC - O(N*Q)
Takes constant size;

```

# Intuition
```
If (target > all numbers in the array) -> (target > max element of array)
      arr = {a,b,c,d} and tar = e; as tar > arr[i] where i = {0,1,2,4}
      -> ans = abs(a-tar)+abs(b-tar)+abs(c-tar)+abs(d-tar)   // tar i srepeated in 4 times(for every ele in array) i.e len of array
      -> ans = tar * (n) - sum ; n = length of array and sum = sum of elements in array
-> answer = target*n - sum; =>O(1)

If target < all numbers in the array ->(target < min element of the array)
-> answer = sum - target*n;

As we need suum of n elements do the prefix sum of given array to get the sum of n elemnts easily rather then loop

```
# code
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    ll n;cin >> n;
    vector<ll> b(n + 1);          // Array to store the elements
    vector<ll> prefix(n + 1, 0);  // Prefix sum array as array contains both > tar and < tar values and to group[ them we sort the array 
    ll total_sum = 0; b[0] = -1e18; b[n+1] = 1e18;

    // Input array elements and calculate prefix sums
    for (ll i = 1; i <= n; i++) {
        cin >> b[i];
        total_sum += b[i];
    }

    // Sort the array for binary search 
    sort(b.begin() + 1, b.begin() + n + 1);
    
    for(ll i = 1; i <= n; i++){
        prefix[i] = b[i] + prefix[i-1];  
    }

    // Handle queries
    ll q;cin >> q;
    while (q--) {
        ll target;cin >> target;

        // Binary search to find the last element <= target
        ll low = 1, high = n, g = 0;

        while (low <= high) {
            ll mid = (low + high) / 2;
            if (b[mid] <= target) {
                g = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        // Calculate left part and right part
        ll left_part = target * g - prefix[g];
        ll right_part = (total_sum - prefix[g]) - target * (n - g);

        // Output the total operations
        cout << left_part + right_part << endl;
    }

    return 0;
}
```
