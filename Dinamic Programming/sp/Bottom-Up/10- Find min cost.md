# PROBLEM
<img width="818" height="604" alt="image" src="https://github.com/user-attachments/assets/68680f9e-f1c1-4053-a57d-4214c971198e" />

# INTUITION
<img width="807" height="337" alt="image" src="https://github.com/user-attachments/assets/c09403df-1551-4606-bd15-5589b4a1c7b2" />
<img width="807" height="430" alt="image" src="https://github.com/user-attachments/assets/a7d0a8ea-1a41-4eb6-83db-ab0a07bdfea0" />

## Example
<img width="778" height="449" alt="image" src="https://github.com/user-attachments/assets/ae292df8-c30c-4892-b601-7c32ea0c5040" />
<img width="797" height="415" alt="image" src="https://github.com/user-attachments/assets/3937d399-828a-40a3-84b0-5d3360a22915" />
<img width="922" height="392" alt="image" src="https://github.com/user-attachments/assets/54ed2e9c-3c4c-476a-95c7-0257f7260698" />

---

<img width="791" height="406" alt="image" src="https://github.com/user-attachments/assets/9e768bd3-6acd-4a3d-b1a9-6b40217af43b" />
<img width="814" height="472" alt="image" src="https://github.com/user-attachments/assets/cb35540d-6519-4b07-923b-6fa684d59401" />
<img width="815" height="425" alt="image" src="https://github.com/user-attachments/assets/f21cc3cd-a6af-40b7-bb75-2d77f94fa601" />
<img width="818" height="423" alt="image" src="https://github.com/user-attachments/assets/9ded8493-4197-4ef0-bdc8-a2a8edf10663" />
<img width="805" height="429" alt="image" src="https://github.com/user-attachments/assets/b29c8c74-dd85-4ae1-a4aa-76ced5178988" />


# CODE
```
#include <bits/stdc++.h>
 
using namespace std;
typedef long long int ll;
 
int main() {
 
    int n; 
    cin>>n; 
    int y,x,z,b;
    cin>>y>>x>>z>>b;
 
    int dp[n+1]={0};
 
    dp[1] = 0 ; 
 
    int i = 2 ; 
    while(i<=n){
        int v1 = dp[i-1] + y ; 
        int v2 = 1e8;
        int v3 = 1e8;
        int v4 = 1e8;
        if(i%7==0){
            v2 = dp[i/7] + x; 
        }
        if(i%3==0){
            v3 = dp[i/3] + z;
        }
        if(i%5==0){
            v4 = dp[i/5] + b;
        }
 
        dp[i] = min(v1,min(v2,min(v3,v4)));
        i++;
    }
    cout<<dp[n];
    return 0 ; 
}
```
