# Sumbission Link
https://leetcode.com/problems/minimum-score-after-removals-on-a-tree/submissions/1716486968/?envType=daily-question&envId=2025-07-24

# Problem
<img width="1023" height="639" alt="image" src="https://github.com/user-attachments/assets/e3566f18-33b9-42f0-b6d9-982dad53f253" />
<img width="1023" height="700" alt="image" src="https://github.com/user-attachments/assets/33418569-ac9d-4baa-923c-c45badd649d6" />
<img width="1018" height="681" alt="image" src="https://github.com/user-attachments/assets/0c42c431-b4d0-4ad6-8da5-873238973839" />
<img width="976" height="445" alt="image" src="https://github.com/user-attachments/assets/1ddd32c4-6213-48ed-a9eb-9503b843dd24" />

# Code
```
T.C : O(n^2)
S.C : O(V+E), V = number of vertices and E = number of edges
```
```
class Solution {
public:
    void dfs(int node, int parent, vector<int>& subtreeXor, vector<int>& inTime, vector<int>& outTime,
            int &timer, vector<int>& nums, unordered_map<int, vector<int>>& adj) {
                
            subtreeXor[node] = nums[node];
            inTime[node] = timer;
            timer++;
            for(int &ngbr : adj[node]) {
                if(ngbr != parent) {
                    dfs(ngbr, node, subtreeXor, inTime, outTime, timer, nums, adj);
                    subtreeXor[node] ^= subtreeXor[ngbr];
                }
            }
            outTime[node] = timer;
            timer++;
    }

    bool isAncestor(int u, int v, vector<int>& inTime, vector<int>& outTime) {
        return inTime[v] >= inTime[u] && outTime[v] <= outTime[u];
    }

    int getScore(int a, int b, int c) {
        int maxXor = max({a, b, c});
        int minXor = min({a, b, c});

        return maxXor - minXor;
    }
    int minimumScore(vector<int>& nums, vector<vector<int>>& edges) {
        int n = nums.size(); //Total number of nodes

        unordered_map<int, vector<int>> adj; //adjacency list
        for(auto &edge : edges) {
            int u = edge[0];
            int v = edge[1];

            adj[u].push_back(v);
            adj[v].push_back(u);
        }

        vector<int> subtreeXor(n, 0);

        vector<int> inTime(n, 0);
        vector<int> outTime(n, 0);

        int timer = 0;

        //root = 0
        dfs(0, -1, subtreeXor, inTime, outTime, timer, nums, adj);

        int result = INT_MAX;
        for(int u = 1; u < n; u++) {
            for(int v = u+1; v < n; v++) {
                int xor1;
                int xor2;
                int xor3;

                if(isAncestor(u, v, inTime, outTime)) {
                    xor1 = subtreeXor[v];
                    xor2 = subtreeXor[u] ^ subtreeXor[v];
                    xor3 = subtreeXor[0] ^ xor1 ^ xor2;
                } else if(isAncestor(v, u, inTime, outTime)) {
                    xor1 = subtreeXor[u];
                    xor2 = subtreeXor[v] ^ subtreeXor[u];
                    xor3 = subtreeXor[0] ^ xor1 ^ xor2;
                } else {
                    xor1 = subtreeXor[u];
                    xor2 = subtreeXor[v];
                    xor3 = subtreeXor[0] ^ xor1 ^ xor2;
                }

                result = min(result, getScore(xor1, xor2, xor3));
            }
        }

        return result;

    }
};
```

<img width="1052" height="264" alt="image" src="https://github.com/user-attachments/assets/261a2760-4e49-4ef9-9cc5-b0f7a6218e63" />
<img width="817" height="273" alt="image" src="https://github.com/user-attachments/assets/4ece6ae4-9b21-4bcb-9a2b-73cd006867a1" />
