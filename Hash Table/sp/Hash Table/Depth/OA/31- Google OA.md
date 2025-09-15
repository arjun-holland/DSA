# Problem
<img width="749" height="332" alt="image" src="https://github.com/user-attachments/assets/7582674c-007b-4a19-901c-f155bf4425a2" /> 

## Intuition
` Understanding :-> Find the subarray with maximum sum such that the first and last elements are the same.  ` 

## Brute Force => TC: O(n^2) , SC : O(constant)
```
-> n 
-> b[n+1] ....... 

answer = INT_MIN. 
for(i=1; i<=n; i++){
    sum = 0 
    for(j=i; j<=n; j++){
        sum = sum + b[j] 
        if(b[i]==b[j]){
            answer = max(answer,sum)
        }
    }
}
print(answer)
```

## Brute Force 2 => => TC: O(n^2) , SC : O(n)
```
#include <bits/stdc++.h>
using namespace std;

int solve(vector<int> a){
    int n = a.size();
    unordered_map<int,vector<int>> mp;  // map : < element , indices of element >
    
    vector<int> prf(n);
    prf[0] = a[0];
    for(int i=1; i<n; i++){
        prf[i] = prf[i-1] + a[i];
    }
    
    int sum = 0;
    for(int i=0; i<n; i++){
        int e = a[i];
        if(mp.find(e) != mp.end()){
            int tot_sum = prf[i];
            for(int req_id : mp[e]){
                int req_sum = (req_id > 0) ? prf[req_id-1] : 0;
                sum = max(sum , (tot_sum - req_sum));
            }
            mp[e].push_back(i);
        }else{
            mp[e].push_back(i);
        }
    }
    
    return sum;
}

int main() {
	vector<int> a = {1, 8, 10, 8, -5, 8};
	//find the max sum of subarray which has same ele in first and last
	cout << solve(a);
	return 0;
}
```

## Optimal 1
<img width="738" height="397" alt="image" src="https://github.com/user-attachments/assets/6b451240-6eb7-48e5-a0ef-684f35803eb0" />
<img width="724" height="416" alt="image" src="https://github.com/user-attachments/assets/bf7852d9-521f-49a6-9fd9-a566019e6e0b" />
<img width="402" height="208" alt="image" src="https://github.com/user-attachments/assets/d82b6443-4112-4cf1-94d7-651f1756b734" />

<img width="778" height="498" alt="image" src="https://github.com/user-attachments/assets/889cb888-050f-432a-a6b1-e5671b1ebe70" />

```
Efficient :-> Trick for subarray problems.-> always consider the subarray [i……….j] and try to analyze it 
Let's declare a function p(i) = means the sum of the first i numbers. 
Sum of subarray [i…..j] = p[j] - p[i-1] -> required sum for each subarray considered = p[j]-p[i-1]
If you want to find the maximum sum subarray which ends at index j. What will you do ?
For a fixed index “j” ; p[j] will be constant ; i is variable. 
So maximum sum subarray ending at index j = p[j] - p[i-1]

-> p[i-1] should be as small as possible to get the max sum as possible.
Hence you can do it hashing

-> Map < Value ; Prefix-Sum excluding that value at index i(minimum possible.)
If you are able to find this answer for any index j then you do it for all j from 1 to N and your question is solved. And take max.
```

```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    ll n; 
    cin >> n;

    ll answer = -1e18;      // final maximum sum (initialize very small)
    ll sum = 0;             // prefix sum till current index
    unordered_map<ll,ll> kk; // stores: element -> minimum prefix sum before it appeared

    for (ll i = 1; i <= n; i++) {
        ll yy; 
        cin >> yy;          // current element

        // Case 1: subarray of length 1 (just the element itself)
        answer = max(answer, yy);

        // Case 2: if this element appeared before
        if (kk.find(yy) != kk.end()) {
            // Compute subarray sum from some earlier occurrence of yy to here:
            // Formula: (prefix sum till now) - (smallest prefix before that occurrence)
            ll candidate = sum + yy - kk[yy];

            // Update maximum answer
            answer = max(answer, candidate);

            // Maintain the minimum prefix sum seen before this element
            kk[yy] = min(kk[yy], sum);
        } 
        // First time we see this element -> store prefix before it
        else {
            kk[yy] = sum;
        }

        // Update running prefix sum
        sum += yy;
    }

    cout << answer << endl;
    return 0;
}
```

## Optimal 2
```
#include <bits/stdc++.h>
using namespace std;

int solve(vector<int> a){
    int n = a.size();
    vector<int> prf(n+1, 0); // prf[0] = 0
    for(int i=0; i<n; i++){
        prf[i+1] = prf[i] + a[i];
    }

    unordered_map<int,int> minPref; // element -> min prefix sum before it appeared
    int ans = INT_MIN;

    for(int i=0; i<n; i++){
        int e = a[i];
        if(minPref.find(e) != minPref.end()){
            // candidate subarray sum = current prefix - best (smallest) prefix before
            ans = max(ans, prf[i+1] - minPref[e]);
        }
        // update min prefix for this element
        minPref[e] = min(minPref[e], prf[i]);
        if(minPref.find(e) == minPref.end()) minPref[e] = prf[i];
    }
    return ans;
}

int main(){
    vector<int> a = {1, 8, 10, 8, -5, 8};
    cout << solve(a) << endl; // 29
    return 0;
}

```
