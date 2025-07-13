# Problem 
<img width="1084" height="406" alt="image" src="https://github.com/user-attachments/assets/f6d38693-3c7f-4336-94b0-24db1fea45ab" />

<img width="904" height="610" alt="image" src="https://github.com/user-attachments/assets/c76b2738-8007-4558-8df7-f717e6904636" />

<img width="927" height="365" alt="image" src="https://github.com/user-attachments/assets/37207dfe-3f41-42df-86ab-927b4e08349b" />

# Intuition
```
As maximum edge cost can be the highest edge cost (In question he saya atmost k connected componenets that means the highest cost edge is ans for entire graph(0-connected graph))
but we need the answer which has to be minimum of the maximum cost, we have to find the median of the maximum value(highest cost) and the minimum value(0) which
means we have to use the binary search on answer ans here the median(mid) indicates that the minimum of tha maximum cost
If we gather all the edges which are having less than or equal to that median cost that means they all can form one component and
if we write a DFS just to find how many components are there in the graph if we form a compound one of the component with the justice the
less than or equal to that cost
```

# Code 
```
class Solution {
public:
    // Depth-First Search to mark all nodes reachable from 'node'
    void DFS(vector<vector<int>>& adj, int node, vector<int>& visited) {
        visited[node] = true;
        for (auto neighbor : adj[node]) {
            if (!visited[neighbor]) DFS(adj, neighbor, visited);
        }
    }

    // Check if it's possible to partition the graph into ≤ k connected components using only edges with cost ≤ maxCost
    bool check(vector<vector<pair<int, int>>>& graph, int maxCost, int k) {
        int n = graph.size();

        // Build an adjacency list including only edges with cost ≤ maxCost
        vector<vector<int>> adj(n);
        for (int i = 0; i < n; i++) {
            for (auto [neighbor, cost] : graph[i]) {
                if (cost <= maxCost) {
                    adj[i].push_back(neighbor);
                }
            }
        }

        // Count connected components using DFS
        vector<int> visited(n, false);
        int components = 0;

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                components++;
                if (components > k) return false;  // If more than k components are needed, this cost is too low
                DFS(adj, i, visited);
            }
        }

        // It's possible to form ≤ k components with cost ≤ maxCost
        return true;
    }

    // Binary search to find the **minimum cost** to divide the graph into ≤ k components
    int minCost(int n, vector<vector<int>>& edges, int k) {
        if(edges.empty()) return 0;

        vector<vector<pair<int, int>>> graph(n);
        int low = 0, high = -1;

        // Build full graph and determine the maximum edge cost
        for (int i = 0; i < edges.size(); i++) {
            int u = edges[i][0], v = edges[i][1], cost = edges[i][2];
            graph[u].push_back({v, cost});
            graph[v].push_back({u, cost});
            high = max(high, cost);           // upper bound for binary search
        }

        int ans = high;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (check(graph, mid, k)) {
                ans = mid;               // valid: try lower cost
                high = mid - 1;
            } else {
                low = mid + 1;           // not valid: need higher cost
            }
        }
        return ans;    // minimum cost that allows splitting into ≤ k components
    }
};

```
