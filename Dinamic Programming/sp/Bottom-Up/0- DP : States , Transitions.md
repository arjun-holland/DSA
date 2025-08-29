<img width="1036" height="182" alt="image" src="https://github.com/user-attachments/assets/82b9a1e4-8b4c-48f5-a9f0-b599e36599f6" />
<img width="1079" height="543" alt="image" src="https://github.com/user-attachments/assets/e5fb8682-c8fa-43bf-a9d9-6ae436463f03" />
<img width="1054" height="752" alt="image" src="https://github.com/user-attachments/assets/49a29f84-bcad-45f2-bd37-9da76c1c61d4" />

<img width="1053" height="407" alt="image" src="https://github.com/user-attachments/assets/243e0c43-bef6-40c4-8fc8-6bdfd02c5b5b" />
<img width="1047" height="224" alt="image" src="https://github.com/user-attachments/assets/67a1d89a-a18b-4a3e-89f6-d25ccfa7fcb2" />

## EXAMPLE FOR 2D - DP
<img width="1074" height="548" alt="image" src="https://github.com/user-attachments/assets/0c959b05-d926-4934-8d23-39959edf9e62" />
<img width="1070" height="739" alt="image" src="https://github.com/user-attachments/assets/34b89e51-df4d-4673-b3ef-304491e3eb82" />
<img width="893" height="734" alt="image" src="https://github.com/user-attachments/assets/9f1c9a15-c7c9-4428-bbde-1a4b214032ff" />


<img width="790" height="192" alt="image" src="https://github.com/user-attachments/assets/aec4ed1b-6fca-4986-b6f1-3828d1250e5b" />




### CODE
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n+1), b(n+1);
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
    }
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // dp[i][0] = max EVEN sum ending at index i
    // dp[i][1] = max ODD  sum ending at index i
    vector<vector<long long>> dp(n+1, vector<long long>(2, -1e15));

    // Base case: index 1 can start either from a[1] or b[1]
    dp[1][a[1] % 2] = max(dp[1][a[1] % 2], 1LL * a[1]);
    dp[1][b[1] % 2] = max(dp[1][b[1] % 2], 1LL * b[1]);

    // Transition
    for (int i = 2; i <= n; i++) {
        // Try picking from a[i]
        if (a[i] % 2 == 0) {
            // even value -> parity stays same
            dp[i][0] = max(dp[i][0], dp[i-1][0] + a[i]);  //whay compare dp[i][0] that is current statent as we have to use the a[], b[] and gety the max one only 
            dp[i][1] = max(dp[i][1], dp[i-1][1] + a[i]);
        } else {
            // odd value -> parity flips
            dp[i][0] = max(dp[i][0], dp[i-1][1] + a[i]);
            dp[i][1] = max(dp[i][1], dp[i-1][0] + a[i]);
        }

        // Try picking from b[i]
        if (b[i] % 2 == 0) {
            dp[i][0] = max(dp[i][0], dp[i-1][0] + b[i]);
            dp[i][1] = max(dp[i][1], dp[i-1][1] + b[i]);
        } else {
            dp[i][0] = max(dp[i][0], dp[i-1][1] + b[i]);
            dp[i][1] = max(dp[i][1], dp[i-1][0] + b[i]);
        }
    }

    cout << "Max EVEN sum = " << dp[n][0] << endl;
    cout << "Max ODD sum  = " << dp[n][1] << endl;
}
```

## Example For 3D - DP
# PROBLEM
```
You are given two arrays a and b -> both are of size “N”. 
Start your journey at index 1 and end your journey at index “N”. 
In a move you can move from a[i]->a[i+1] or a[i]->b[i+1] 
OR  b[i]->b[i+1] or b[i]->a[i+1]
Output the number of journeys whose sum is even and odd.
Input -> 
A         B
1         3
2         1
1         1
Total 4 even journeys :- (1→2→1) 2 times; + (3→2→1) 2 times; = 4.
Similarly 4 odd journeys. 
```

# INTUITION

```
Here we have to use the 3D- DP, why
    the 1st dimentional -> to know the current index
    the 2nd dimentional -> to know the array from which we are taking the value
    the 3rd dimentional -> to know the parity(even / odd) of the element which we are taking from the array which is shown in 2nd dimentional
