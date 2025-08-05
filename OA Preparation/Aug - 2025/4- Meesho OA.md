# Problem
<img width="965" height="467" alt="image" src="https://github.com/user-attachments/assets/a072b20e-c064-430c-ac6d-ec81b559603c" />


# Intuition
<img width="780" height="161" alt="image" src="https://github.com/user-attachments/assets/0cc36610-6269-46ac-9542-ff351bdc6f63" />

<img width="940" height="326" alt="image" src="https://github.com/user-attachments/assets/551e926b-26d0-40dd-bb1d-e9e35883cac6" />
<img width="907" height="404" alt="image" src="https://github.com/user-attachments/assets/cffbbea4-9cce-4f64-8007-07a18a2abe61" />
<img width="882" height="685" alt="image" src="https://github.com/user-attachments/assets/e81c86e9-d3d2-483b-8ced-c3ea0bdbb534" />

## Important Counting trick in 
<img width="769" height="432" alt="image" src="https://github.com/user-attachments/assets/de812c7b-be16-4578-82eb-c5d783f6cfeb" />
<img width="726" height="422" alt="image" src="https://github.com/user-attachments/assets/55f84fbc-a25f-417e-8cfc-0863896d9259" />
<img width="760" height="319" alt="image" src="https://github.com/user-attachments/assets/170045b7-5e0b-43bd-b59e-1d70e8dd4f7b" />
<img width="755" height="512" alt="image" src="https://github.com/user-attachments/assets/26cddf43-dc9d-468d-bce5-09a9571cd991" />
<img width="769" height="346" alt="image" src="https://github.com/user-attachments/assets/dc393a11-1235-44e9-ac88-322399be2c50" />


<img width="1249" height="922" alt="image" src="https://github.com/user-attachments/assets/6a5bb9ce-9ced-410b-8bd1-ea5de8c58e2f" />
<img width="664" height="231" alt="image" src="https://github.com/user-attachments/assets/2c419799-1c94-4b1e-a87d-fd7b1c7190ca" />


# Code
```
#include <bits/stdc++.h>
using namespace std;
 
// Sieve for prime checking
vector<int> isPrime(1e6+1, 1);
void sieve() {
    isPrime[0] = isPrime[1] = 0;
    for (int i = 2; i*i <= 1e6; ++i) {
        if (isPrime[i]) {
            for (int j = i*i; j <= 1e6; j += i)
                isPrime[j] = 0;
        }
    }
}
 
int bfs_count(int start, int parent, const vector<vector<int>> &adj) {
    // BFS starting from 'start', not crossing black nodes, except entry node
    int cnt = 0;
    queue<pair<int,int>> q;
    q.push({start, parent});
    while (!q.empty()) {
        int u = q.front().first, p = q.front().second; 
          q.pop();
        if (isPrime[u]) continue; // stop at black
        ++cnt; // white node found
        for (int v : adj[u]) {
            if (v != p)
                q.push({v,u});
        }
    }
    return cnt;
}
 
int main() {
    int n;
    cin >> n;
    vector<vector<int>> adj(n+1);
    for (int i=1; i<n; ++i) {
        int u,v; cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    sieve();
 
    // If node values are their labels:
    // (Otherwise, read values in and check isPrime[val[node]])
 
    int total = 0;
    for (int i = 1; i <= n; ++i) {
        if (!isPrime[i]) continue;   //if i is not a black node
 
 
        //For every black node assume that it is the root node
        vector<int> white_subtree_counts;
        for (int neigh : adj[i]) {   // 2 => 1, 4  , for all neighbours of that root node
            int cnt = bfs_count(neigh, i, adj);
            if (cnt > 0)
                white_subtree_counts.push_back(cnt);
        }
 
        // Count single white paths (i to each white node) (seperate branchs are all valid from i)
        int sum = 0;
        for (int c : white_subtree_counts) sum += c;
        total += sum;
 
        // Count all pairs of whites from different subtrees This is sum of products of pairs
        int cur_sum = 0;   // sum of all previous (seen white nodes) subtree sizes encountered so far.
        for (int c : white_subtree_counts) {  //For the current subtree of size c,it can pair with all previously seen white nodes 
            total += c * cur_sum;
            cur_sum += c;   // update cur_sum by adding c to it (so next subtrees can pair with this subtree too).
        }
    }
    cout << total << '\n';
    return 0;
}
```


# Run:
https://ideone.com/A77Ih5
