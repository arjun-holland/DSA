# Problem
<img width="944" height="690" alt="image" src="https://github.com/user-attachments/assets/75301d78-080e-423b-9dd8-3ece5853c37d" />
<img width="917" height="158" alt="image" src="https://github.com/user-attachments/assets/1dd2ce12-0b3f-4440-bcf3-98f7589be1ee" />

# Brute Force Code 
```
class Solution {
  public:
    int powerfulInteger(vector<vector<int>>& intervals, int k) {
        unordered_map<int,int> mp;
        for(auto i : intervals){
            int s = i[0];
            int e = i[1];
            for(int j=s; j<=e; j++){    //inworest case s = 1 and e = 10^9 
                mp[j]++;
            }
        }
        int ans = -1;
        for(auto [e,c] : mp){
            if(c >= k)ans = max(ans,e);
        }
        return ans;
    }
};
T.c : O(n^2) 
```


# Intuition

<img width="1166" height="142" alt="image" src="https://github.com/user-attachments/assets/cc771ef1-4f17-4fee-a473-698f3bf5c698" />

```
class Solution {
public:
    int powerfulInteger(vector<vector<int>>& intervals, int k) {
        const int MAX = 1e5 + 10;      // safely beyond upper bound : max constraint value 
        vector<int> freq(MAX, 0);

        // Build difference array
        for (auto& i : intervals) {
            freq[i[0]] += 1;
            if (i[1] + 1 < MAX) {
                freq[i[1] + 1] -= 1;
            }
        }

        // Convert to prefix sum to get actual counts
        int active = 0;
        int ans = -1;

        for (int i = 0; i < MAX; i++) {
            active += freq[i];
            if (active >= k) {
                ans = i;  // update with latest powerful integer
            }
        }

        return ans;
    }
};
```

```
BUt in the quesstion we have 10^9, As we can't create an array of size 10^9 , we can use the other data-structure like map<> with the same logic
```


<img width="1115" height="381" alt="image" src="https://github.com/user-attachments/assets/70acb13f-9ab0-4b86-90bd-5de0256132b6" />


# Code
```
class Solution {
public:
    int powerfulInteger(vector<vector<int>>& intervals, int k) {
        map<int, int> events;

        // Mark events
        for (auto& i : intervals) {
            events[i[0]] += 1;
            events[i[1] + 1] -= 1;  // use end+1 to make interval inclusive
        }

        int active = 0;
        int ans = -1;
        int prev = -1;

        for (auto it = events.begin(); it != events.end(); ++it) {
            int curr = it->first;
            if (prev != -1 && active >= k) {      // [prev, curr - 1] is a continuous range with the same active count
                ans = max(ans, curr-1);         // last integer in this valid range
            } 
            active += it->second;
            prev = curr;
        }

        return ans;
    }
};
```

# Submission Link
https://www.geeksforgeeks.org/problems/powerfull-integer--170647/1
