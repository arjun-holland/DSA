# 🔄 Breadth-First Search (BFS) – Graph Traversal

Breadth-First Search is a fundamental graph traversal algorithm that explores vertices **level by level** starting from a source node. 
It uses a **queue** to keep track of nodes to visit.

---

## code
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll ; 

int main() {
    int n ; 
    cin>> n ; 
    int m ;
    cin>> m ; 
    vector <int> G[n+5] ; 
    
    int i = 1 ; 
    while(i<=m){
        int x,y;
        cin>>x>>y;
        G[x].push_back(y);
        G[y].push_back(x);
        i++;
    }
    
    
    int source = 1 ;     // Start traversal from source 
    int used[n+5] = {0};   //to make sure that node is used 
    int level[n+5] = {0} ; 
    queue <int> q ; 
    
    q.push(source);         //push source into the queue q
    used[source] = 1 ;      //mark source node as visited
    level[source] = 0 ;     //source node is always at 0-level

    while(!q.empty()) {        
        int removed = q.front();
        cout<<removed<<" ";
        q.pop();
        cout<<level[removed]<<"\n"; 
 
        for(auto u : G[removed]){   //neighbours nodes of removed node
            if(used[u]==0) { 
                q.push(u); 
                used[u] = 1 ;
                level[u] = level[removed] + 1 ; 
            }
        }        
    }
    return 0 ; 
}
```


## 📘 Code Summary

This C++ code:
- Takes input of `n` nodes and `m` edges.
- Builds an **adjacency list** to represent the graph.
- Performs BFS starting from `source = 1`.
- Outputs the order of nodes visited and their levels (distance from the source).

---


## 📦 Data Structures Used

| Structure | Purpose |
|----------|---------|
| `vector<int> G[]` | Adjacency list |
| `queue<int> q` | BFS queue |
| `used[]` | Marks visited nodes |
| `level[]` | Stores depth from source |

---

## 🔄 BFS Algorithm Steps

1. Enqueue the **source** node and mark as visited.
2. While the queue is not empty:
   - Dequeue a node.
   - For each unvisited neighbor:
     - Mark as visited.
     - Set its level to current node's level + 1.
     - Enqueue it.

---

## 📌 BFS Properties

| Feature | Value |
|--------|-------|
| Time Complexity | `O(V + E)` |
| Space Complexity | `O(V)` |
| Type | Level-order traversal |
| Good For | Shortest path in unweighted graphs, Layer-wise exploration |

---

## 🛠️ Applications of BFS

- Finding shortest path in **unweighted** graphs
- Peer-to-peer networking (like BitTorrent)
- Crawling the web (like Googlebot)
- Social networking (finding degrees of separation)
- GPS navigation (simplified models)

---

## 💡 Bonus Tip:
Use BFS when you need the **shortest path** or want to explore **closest neighbors first**. For trees, it's ideal for **level-order traversal**.

---




