//Submission : https://leetcode.com/problems/minimum-jumps-to-reach-end-via-prime-teleportation/submissions/1716463290/ 

# Problem
<img width="1206" height="469" alt="image" src="https://github.com/user-attachments/assets/9578e9df-a582-4ff0-8274-0d53b5730818" />
<img width="1168" height="454" alt="image" src="https://github.com/user-attachments/assets/a1b7fb1b-2dae-4577-aef3-e31cb46ab611" />
<img width="1126" height="453" alt="image" src="https://github.com/user-attachments/assets/d9fa940f-f808-48f2-a2e2-52282a0dc5e9" />
<img width="1017" height="263" alt="image" src="https://github.com/user-attachments/assets/f2178373-1594-493b-82e2-0977b602155a" />
<img width="751" height="159" alt="image" src="https://github.com/user-attachments/assets/e2287dcb-b2b6-4809-a80a-1341365a4228" />

# Intution
<img width="1072" height="258" alt="image" src="https://github.com/user-attachments/assets/221b403a-d39b-4d11-ba19-d0cc7bcca147" />
<img width="1105" height="583" alt="image" src="https://github.com/user-attachments/assets/7682229d-e8be-464a-a8e8-f2e0e5de323a" />

<img width="1163" height="374" alt="image" src="https://github.com/user-attachments/assets/c242cbf4-7294-47fa-bddc-47280f9d1a6c" />
<img width="1170" height="476" alt="image" src="https://github.com/user-attachments/assets/c068746a-0f27-4099-8519-800b22da3730" />


# Code
```
vector<bool> isPrime (1e6 + 1, true);

class Solution {
public:
    void fill () {      //seive()
        isPrime [0] = isPrime [1] = false;
        for (int i = 2; i * i <= 1e6; ++i) {
            if (isPrime [i]) {
                for (int j = i * i; j <= 1e6; j += i)
                    isPrime [j] = false;
            }
        }
    }

    int minJumps(vector<int>& nums) {
        if (isPrime[0]) fill();

        int n = nums.size();
        unordered_map <int,vector <int>> mp;
        for (int i = 0; i < n; i++) mp[nums[i]].push_back(i);  //mp : value -> index
        
        vector<int> dist (n, -1);
        queue<int> qu;   //hold the inidices

        qu.push(0); dist[0] = 0;
        unordered_set<int> used;

        while (!qu.empty()) {  
            int node = qu.front();qu.pop();

            if (node - 1 >= 0 && dist[node-1] == -1) {
                qu.push(node-1);
                dist[node-1] = dist[node] + 1;
            }
            if (node + 1 < n && dist[node+1] == -1) {
                qu.push(node+1);
                dist[node+1] = dist[node] + 1;
            }

            if (isPrime[nums[node]] == false || used.contains(nums[node])) continue;

            //when the node is prime 
            for (int i = 1; i*nums[node] <= 1e6 ; i++) {
                if (mp.contains(i*nums[node]) == false) continue;
                for (auto it : mp[i*nums[node]]) {
                    if (dist[it] != -1) continue;
                    qu.push(it);
                    dist[it] = dist[node] + 1;
                }
            }
            used.insert(nums[node]);
        }
        return dist.back();
    }
};
```


---
# Crux in the Problem
<img width="917" height="749" alt="image" src="https://github.com/user-attachments/assets/dfd9ac17-b5e1-460a-ab39-8cce6a12c404" />
<img width="1000" height="698" alt="image" src="https://github.com/user-attachments/assets/1daae668-fb1d-418c-8b0d-ee6acddcc49d" />

# Optimized Intuition
<img width="857" height="527" alt="image" src="https://github.com/user-attachments/assets/daed2400-195a-45c5-a392-ca3affea7d55" />

<img width="1760" height="850" alt="image" src="https://github.com/user-attachments/assets/db2afb24-e412-4fac-a5d1-a7e7b2cf4298" />

## Time complexity for finding no.of multiplies of p(prime number) in 10^6 range = Tailer Series

<img width="1784" height="847" alt="image" src="https://github.com/user-attachments/assets/63e44966-2617-40b9-b557-fb08bf37cc8c" />

