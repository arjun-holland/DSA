# Problem
```
P1 :- Given a Tree of N Nodes, rooted at node 1 find the maximum sum of subtree possible.
```
---

# Sol : - Find the sum of all the subtrees and find the maximum. 
```
TC : O(N)--->
SC : O(N) → Sum array 
-> O(N)--> for the graph of tree→ you can ignore this depending on the interviewer
→ Recursion takes O(N) space in the worst case; so you may consider that too —> O(height) ; but in the worst case ; height = N. 
```
---
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll ; 
ll sum[500000+5];
int b[500000+5];

void DFS(int node,vector <int> G[],int used[],int parent[]){
    used[node] = 1 ;

    for(auto u: G[node]){ //iterating all children "u" of "node"
        
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
            s = s + sum[child]; 
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
    DFS(1,G,used,parent); //starts from node 1  
    
    ll answer = -100000000000000;    
    i = 1 ;
    while(i<=n){
        answer=max(answer,sum[i]);    //get trhe maximum subarray sum
        i++;
    }
    cout<<(answer); 
    return 0 ; 
}

```

