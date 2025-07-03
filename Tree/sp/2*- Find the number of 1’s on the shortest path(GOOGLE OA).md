# Problem
```
Google Interview Problem.-> Given a Tree of ‘N’ Nodes and ‘N-1’ Edges; rooted at Node-1 ; each node is assigned either 1 or 0 ; 
for each node “i” ; find the number of 1’s on the shortest path from node '1' to node “i”
```

# Intuition
```
From any node ‘x’ to any node ‘y’ ; there is only 1 single path in the tree ; and that is only the shortest path ; 
Reframing the question :->  Given a Tree of ‘N’ Nodes and ‘N-1’ Edges; rooted at Node-1 ; each node is assigned either 1 or 0 ;
for each node “i” ; find the number of 1’s on the shortest path from node 1 to node “i

         1(1)
        / \
     2(0)   3(1)
           / \
        4(1)  5(0)

Node:     1  2  3  4  5
Answer:   1  1  2  3  2
```

# solution
```
#include <bits/stdc++.h>    // Includes all standard C++ libraries
using namespace std;

int main() {
    int n ; 
    cin >> n ;  // Read number of nodes in the tree

    int b[n+1] = {0};  // Array to store value (0 or 1) of each node; using 1-based indexing

    vector<int> G[n+1];  // Adjacency list to store the tree
    int i = 1 ; 
    while(i <= n-1) {  // Read n-1 edges of the tree
        int x, y ; 
        cin >> x >> y ;  // Read an undirected edge between x and y
        G[x].push_back(y);  // Add y to the adjacency list of x
        G[y].push_back(x);  // Add x to the adjacency list of y (since it's undirected)
        i++;
    }
    
    i = 1 ; 
    while(i <= n) {  // Read the binary values assigned to each node
        cin >> b[i];  // b[i] is either 0 or 1
        i++;
    }

    queue<int> q ;         // Queue for BFS traversal
    int used[n+1] = {0};   // Array to keep track of visited nodes (0 = not visited, 1 = visited)

    used[1] = 1 ;  // Mark root node (1) as visited
    q.push(1);     // Start BFS from node 1

    int answer[n+1] = {0};  // answer[i] will store number of 1s on path from node 1 to i
    answer[1] = b[1] ;      // Initialize answer for root node (itself either 0 or 1)

    while(!q.empty()) {  // Standard BFS loop
        int top = q.front();    // Get the front node in the queue
        q.pop();                // Remove it from the queue

        for(auto u : G[top]) {  // Traverse all adjacent nodes (neighbors) of current node
            if(used[u] == 0) {  // If neighbor node hasn't been visited yet
                used[u] = 1 ;   // Mark it as visited
                q.push(u);      // Push it into the queue for further exploration

                if(b[u] == 1) {  // If the node itself is 1
                    answer[u] = answer[top] + 1 ;  // Add 1 to the parent's count
                }
                else {
                    answer[u] = answer[top];       // Else, inherit parent's count
                }
            }
            else {
                // Already visited node; do nothing (this avoids going back to parent)
            }
        }
    }

    i = 1 ; 
    while(i <= n) {                   //Output the answer for each node
        cout << answer[i] << '\n';    // Print number of 1s on the path from node 1 to i
        i++;
    }   
    return 0 ;  // Program ends
}
```

