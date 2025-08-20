# PROBLEM
<img width="1472" height="847" alt="image" src="https://github.com/user-attachments/assets/f86d4a40-cc37-4ca8-a96f-5f719e8b027e" />
<img width="1368" height="498" alt="image" src="https://github.com/user-attachments/assets/9f354cdb-4d65-44e6-82d9-606cfcc1714d" />
<img width="1263" height="440" alt="image" src="https://github.com/user-attachments/assets/20185c64-2ce4-411e-bcc2-9dc76427aa26" />


# INTUITION

```
Greedy vs DP :-> 

-> If a problem can be solved by the Greedy approach ; it means it is guaranteed ;
   that at each step ; you make a choice and that choice is the best possible for now as well as the future.
   Then you can solve this problem using the Greedy Method.

-> If there are multiple choices at each step and it is not clear which choice can given you
   the better answer long term -> use DP 
```

```
Easier version of the Question :-> You are given three arrays a ; b ; c ->
at each index you either select a[i] or b[i] or c[i] ; once you are done selecting n elements
we want the sum of all elements to be maximum.

******** Intuition *******
WE NEED TO PICK ONLY THE MAX VALUE AMONG a[i], b[i] and c[i]
-->n
-->a[n+1], b[n+1], c[n+1]

sum = 0 
i = 1
while(i <= n){
    sum = sum + max(a[i],max(b[i],c[i]))
    i=i+1   
}
print(sum)
TC :- O(N)
```

```
The current problem is 
HARD Version -> You cannot select a number from a particular array for more than 1 time consecutively
-> You have to find the maximum sum of all the numbers -> can only be solved by DP
-> because there are multiple choice and any choice you has not guarantee if the future will be great or final answer will be maximum.

******** Intuition **********
-> 3 arrays a, b, c - hence we create 3 dp arrays dpa[] dpb[] dpc[]

dpa[i] = best answer to the question if size of the array was ‘i’ and you selected a[i] at the ith index. 
dpb[i] = best answer to the question if size of array is i and selected b[i] at index i
dpc[i] = best answer to the question if size of array is i and selected c[i] at index i 

-> dpa[3] = a[3] + max(dpb[2],dpc[2]) 
Generalize ; substitute.-> i 

dpa[i] = a[i] + max(dpb[i-1],dpc[i-1])  //need to take the max value of previous b[],c[] arrays if we want to take the current value from a[]
dpb[i] = b[i] + max(dpc[i-1],dpa[i-1])
dpc[i] = c[i] + max(dpb[i-1],dpa[i-1])

Put these in a for loop and your job is done. 
TC :- O(N).. 
SC:- O(N)...... 
```
 
# CODE 1
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll ; 

int main() {
    ll n ; cin >> n ; 
    ll a[n+1],b[n+1],c[n+1];
    
    ll i = 1 ; 
    while(i<=n){
        cin>>a[i]>>b[i]>>c[i]; 
        i++;
    }
    
    ll dpa[n+1]={0};
    ll dpb[n+1]={0};
    ll dpc[n+1]={0};
    
    dpa[1] = a[1];
    dpb[1] = b[1];
    dpc[1] = c[1];
    
    i = 2 ; 
    while(i<=n){
        dpa[i] = a[i] + max(dpb[i-1],dpc[i-1]);
        dpb[i] = b[i] + max(dpa[i-1],dpc[i-1]);
        dpc[i] = c[i] + max(dpa[i-1],dpb[i-1]);
        i++;
    }
    cout<<max(dpa[n],max(dpb[n],dpc[n]));
    return 0 ; 
}
```

# CODE 2

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    vector<int> a(n+1), b(n+1), c(n+1);
    for (int i = 1; i <= n; i++) {
        cin >> a[i] >> b[i] >> c[i];
    }

    // dp[i][0] -> choose A on day i
    // dp[i][1] -> choose B on day i
    // dp[i][2] -> choose C on day i
    vector<vector<long long>> dp(n+1, vector<long long>(3, 0));

    // Base case
    dp[1][0] = a[1];
    dp[1][1] = b[1];
    dp[1][2] = c[1];

    // Fill dp
    for (int i = 2; i <= n; i++) {
        dp[i][0] = a[i] + max(dp[i-1][1], dp[i-1][2]); // Swim
        dp[i][1] = b[i] + max(dp[i-1][0], dp[i-1][2]); // Bugs
        dp[i][2] = c[i] + max(dp[i-1][0], dp[i-1][1]); // Homework
    }

    long long ans = max({dp[n][0], dp[n][1], dp[n][2]});
    cout << ans << endl;
    return 0;
}
```

---

# NEW PROBLEM 1 (Hard)

```
New Question.-> Same as above ; but you are allowed to take a maximum of only 2 consecutive numbers ;
not more than that->(3 numbers should not be consecutive.)

-> 2 consecutive are allowed; 
-> 3 consecutive are not allowed; 

```

# Intuition

```
-> dpa[1] = a[1] dpb[1] = b[1] dpc[1] = c[1] 

-> dpa[2] = a[2] + max(a[1],b[1],c[1]) 
-> dpb[2] = b[2] + max(a[1],b[1],c[1])
-> dpc[2] = c[2] + max(a[1],b[1],c[1])

-> dpa[3] = a[3] + max(dpb[2],dpc[2]) -> first 
               = OR a[3] + a[2] + max(dpb[1],dpc[1]) 

-> dpb[i] = max(b[i] + max(dpa[i-1],dpc[i-1]),
                b[i] + b[i-1] +max(dpa[i-2],dpc[i-2]))  //considering the adaject element taken only 1 time 

```

# Code
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main() {
    int n;
    cin >> n;
    vector<ll> a(n), b(n), c(n);
    for (int i = 0; i < n; i++) cin >> a[i] >> b[i] >> c[i];

    vector<ll> dpa(n, 0), dpb(n, 0), dpc(n, 0);

    dpa[0] = a[0];
    dpb[0] = b[0];
    dpc[0] = c[0];

    if (n > 1) {
        dpa[1] = a[1] + max({a[0], b[0], c[0]});
        dpb[1] = b[1] + max({a[0], b[0], c[0]});
        dpc[1] = c[1] + max({a[0], b[0], c[0]});
    }

    for (int i = 2; i < n; i++) {
        dpa[i] = max(a[i] + max(dpb[i - 1], dpc[i - 1]),  a[i] + a[i - 1] + max(dpb[i - 2], dpc[i - 2]));
        dpb[i] = max(b[i] + max(dpa[i - 1], dpc[i - 1]),  b[i] + b[i - 1] + max(dpa[i - 2], dpc[i - 2]));
        dpc[i] = max(c[i] + max(dpa[i - 1], dpb[i - 1]),  c[i] + c[i - 1] + max(dpa[i - 2], dpb[i - 2]));
    }

    cout << max({dpa[n - 1], dpb[n - 1], dpc[n - 1]}) << endl;
    return 0;
}

```