<img width="886" height="811" alt="image" src="https://github.com/user-attachments/assets/fd21aa23-8643-4a94-a89a-894f2a7a193e" />
<img width="839" height="493" alt="image" src="https://github.com/user-attachments/assets/3081b0d8-f6f0-4754-a1fe-69633761b3c4" />

# 🚀 Summary of the Optimization

| Part                         | Complexity             |
| ---------------------------- | ---------------------- |
| Sieve / Prime Precomputation | O(d log log d)         |
| Graph Construction           | O(n + d log log d)     |
| BFS Traversal (0-1 BFS)      | O(n + d log log d)     |
| **Total**                    | **O(n + d log log d)** |

Where n = array size, d = max(nums[i]) = 1e6

<img width="851" height="281" alt="image" src="https://github.com/user-attachments/assets/f856adba-85bd-421a-848a-66b983f93b8d" />


# Dry Run
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/61776d25-b3e1-4d7f-ae17-81787e82c923" />

# Code
```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

// Utility macros
#define fo(i, start, end) for (ll i = start; i <= end; i++)
#define all(x) x.begin(), x.end()

class Solution {
public:
    // Sieve of Eratosthenes to mark prime numbers up to 'my'
    vector<bool> sieve(int my) {
        vector<bool> is_prime(my + 1, true);
        is_prime[0] = is_prime[1] = false;

        for (int i = 2; i * i <= my; ++i) {   //O(N log log N)
            if (is_prime[i]) {
                for (int j = i * i; j <= my; j += i) {
                    is_prime[j] = false;
                }
            }
        }
        return is_prime;
    }

    int minJumps(vector<int>& b) {
        int n = b.size(), max_val = 0;
        unordered_map<int, int> freq;

        // Step 1: Precompute max element and frequency map
        fo(i, 0, n - 1) {
            freq[b[i]]++;
            max_val = max(max_val, b[i]);
        }

        // Step 2: Precompute primes up to max_val
        vector<bool> is_prime = sieve(max_val);

        // g[val] holds all indices where b[i] == val
        vector<vector<int>> g(max_val + 1);
        fo(i, 0, n - 1) {
            g[b[i]].push_back(i);
        }
 
        // G is the final graph with nodes: [0, n-1] (array indices), [n, 2n+15] (God nodes)
        vector<vector<pair<int, int>>> G(2 * n + 15);

        // Step 3: Add adjacent index edges with cost 1
        fo(i, 1, n - 2) {
            G[i].push_back({i - 1, 1});
            G[i].push_back({i + 1, 1});
        }
        if (n >= 2) {
            G[0].push_back({1, 1});
            G[n - 1].push_back({n - 2, 1});
        }

        ll god_node = n;  // start assigning god nodes from index 'n'

        // Step 4: Build edges using God node mechanism
        fo(i, 2, max_val) {
            if (is_prime[i] && freq[i] >= 1) {
                // 1. Connect every index with value == i to god node (cost 0)
                for (int idx : g[i]) {
                    G[idx].push_back({god_node, 0});
                }

                // 2. Connect god node to every index where value is multiple of i (cost 1)
                for (int j = i; j <= max_val; j += i) {
                    for (int idx : g[j]) {
                        G[god_node].push_back({idx, 1});
                    }
                }

                god_node++; // move to next god node
            }
        }

        // Step 5: 0-1 BFS to find shortest path from index 0 to index n-1
        vector<int> dist(god_node + 1, INT_MAX);
        deque<int> dq;
        dist[0] = 0;
        dq.push_front(0);

        while (!dq.empty()) {
            int u = dq.front(); dq.pop_front();
            for (auto [v, wt] : G[u]) {
                if (dist[u] + wt < dist[v]) {
                    dist[v] = dist[u] + wt;
                    if (wt == 0)
                        dq.push_front(v);  // zero-cost edge -> front
                    else
                        dq.push_back(v);   // cost-1 edge -> back
                }
            }
        }

        return dist[n - 1];
    }
};
```

# Optimal Submission: 
https://leetcode.com/problems/minimum-jumps-to-reach-end-via-prime-teleportation/submissions/1721630515/
