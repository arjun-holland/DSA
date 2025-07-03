# Problem
```
Q :-> Given a Tree of “N” nodes and N-1 edges ; rooted at node “1” ; print “N” integers ; 
where the ith integer prints the number of children of the ith node. 
Once this is done ; print all the leaves of the particular tree. 
```

# solution : As we need the no.of childs per node we can use 'level wise traversal' Tree traversal technique.
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n ; 
    cin>>n ;   //no.od nodes
    vector <int> G[n+1];  //as 1 based index
    int i = 1 ;  //no.od edges
    while(i <= n-1){   //edges always 'n-1' when 'n' nodes in TREE
        int x,y ; 
        cin >> x >> y ;
        G[x].push_back(y);
        G[y].push_back(x);
        i++;
    }

    queue <int> q ; 
    int used[n+1] = {0};   //visited vector: all nodes are not visited
    used[1] = 1 ; 
    q.push(1); 
    
    while(!q.empty()){
        
        int node = q.front();
        q.pop();
        int c = 0 ;               //for count the no.of childs for node
        for(auto u : G[node]){      //all neighbours of node
            if(used[u] == 0){
                c++;
                used[u] = 1 ; 
                q.push(u);
            }
            //else the node is parent dont use it
        }
        cout << node <<" "<<c ; 
        cout<<'\n';
    }  
    return 0 ; 
}
```
