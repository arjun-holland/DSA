# PROBLEM
<img width="955" height="645" alt="image" src="https://github.com/user-attachments/assets/291c208a-a9d4-41d3-9179-8c2f8bd1a1f0" />
<img width="961" height="408" alt="image" src="https://github.com/user-attachments/assets/670dc31d-ef0a-4d53-8860-e20e3481e067" />

# BRUTE FORCE INTUITION
<img width="758" height="390" alt="image" src="https://github.com/user-attachments/assets/4fffd5da-2239-4a00-a0b5-19273e78a15c" />
<img width="890" height="488" alt="image" src="https://github.com/user-attachments/assets/d99f6494-c3c2-4169-9ae9-01deec7b001a" />

| Why DFS?                         | Explanation                              |
| -------------------------------- | ---------------------------------------- |
| 🔁 Two choices per element       | `+k` or `-k`                             |
| 🌲 Forms a decision tree         | 2 branches per element                   |
| 📚 Need to try all combinations  | Hence DFS through the tree               |
| 🛑 Can prune invalid paths early | e.g., skip `arr[i] - k` if it's negative |

## CODE : Recurssion (Brute Force)  => Time: O(2^n)
```
class Solution {
public:
    int ans = INT_MAX;

    void dfs(int idx, vector<int>& arr, vector<int>& temp, int k, int n) {
        if (idx == n) {
            int mn = INT_MAX, mx = INT_MIN;
            for (int i = 0; i < n; i++) {
                mn = min(mn, temp[i]);
                mx = max(mx, temp[i]);
            }
            ans = min(ans, mx - mn);
            return;
        }

        // Option 1: Add k
        temp[idx] = arr[idx] + k;
        dfs(idx + 1, arr, temp, k, n);

        // Option 2: Subtract k, only if non-negative
        if (arr[idx] - k >= 0) {
            temp[idx] = arr[idx] - k;
            dfs(idx + 1, arr, temp, k, n);
        }
    }

    int getMinDiff(vector<int>& arr, int k) {
        int n = arr.size();
        vector<int> temp(n);
        dfs(0, arr, temp, k, n);
        return ans;
    }
};
```

## CODE : Recursion + Memoization (Top-Down DP)           
## => O(n * 1000 * 1000) = O(n * 10^6) :: This is okay for n = 10^2, but not feasible for n = 10^5.
```
class Solution {
public:
    int k;
    int n;
    vector<int> arr;

    // Memoization table: key = string "i|min|max"
    unordered_map<string, int> dp;

    int dfs(int i, int currMin, int currMax) {
        if (i == n) return currMax - currMin;

        // Memoization key
        string key = to_string(i) + "|" + to_string(currMin) + "|" + to_string(currMax);
        if (dp.count(key)) return dp[key];

        int ans = INT_MAX;

        // Option 1: Add k
        int newVal1 = arr[i] + k;
        ans = min(ans, dfs(i + 1, min(currMin, newVal1), max(currMax, newVal1)));

        // Option 2: Subtract k (only if non-negative)
        if (arr[i] - k >= 0) {
            int newVal2 = arr[i] - k;
            ans = min(ans, dfs(i + 1, min(currMin, newVal2), max(currMax, newVal2)));
        }

        return dp[key] = ans;
    }

    int getMinDiff(vector<int>& inputArr, int kVal) {
        k = kVal;
        arr = inputArr;
        n = arr.size();
        dp.clear();

        int ans = INT_MAX;

        // Start by trying both options for first element
        if (arr[0] - k >= 0)
            ans = min(ans, dfs(1, arr[0] - k, arr[0] - k));
        ans = min(ans, dfs(1, arr[0] + k, arr[0] + k));

        return ans;
    }
};

```

## OPTIMAL : Greedy + Sorting	O(n log n)	✅ Yes	Best choice for this problem as constraint as (10^5)
```


class Solution {
  public:
    int getMinDiff(vector<int>& arr, int k) {
        int n = arr.size();
        if (n == 1) return 0;

        sort(arr.begin(), arr.end());

        int ans = arr[n - 1] - arr[0];

        int smallest = arr[0] + k;
        int largest = arr[n - 1] - k;

        for (int i = 0; i < n - 1; i++) {
            int minVal = min(smallest, arr[i + 1] - k);
            if (minVal < 0) continue;
            
            int maxVal = max(largest, arr[i] + k);
            ans = min(ans, maxVal - minVal);
        }

        return ans;
    }
};

```


# RUN HERE : 
https://www.geeksforgeeks.org/problems/minimize-the-heights3351/1?_gl=1*1mql1a0*_up*MQ..*_gs*MQ..&gclid=Cj0KCQjw5onGBhDeARIsAFK6QJZpNlZk3xIPfgk3WLnr6RlWcZ-0ngSUngr7kISQeZ0tOwkMOu-wyckaAvy_EALw_wcB&gbraid=0AAAAAC9yBkBiJ1FNJ9VIXeD_y1b7uFGmN
