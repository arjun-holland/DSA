# Problem
<img width="760" height="538" alt="image" src="https://github.com/user-attachments/assets/0fc1e605-e8a6-40f4-8a2b-512972a9061a" />

# Intuition
<img width="823" height="238" alt="image" src="https://github.com/user-attachments/assets/5702886a-c34f-4708-8e25-043fcb13f05a" />

## Brute Force => TC : O(N^2) , SC : O(1) 

```
-> n. 
-> b[n+1]-->
 
count = 0 
for(i=1; i<=n; i++){
	for(j=i+1; j<=n; j++){
 
		if((b[i]+b[j])%k==0){
			count = count + 1 
		}
 
	}
}
``` 

## Optimal => TC : O(N) SC : O(min(n,k))
<img width="744" height="428" alt="image" src="https://github.com/user-attachments/assets/2084c469-83c5-4b61-b800-1475a9f07d6d" />

` (a + b) % k => ((a % k) + (b % k)) % k `

`Take k = 3 => 13 % 3 => 1 `

<img width="733" height="363" alt="image" src="https://github.com/user-attachments/assets/b03cbb24-e79b-40d0-9c86-49e9f0b097ce" />

`if (b % k) => 1 then (a % k) should be 2 then only its is divisible by 3 `

<img width="698" height="362" alt="image" src="https://github.com/user-attachments/assets/c7579c48-3003-4d2a-920f-357dbd423338" />
<img width="705" height="423" alt="image" src="https://github.com/user-attachments/assets/1b642014-939c-4059-b73d-8094bf7c6de7" />
<img width="739" height="282" alt="image" src="https://github.com/user-attachments/assets/f45f15a0-6183-4b09-a868-ac7e90edae53" />
<img width="728" height="380" alt="image" src="https://github.com/user-attachments/assets/0b990a12-f96a-4810-bd05-19b8a0e9cf16" />
<img width="746" height="372" alt="image" src="https://github.com/user-attachments/assets/36849f99-6ed6-4bd7-81be-167437fdf3bd" />

```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll; 
 
int main() {
    ll n; cin>>n;
    ll k; cin>>k;

    unordered_map <ll,ll> mp;
    ll sum = 0 ; 
    for(ll i=1;i<=n;i++){
        ll yy;
        cin >> yy;
 
        ll g = k - (yy % k) ;
        g = g % k;  //for safe side 
        sum = sum + mp[g];
        mp[yy % k] = mp[yy % k] + 1;  //store the : remainder - increment value
    }
    cout<<sum;
    return 0;
}
```

## RUN HERE
https://ideone.com/Nsg1Ur
