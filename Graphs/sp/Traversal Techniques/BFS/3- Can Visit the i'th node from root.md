## 📘 Problem Statement

You are given:
- An undirected graph `G` with `N` nodes and `M` edges.
- Node `1` is the source node.

🧩 **Your task**:  
Print **"yes"** if node `i` is reachable from node `1`, otherwise print **"no"** for each `i` from `1` to `N`.

---

## 💡 Intuition

The problem is about finding which nodes can be **reached from a given starting node (node 1)** in an undirected graph.  
We use **BFS** starting from node 1 and **mark each visited node**.  
After the traversal, any node **not visited** is **not reachable** from node 1.

---

## 🛠️ Solution (C++ using Adjacency List & BFS)

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    ll n, m;
    cin >> n >> m;

    // Construct the graph using adjacency list
    vector<ll> G[n + 5];

    for (ll i = 1; i <= m; i++) {
        ll u, v;
        cin >> u >> v;
        G[u].push_back(v);
        G[v].push_back(u);         // Undirected graph
    }

    queue<ll> q;
    ll source;
    cin >> source;

    q.push(source);
    ll used[n + 5] = {0};    //we can take vector<ll> used(n+1,0);
    used[source] = 1;

    ll lvl[n + 5] = {0};
    lvl[source] = 0;

    // Perform BFS
    while (!q.empty()) {
        ll v = q.front();
        q.pop();

        for (auto u : G[v]) {
            if (used[u] == 0) {
                q.push(u);
                used[u] = 1;
                lvl[u] = lvl[v] + 1;
            }
        }
    }

    // Output reachability result
    for (ll i = 1; i <= n; i++) {
        if (used[i] == 0) {
            cout << "no\n";
        } else {
            cout << "yes\n";
        }
    }

    return 0;
}
