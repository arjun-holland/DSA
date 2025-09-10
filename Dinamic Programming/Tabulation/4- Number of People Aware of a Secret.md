# PROBLEM
<img width="1054" height="297" alt="image" src="https://github.com/user-attachments/assets/67102694-0a10-4d53-bf4d-139c189dff18" />
<img width="1052" height="681" alt="image" src="https://github.com/user-attachments/assets/48e04713-128e-442c-a589-d2b5d1d00906" />
<img width="810" height="160" alt="image" src="https://github.com/user-attachments/assets/b71221c8-38be-4715-b52c-3ed3260921db" />

# CODE : SIMULATION + QUEUE
```
class Solution {
private:
    static constexpr int mod = 1000000007;

public:
    int peopleAwareOfSecret(int n, int delay, int forget) {
        deque<pair<int, int>> know, share;
        know.emplace_back(1, 1);
        int know_cnt = 1, share_cnt = 0;
        for (int i = 2; i <= n; ++i) {
            if (!know.empty() && know[0].first == i - delay) {
                know_cnt = (know_cnt - know[0].second + mod) % mod;
                share_cnt = (share_cnt + know[0].second) % mod;
                share.push_back(know[0]);
                know.pop_front();
            }
            if (!share.empty() && share[0].first == i - forget) {
                share_cnt = (share_cnt - share[0].second + mod) % mod;
                share.pop_front();
            }
            if (!share.empty()) {
                know_cnt = (know_cnt + share_cnt) % mod;
                know.emplace_back(i, share_cnt);
            }
        }
        return (know_cnt + share_cnt) % mod;
    }

};
```


# OPTIMAL CODE : DP
```
class Solution {
private:
    static constexpr int mod = 1000000007;  // modulus to avoid large numbers, 1e9+7 = 1000000007
    
public:
    int peopleAwareOfSecret(int n, int delay, int forget) {
        // dp[i] = number of people who learn the secret on day i
        vector<long long> dp(n + 1, 0);
        
        // On day 1, exactly 1 person knows the secret
        dp[1] = 1;
        
        long long share = 0; // running total of how many people can currently share
        
        // iterate over each day
        for (int i = 2; i <= n; i++) {
            
            // 1️⃣ Add people who become eligible to share today
            // People who learned the secret (delay days ago) start sharing today
            if (i - delay >= 1) {
                share = (share + dp[i - delay]) % mod;
            }
            
            // 2️⃣ Remove people who forget today
            // People who learned the secret (forget days ago) forget today
            if (i - forget >= 1) {
                share = (share - dp[i - forget] + mod) % mod;
            }
            
            // 3️⃣ People who can share today create new learners
            dp[i] = share;  // all current sharers tell the secret to 1 new person each
        }
        
        // Final answer = all people who still remember the secret at day n
        long long result = 0;
        for (int i = n - forget + 1; i <= n; i++) {
            if (i >= 1) {
                result = (result + dp[i]) % mod;
            }
        }
        
        return (int)result;
    }
};

```
