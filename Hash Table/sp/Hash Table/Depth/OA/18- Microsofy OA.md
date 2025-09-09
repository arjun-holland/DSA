# Probelm
<img width="677" height="227" alt="image" src="https://github.com/user-attachments/assets/1a75ca41-1ba2-42c0-ae0a-e61d611b1bdb" />

# Intuition
## Brute Force : O(n^4)
``` 
-> n 
-> b[n+1] r = 0

for(i=1; i<=n; i++){
    for(j=i+1; j<=n; j++){
        for(k=j+1; k<=n; k++){
            for(l=k+1; l<=n; l++){
                if(b[i]+b[j]+b[k]+b[l]==0){   
                    r = r + 1 
                }            
            }
        }
    }
}
print(r)
```

## Optimal 1 : O(n^3)
<img width="666" height="243" alt="image" src="https://github.com/user-attachments/assets/8484e0e4-0bbc-47f6-b050-47c809e316d8" />
<img width="1272" height="704" alt="image" src="https://github.com/user-attachments/assets/f490610f-52ae-48da-9b27-332c54367a5c" />
<img width="717" height="391" alt="image" src="https://github.com/user-attachments/assets/c30d2ed8-83e0-4abb-9bb6-7d62ad704b36" />
<img width="727" height="394" alt="image" src="https://github.com/user-attachments/assets/4fc06c69-cb93-4434-8935-2b374cdc7ff2" />
<img width="738" height="406" alt="image" src="https://github.com/user-attachments/assets/5368fd31-cb87-4237-8db8-1d6a7d9cdb94" />
### When k { which has hashmap from (K+1 to n) } incremented to k+1 then we need hasnmap from k+2 to n .
<img width="727" height="416" alt="image" src="https://github.com/user-attachments/assets/91958bd9-3f49-4b2e-b0cd-855f059aaa6f" />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;

    vector<int> b(n + 1);
    unordered_map<int, int> u;
    long long r = 0;

    // Input array b
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // Initializing hashmap for elements in range [4, n] because we aree having i = 1,j = 2, k = 3 and l = 4 to n initally
    for (int i = 4; i <= n; i++) {
        u[b[i]]++;
    }

    // Nested loops to calculate r
    for (int i = 1; i <= n; i++) {
        for (int j = i + 1; j <= n; j++) {
            for (int k = j + 1; k <= n - 1; k++) {   //to handke k+1 outof bound error take to n-1 only
                int d = -(b[i] + b[j] + b[k]);
                r += u[d];          // count frequency of d in the range [k+1, n]

                // Decrement frequency of b[k+1]
                u[b[k + 1]]--;
            }

            // Restore the counts of b[z] for future iterations
            for (int z = j + 3; z <= n; z++) { // for next interation j = j + 1, and k = j + 2 then l range = {j+3 , n}
                u[b[z]]++;
            }
        }
    }
    cout << r << endl;
    return 0;
}
```

## Optimal 2 : O(n^2)
<img width="633" height="152" alt="image" src="https://github.com/user-attachments/assets/2c33a266-7c51-43cf-90e0-a6220ce6690a" />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;
    
    vector<int> b(n + 1);
    unordered_map<int, int> y;
    
    // Input array b
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // First loop to count sums of pairs (k, l)
    for (int k = 3; k <= n; k++) {
        for (int l = k + 1; l <= n; l++) {
            y[b[k] + b[l]]++;
        }
    }

    long long r = 0;

    // Second loop to count results
    for (int j = 2; j <= n - 2; j++) {
        for (int i = 1; i < j; i++) {
            int d = b[i] + b[j];
            int u = -(b[i] + b[j]);
            r += y[u];  // count of (k, l) whose sum = u
        }

        for (int j1 = j + 2; j1 <= n; j1++) {  //when j = j + 1 => 3, we need to remove all the sum values which we tought k = 3 , l = {4,n}  
            y[b[j + 1] + b[j1]]--;
        }
    }

    cout << r << endl;
    
    return 0;
}

```

