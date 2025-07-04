# Problem Statement:
```
Given a tree with n nodes, rooted at node 0 (nodes are numbered from 0 to n−1), with values assigned to nodes such that values[i] denotes
the value of node i, find the maximal sum of values along any path starting at some node u and going only downward in the tree.
In other words, only consider paths u₁, u₂, u₃, ..., uₖ where each node uᵢ is a child of node uᵢ₋₁ for 1 < i ≤ k.
```
# constraints
```
Understanding -> Given a Tree of “N” nodes and “N-1” edges; each node has a value; b[i] -> value of the ith node. Tree is rooted at node 1(1—>N)
-1000000000<=b[i]<=1000000000
-> Find any path in the tree with a maximum sum such that it only goes downwards. 
```
# Intuition Understanding
```
-> ex:-

                               1(10)
                              /     \
                          2(2)     3(3)      //solve this in Prefix sum from root to leaf
                           /    \
                        4(4)    5(5)

            Ans: 5 + 2 + 10 => 17
 -------------------------------------------------------------------------------------------------------
                                -3
                              /   \
                           -8       -1         //solve this with best downward path sum
                          /            \
                       -30              5
                                        / \
                                       10   8
            Ans: 10 + 5 = 15

```
# solution
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll ; 
ll sum[500000+5];
int b[500000+5];

void DFS(int node,vector <int> G[],int used[],int parent[]){
    used[node] = 1 ; 
    
    for(auto u: G[node]){          //iterating all children "u" of "node"
        
        if(used[u]==0){
            //if this node/branch has never been visited before 
            //just go into it and search it using dfs in recursion
            parent[u] = node ; 
            DFS(u,G,used,parent);
            
        }
    }

    //print(node)--->parent
    //----> bottom up traversal

    ll s = 0 ; 
    for(auto child: G[node]){
        
        if(child==parent[node]){
            //it means the child node is parent of the node
            //it is not the child
            //ignore it
        }
        
        else{
            s = max(s, sum[child]);   //get sum of max child
        }
    }
    sum[node] = b[node] + s; 
}

int main(){
    int n ; 
    cin>>n ; 
    vector <int> G[n+1];
    int i = 1 ; 
    while(i<=n){
        cin>>b[i] ; 
        i++;
    }
    
    i = 1 ; 
    while(i<=n-1){
        int u,v;
        cin>>u>>v ; 
        G[u].push_back(v);
        G[v].push_back(u); 
        i++;
    }
    int used[n+1] = {0};
    int parent[n+1] = {0};
    DFS(1,G,used,parent);          //starts from node 1  
    
    ll answer = -100000000000000;    
    i = 1 ;
    while(i<=n){
        answer = max(answer,sum[i]);
        i++;
    }
    cout<<(answer); 
    return 0 ; 
}
```
