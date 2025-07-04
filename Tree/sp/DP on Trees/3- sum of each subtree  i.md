# problem
```
P1 : -  Given a Tree of N Nodes, rooted at node 1 find the sum of each subtree “i” in the given tree. 
Sum[i] = value of node “i” + sum(sum[c1] + sum[c2] + sum[c3] +...sum[cg]) = sum of subtree rooted at node ‘i’ 
—-> c1,c2,..............cg:-> children of node “i” 
```
## 🧠 Intuition Behind DP on Tree — Subtree Sum Problem
### 📌 Problem:
> Given a Tree of `N` nodes rooted at node `1`, find `Sum[i]`  
> where `Sum[i]` = sum of the subtree rooted at node `i`.
---
## 🤯 Why Is This DP on Trees?
- The value of `Sum[i]` depends on the values of all its children.
- Leaf nodes have a **fixed value** (base case): they have **no children** → their subtree sum is just their own value.
- Therefore, you **must compute children's values before the parent** — **Bottom-Up** approach!
---
## 🔁 Core Formula:
```text
Sum[i] = value[i] + Sum[c1] + Sum[c2] + ... + Sum[ck]
```

# Pseudo Code 
```
---> sum[n+1]   //to store sum each subtree of i node, 1 based index
-> b[n+1]   //globally taken the array to store the value of each node

void DFS(integer node,G[][],used[],parent[]){
    used[node] = 1 ; 
    
    for(auto u: G[node]){                //iterating all children "u" of "node"
        if(used[u]==0){
            //if this node/branch has never been visited before , just go into it and search it using dfs in recursion
            parent[u] = node ; 
            DFS(u,G,used,parent);
            
        }
    }

    print(node)
    ----> bottom up traversal 
    s = 0 ;   //taking sum = 0

    for(auto child: G[node]){
        if(child==parent[node]){
            //it means the child node is parent of the node
            //it is not the child
            //ignore it
        } 
        else{ 
            s = s + sum[child] 
        }      
    }
    sum[node] = b[node] + s   
}

-> n 
G[n+5][]  

i = 1 ; 
while(i<=n-1){
    read(u)
    read(v)
    G[u].push_back(v);
    G[v].push_back(u); 
    i++;
}

i = 1 
while(i<=n){
    read(b[i])
    i=i+1
}
    
used[n+1]-->0
parent[n+1]-->0
    
DFS(1,G,used,parent); //starts from node 1   
    
i = 1 
while(i<=n){
    print(sum[i])
    i=i+1
}    
   return 0 ; 
}
```
