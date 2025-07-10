# Problem
![image](https://github.com/user-attachments/assets/b078adf8-855f-4b29-b5ec-611e3fd0882a)

---
## Example
![image](https://github.com/user-attachments/assets/47328f97-aef2-442f-81e7-3dfcf7c7042b)

---
## Intuition
```
 
when you are at index “j” trying to calculate the number of valid subarrays ending at index “j”;
only possible subarrays are -> [j1+1….j],[j1+2……j],..........[j-2….j] -> j1 = index of previous greater element for "j"
and all {j1+1 , j1+2.....j-2} have the "j" as next greater elment
       
```

## Code : Using Stack (NOT OPTMIZED)
```
#include <bits/stdc++.h>
using namespace std;

// Function to solve and count valid subarrays (offer periods)
void solve(int n, vector<int>& a) {

    // Step 1: Compute Previous Greater Index (PGI)
    vector<int> pgi(n, -1);    // For each index i, store the index of the previous greater element
    stack<int> st;

    for (int i = 0; i < n; i++) {
        // Maintain a decreasing stack to find the previous greater
        while (!st.empty() && a[st.top()] < a[i]) {   //top os stack < cur ele
            st.pop();
        }
        if (!st.empty()) {
            pgi[i] = st.top();        // Top of the stack is the previous greater index
        }
        st.push(i); // Push current index to stack
    }

    // Clear the stack for next use
    while (!st.empty()) {
        st.pop();
    }

    // Step 2: Compute Next Greater Index (NGI)
    vector<int> ngi(n, n); // For each index i, store the index of the next greater element
                           // Default is n (no greater to the right)
    for (int i = n - 1; i >= 0; i--) {
        // Maintain a decreasing stack to find the next greater
        while (!st.empty() && a[st.top()] < a[i]) {
            st.pop();
        }
        if (!st.empty()) {
            ngi[i] = st.top(); // Top of the stack is the next greater index
        }
        st.push(i); // Push current index to stack
    }

    // Step 3: Count Valid Offer Periods
    int ans = 0;

    // For each index `i` starting from 2 (since we need at least two elements before i)
    for (int i = 2; i < n; i++) {   // the offer period is atleswt 3 days
        int ji = pgi[i];            // Index of the previous greater than a[i], i.e., a[ji] > a[i]

        // Now check all positions j between (ji+1) to (i-2) arew valid periods if 
        // We're looking for an index j such that:
        // - j is between the previous greater of i and i-2
        // - The next greater index of j is exactly i
        for (int j = ji + 1; j <= i - 2; j++) {
            if (ngi[j] == i) {
                ans++; // Valid (j, i) pair found
            }
        }
    }

    // Output the final count
    cout << "Total No. of Offer Periods: " << ans << endl;
}


int main() {
	int n; cin>>n;
	
	vector<int> v(n);
	for(int &e : v)cin>>e;
	
	solve(n,v);
  return 0;
}



```
