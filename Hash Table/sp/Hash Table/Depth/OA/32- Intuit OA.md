# PROBLEM
<img width="689" height="912" alt="image" src="https://github.com/user-attachments/assets/a0529c85-b64d-4c8e-90f6-ad9933fc3a27" />
<img width="1222" height="487" alt="image" src="https://github.com/user-attachments/assets/cb6ed0be-bc01-499f-9b86-1e7d305d757e" />


# INTUITION
## BRUTE FORCE
```
#include <bits/stdc++.h>
using namespace std;

int bruteForce(vector<int>& nums, int k) {
    set<pair<int,int>> st; // to store distinct pairs
    
    int n = nums.size();
    
    // check all possible pairs
    for (int i = 0; i < n; i++) {
        for (int j = i+1; j < n; j++) {
            if (abs(nums[i] - nums[j]) == k) {
                // store smaller first to avoid (a,b) and (b,a) duplication
                st.insert({min(nums[i], nums[j]), max(nums[i], nums[j])});
            }
        }
    }
    
    return st.size();
}

int main() {
    vector<int> nums = {1, 1, 1, 2};
    int k = 1;
    cout << bruteForce(nums, k) << endl; // Output: 1
    return 0;
}

```


## OPTIMAL

```
Approach:-> 

for a pair to be counted as an answer , both the elements ( x and x+k ) , need to be in the array.
So we simply create a map and store the frequency of each element in the map.
Now we traverse the map and for each element 'x' , we check if 'x+k' exists in the map . If it does , then it means a unique pair can be formed and hence, we increment the answer.

EDGE CASE :
The only edge case is the situation where k=0. If k=0 , instead of finding 'x+k' , we check if the frequency of 'x'>1. If it is , then we increment the answer .
Else , we don't increment the answer , as the frequency of x=1 and hence it can't form a pair with itself.
(only incrementing by one because in this case two the repeated pair say (4,4) needs to be counted only once it only needs to be counted once only)

```
<img width="1179" height="237" alt="image" src="https://github.com/user-attachments/assets/27a3dbda-4574-4060-b679-610c04a6012a" />


<img width="1119" height="141" alt="image" src="https://github.com/user-attachments/assets/f72bc26e-19d7-4cac-abe0-6452fd977bf6" />


```
#include <bits/stdc++.h>
using namespace std;

int solve(vector<int>& nums, int k) {
    unordered_map<int,int> freq;
    
    // Count frequency of each number
    for (int num : nums) {
        freq[num]++;
    }
    
    int ans = 0;
    
    for (auto &x : freq) {
        // Case 1: k == 0 -> look for duplicates
        if (k == 0) {
            // If a number appears more than once, (a,a) is a valid pair
            if (x.second > 1) ans++;
        }
        // Case 2: k > 0 -> look for a + k = b
        else {
            if (freq.find(x.first + k) != freq.end()) {
                // We found a distinct valid pair (x.first, x.first + k)
                ans++;
            }
        }
    }
    
    return ans;
}

int main() {
    vector<int> a = {1, 1, 1, 2};
    int k = 1;
    cout << solve(a, k) << endl; // Output: 1
    return 0;
}
```
