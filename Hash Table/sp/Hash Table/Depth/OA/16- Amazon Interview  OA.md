# Problem
<img width="681" height="244" alt="image" src="https://github.com/user-attachments/assets/418891be-0f5f-4114-99d3-2fbc4b99b515" />

`Sum of first and last element of the subarray = k : find shortest subarray`

# Intuition
## Brute Force : O(n^2)
```
->n.
->b[n+1],k
u = INT_MAX;
for(i=1;i<=n;i++){
    for(j=i+1;j<=n;j++){
        //[i......j]
        if(b[i]+b[j]==k){
            l = j - i + 1 
            u = min(u,l)
        }
    }
}
print(u)
```
## Optimal :
```
#include <iostream>
#include <vector>
#include <unordered_map>
#include <climits>
using namespace std;

int main() {
    int n;
    cin >> n;
    
    vector<int> b(n + 1);
    for(int i=1;i<=n;i++) cin>>b[i];

    int k;cin >> k;
    
    int u = INT_MAX;
    unordered_map<int, int> k_map;
    
    for (int j = 1; j <= n; j++) {
    	  int end = b[j];
        int start = k - end;
        if(k_map.count(start)){
        	int i = k_map[start];
	        int l = j - i + 1;
	        u = min(u, l);
        }
        k_map[end] = j;
    }
    cout << u << endl;
    return 0;
}
```


## Follow Up question
```
Find longet valid subarray

    Use the above code but modify that `int u = INT_MAX;` to `int u = 0;` 
```
