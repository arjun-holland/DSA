# PROBLEM
<img width="1006" height="472" alt="image" src="https://github.com/user-attachments/assets/475de355-97a9-4d19-9499-09683780a742" />

# INTUITION
## BRUTE FORCE

```
int max_sum_subarray_brute_force(vector<int>& arr, int N, int K) {
    int max_sum = 0;
    
    for (int i = 0; i < N; ++i) { 
        for (int j = i; j < N; ++j) {
            if (abs(arr[i] - arr[j]) == K) {
                int sub_sum = 0;
                for (int k = i; k <= j; ++k) {
                    sub_sum += arr[k];
                }
                if (sub_sum > max_sum) {
                    max_sum = sub_sum;
                }
            }
        }
    }   
    return max_sum;
}
```

## OPTIMAL O(n^2)
<img width="1092" height="182" alt="image" src="https://github.com/user-attachments/assets/997e2348-abb4-4d18-b225-b9590f5ada49" />
<img width="1009" height="417" alt="image" src="https://github.com/user-attachments/assets/62ed55c2-0fc5-470d-bb7a-e07dafad0643" />
<img width="895" height="386" alt="image" src="https://github.com/user-attachments/assets/90792a21-06ac-4f41-8bb7-e74c3cba60a2" />

```
int max_sum_subarray_optimized(vector<int>& arr, int N, int K) {
    unordered_map<int, vector<int>> mp;  // Stores positions of each value
    vector<int> prefix_sum(N + 1, 0);    // Prefix sum to get subarray sum in O(1)

    // Compute prefix sums
    for (int i = 0; i < N; ++i) {
        prefix_sum[i + 1] = prefix_sum[i] + arr[i];
        mp[arr[i]].push_back(i);  // Map value to its positions
    }

    int max_sum = 0;

    // For each possible subarray ending at index 'j'
    for (int j = 0; j < N; ++j) {
        int end_val = arr[j];

        // Look for possible start values: end_val - K and end_val + K
        vector<int> candidates;

        if (mp.count(end_val - K)) {
            candidates.insert(candidates.end(), mp[end_val - K].begin(), mp[end_val - K].end());
        }
        if (mp.count(end_val + K)) {
            candidates.insert(candidates.end(), mp[end_val + K].begin(), mp[end_val + K].end());
        }

        for (int i : candidates) {
            if (i <= j) {
                int sub_sum = prefix_sum[j + 1] - prefix_sum[i];
                max_sum = max(max_sum, sub_sum);
            }
        }
    }

    return max_sum;
}

int main() {
    vector<int> arr = {1, 5, -5, 8, 8, 8, 10, 15};
    int K = 5;
    int N = arr.size();

    int result = max_sum_subarray_optimized(arr, N, K);
    cout << (result > 0 ? result : 0) << endl;

    return 0;
}
```

## Highly Optimal O(n)
<img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/dfea8aea-4240-4b12-aff0-bce61a8268d7" />

```
#include <bits/stdc++.h>
using namespace std;

int solve(vector<int> a,int k){
    int n = a.size();
    vector<int> prf(n+1, 0);
    for(int i=0; i<n; i++){
        prf[i+1] = prf[i] + a[i];   //store the sum form 0 to i-1 for i'th index
    }

    unordered_map<int,int> minPref; // value -> min prefix sum before first appearance
    int ans = INT_MIN;

    for(int i=0; i<n; i++){
        int e = a[i];

        // Check for start = e + k → arr[start] - arr[end] = K
        if(minPref.find(e - k) != minPref.end()){
            ans = max(ans, prf[i+1] - minPref[e - k]);
        }

        // Only update if not seen yet, to keep the *earliest (min)* prefix sum
        if(minPref.find(e) == minPref.end()){
            minPref[e] = prf[i];
        } else {
            minPref[e] = min(minPref[e], prf[i]);
        }

    }
    return ans;
}


int main() {
    vector<int> arr = {1, 5, -5, 8, 8, 8, 10, 15};
    int K = 0;

    int result = solve(arr, K);
    cout << (result > 0 ? result : 0) << endl;

    return 0;
}

```