```

![WhatsApp Image 2025-08-29 at 14 26 38_a5515b31](https://github.com/user-attachments/assets/4ac71788-c897-4037-8cdf-44514714db40)



# CODE
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a[1000] = {0};
    int b[1000] = {0};
    
    int n; 
    cin >> n;

    // Input two arrays a[] and b[]
    for(int i=1; i<= n; i++){
        cin >> a[i];
    }
    
    for(int i=1; i<=n; i++){
        cin >> b[i];
    }
    
    // dp[i][array][parity]
    // i      = index (1..n)
    // array  = 1 means A[], 2 means B[]
    // parity = 1 means EVEN sum, 2 means ODD sum
    int dp[1000][3][3] = {0};  
    
    // ---------------- Base Case (i=1) ----------------
    // At index 1, you can only "start" from either a[1] or b[1].
    // Depending on whether that number is even or odd, we initialize the corresponding dp entry.

    // If a[1] is even -> one EVEN journey starting at a[1]
    // If a[1] is odd  -> one ODD journey starting at a[1]
    dp[1][1][1] = (a[1] % 2 == 0) ? 1 : 0;
    dp[1][1][2] = (a[1] % 2 != 0) ? 1 : 0;

    // Similarly for b[1]
    dp[1][2][1] = (b[1] % 2 == 0) ? 1 : 0;
    dp[1][2][2] = (b[1] % 2 != 0) ? 1 : 0;
    
    // ---------------- Transition ----------------
    // For each index i (2..n), we want to calculate
    //   dp[i][a][even], dp[i][a][odd], dp[i][b][even], dp[i][b][odd]
    //
    // You can reach a[i] or b[i] from *either* a[i-1] or b[i-1].
    //
    // Case 1: Current number is EVEN
    //   - Adding EVEN keeps parity the same
    //     so even+even=even, odd+even=odd
    //
    // Case 2: Current number is ODD
    //   - Adding ODD flips parity
    //     so even+odd=odd, odd+odd=even

    for(int i=2; i<=n; i++){

        // ---------------- For a[i] ----------------
        if(a[i] % 2 == 0){ 
            // If a[i] is EVEN:
            // even sum -> previous even + this even
            dp[i][1][1] = dp[i-1][1][1] + dp[i-1][2][1];
            // odd sum -> previous odd + this even
            dp[i][1][2] = dp[i-1][1][2] + dp[i-1][2][2];
        }else{ 
            // If a[i] is ODD:
            // odd sum -> previous even + this odd
            dp[i][1][2] = dp[i-1][1][1] + dp[i-1][2][1];
            // even sum -> previous odd + this odd
            dp[i][1][1] = dp[i-1][1][2] + dp[i-1][2][2];
        }

        // ---------------- For b[i] ----------------
        if(b[i] % 2 == 0){ 
            // If b[i] is EVEN:
            dp[i][2][1] = dp[i-1][1][1] + dp[i-1][2][1]; // even stays even
            dp[i][2][2] = dp[i-1][1][2] + dp[i-1][2][2]; // odd stays odd
        }else{ 
            // If b[i] is ODD:
            dp[i][2][1] = dp[i-1][1][2] + dp[i-1][2][2]; // odd+odd = even
            dp[i][2][2] = dp[i-1][1][1] + dp[i-1][2][1]; // even+odd = odd
        }
    }
    
    // ---------------- Answer ----------------
    // At the last index n, we can end at either a[n] or b[n].
    // So we add both counts for EVEN and both for ODD.

    cout << "EVEN ways: " << (dp[n][1][1] + dp[n][2][1]) << endl;
    cout << "ODD ways: "  << (dp[n][1][2] + dp[n][2][2]) << endl;
}
```

