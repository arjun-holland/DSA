# Problem
<img width="1382" height="792" alt="image" src="https://github.com/user-attachments/assets/b3f368fd-74ee-47f0-be87-85510cd3f5a6" />

<img width="1333" height="283" alt="image" src="https://github.com/user-attachments/assets/05622116-81a9-4e07-aaba-c77ca6f59d75" />

# Intuition
```
As we can attend only 'k' events and get the max profit by attending them
- Use Greedy : By greedly take the value which give the max but ans also not overlap with prev end time therre is a possibility that the local min can give the global maximum
   so cant use greedy here
- When Greedy fails then use the DP
```
<img width="1074" height="469" alt="image" src="https://github.com/user-attachments/assets/e8bfe5ad-9624-49dd-ab24-ae1a966d16a6" />


# code
```
class Solution {
public:
    int get(int i, int t, vector<vector<int>>& events, vector<vector<int>>& dp, int k) {
        if (i == events.size() || t == k) return 0;

        if (dp[i][t] != -1) return dp[i][t];

        // Option 1: Skip current event
        int not_take = get(i + 1, t, events, dp, k);

        // Option 2: Take current event
        // Find next event that starts after current ends
        int l = i + 1, r = events.size() - 1, next = events.size();
        while (l <= r) {             //o(n log n)
            int m = (l + r) / 2;
            if (events[m][0] > events[i][1]) {
                next = m;
                r = m - 1;
            } else {
                l = m + 1;
            }
        }

        int take = events[i][2] + get(next, t + 1, events, dp, k);

        return dp[i][t] = max(take, not_take);
    }

    int maxValue(vector<vector<int>>& events, int k) {
        int n = events.size();
        // Sort by start time
        sort(events.begin(), events.end());

        //k+1 : we can attent k meeting , 0,1,2,-------,k as 0 included the total countr is k+1
        vector<vector<int>> dp(n, vector<int>(k + 1, -1)); 

        return get(0, 0, events, dp, k);
    }
};
T.C : //n * k * o(n log n)
```

```
class Solution {
public:
    // Recursive function with memoization
    // i -> current event index
    // t -> number of events attended so far
    // events -> list of events
    // dp -> memoization table
    // k -> maximum events you can attend
    // n -> precomputed 'next' array storing next non-overlapping event index
    int get(int i, int t, vector<vector<int>>& events, vector<vector<int>>& dp, int k, vector<int>& n) {
        // Base case: all events processed or k events already attended
        if (i == events.size() || t == k) return 0;

        // Return already computed result
        if (dp[i][t] != -1) return dp[i][t];

        // Option 1: Skip current event
        int not_take = get(i + 1, t, events, dp, k, n);

        // Option 2: Take current event and move to the next non-overlapping one
        int next = n[i];         // index of next non-overlapping event
        int take = events[i][2] + get(next, t + 1, events, dp, k, n);

        // Memoize and return the best of both choices
        return dp[i][t] = max(take, not_take);
    }

    int maxValue(vector<vector<int>>& events, int k) {
        int n = events.size();

        // Sort events by start time (default lexicographical order: start, end, value)
        sort(events.begin(), events.end());

        // DP table: dp[i][t] = max value from index i with t events already chosen
        // k+1 columns to include t = 0 to k
        vector<vector<int>> dp(n, vector<int>(k + 1, -1)); 

        // Precompute 'next' array using binary search
        // next[i] = index of first event whose start time > events[i]'s end time
        vector<int> next(n);
        for (int i = 0; i < n; i++) {
            next[i] = upper_bound(events.begin(), events.end(), vector<int>{events[i][1] + 1, 0, 0}) - events.begin();
        }

        // Start recursion from event 0 with 0 events attended
        return get(0, 0, events, dp, k, next);
    }
};
T.C : O(n * K) + O(n log n)
```
