# PROBLEM
<img width="731" height="277" alt="image" src="https://github.com/user-attachments/assets/c7ec22f3-ca55-4253-89de-2dc141be6312" />

---

# Easy Prob From Actual Prob:
<img width="751" height="96" alt="image" src="https://github.com/user-attachments/assets/fa238198-37f0-4966-9682-47d30fe9f15b" />

## INTUITION : Backward DP Trick on Strings
```
Backward DP Trick on Strings
When Ever we need to do DP on strings just think DP in backaward  
```

![WhatsApp Image 2025-09-13 at 00 31 37_74eefbe6](https://github.com/user-attachments/assets/c0e09954-725f-4fee-b918-b8bd4096bd4f)
![WhatsApp Image 2025-09-13 at 00 31 37_c36cfcd7](https://github.com/user-attachments/assets/b05dd6d2-97a5-4ab7-884c-b3481cea4a69)
![WhatsApp Image 2025-09-13 at 00 31 37_044805a9](https://github.com/user-attachments/assets/bb6220a3-958f-44f0-ac1e-699f2655027c)


## CODE
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;
#define pfo(i, end, start) for (ll i = end; i >= start; i--)

int main(){
    string a, b;
    cin >> a >> b; 
    ll n = a.size();
    
    ll dp[n+1]={0};
    ll j = 0;
    
    pfo(i,n-1,0){
        ll len = j;     //len = abs(n-i)-1;
        j++;
        if(a[i]>b[0]) {dp[i] = dp[i+1] + pow(2,len); }
        if(a[i]<b[0]) {dp[i] = dp[i+1]; }
        if(a[i]==b[0]) {dp[i] = dp[i+1] + pow(2,len)-1; }
    }
	cout<<dp[0]; 
}
```
---

# Actual Prob
<img width="928" height="247" alt="image" src="https://github.com/user-attachments/assets/9224f54a-30c8-454a-a28b-bf65f77b2e65" />

## INTUITION : Backward DP Trick on Strings
![WhatsApp Image 2025-09-13 at 00 31 38_8ab0ea31](https://github.com/user-attachments/assets/403ca770-7fd0-4590-952c-7bfdec01a27f)
![WhatsApp Image 2025-09-13 at 00 31 38_2e0cc74f](https://github.com/user-attachments/assets/cecec940-0ebc-4104-98a6-bc3c165a68d7)
![WhatsApp Image 2025-09-13 at 00 31 39_d974e834](https://github.com/user-attachments/assets/f84cf530-6308-4d11-8ff6-4e22b78a85dc)
![WhatsApp Image 2025-09-13 at 00 31 40_5829e8f6](https://github.com/user-attachments/assets/c273e903-97f8-44a6-8ec6-c44d6451f8ca)

`A[i] > B[j]`
![WhatsApp Image 2025-09-13 at 00 31 40_1fb88469](https://github.com/user-attachments/assets/0bb4f914-5027-4755-9910-310dec0865f9)
![WhatsApp Image 2025-09-13 at 00 31 40_e63d9305](https://github.com/user-attachments/assets/42957837-212c-494d-b5ee-98adc056cf78)
<img width="537" height="301" alt="image" src="https://github.com/user-attachments/assets/248dfd3f-7d62-40dc-b742-35a38abd335f" />

`A[i] < B[j]`
![WhatsApp Image 2025-09-13 at 00 31 41_4d70716a](https://github.com/user-attachments/assets/304cf34b-afd8-4249-950e-55c01bfdff88)
![WhatsApp Image 2025-09-13 at 00 31 41_43bb809d](https://github.com/user-attachments/assets/9307da27-d5c7-47b3-9d4d-3393d6f7ffe7)

`A[i] == B[j]`
![WhatsApp Image 2025-09-13 at 00 31 42_feea6af7](https://github.com/user-attachments/assets/93227549-e1c7-4cdd-8a13-41aa4cc48180)
![WhatsApp Image 2025-09-13 at 00 31 42_1adbd89f](https://github.com/user-attachments/assets/c4f8bdc9-3e41-4f5d-9c3b-6a8efe78de6e)

<img width="930" height="583" alt="image" src="https://github.com/user-attachments/assets/cb3b81f1-03cb-4dd3-b6d7-2fa9523c33e9" />


## CODE
```
#include <bits/stdc++.h>
using namespace std;

int dp[100][100];
int numberofsubsequence(string s1, string s2){
    int n = s1.size();
    int m = s2.size();

    // Base case: when s2 is exhausted, all non-empty subsequences of s1[i..] are valid
    for (int i = 0; i <= n; i++) {
        int len = n - i;
        dp[i][m] = pow(2, len) - 1;     // Could replace with fast power if needed
    }

    for(int i = n - 1; i >= 0; i--){
        for(int j = m - 1; j >= 0; j--){
            int size = (n - i) - 1;
            if(s1[i] > s2[j]){
                dp[i][j] = dp[i+1][j] + pow(2, size);
            }
            else if(s1[i] < s2[j]){
                dp[i][j] = dp[i+1][j];
            }
            else{
                dp[i][j] = dp[i+1][j] + dp[i+1][j+1];
            }
        }
    }

    return dp[0][0];
}

int main(){
    string s1, s2;
    cin >> s1 >> s2;
    cout << numberofsubsequence(s1, s2);
}
```

```
/*
INPUT : 
s1 = abcd
s2 = ab

OUTPUT:13
abc               
abd
abcd
ac
acd
ad
----------------
b
bc
bcd
bd
---------------
c
cd
---------------
d
*/
```

# Code Explanation 
<img width="904" height="205" alt="image" src="https://github.com/user-attachments/assets/aa55d822-31af-4692-bc77-4d3f18b62f19" />
<img width="734" height="678" alt="image" src="https://github.com/user-attachments/assets/e1212a01-b4cb-49cb-a0f8-e820cc784d87" />
<img width="671" height="296" alt="image" src="https://github.com/user-attachments/assets/1a36f2f5-f600-4dc4-a3b3-a863b7f0501d" />
<img width="814" height="521" alt="image" src="https://github.com/user-attachments/assets/3890c420-3e32-43fe-b806-97a38475e416" />
<img width="937" height="384" alt="image" src="https://github.com/user-attachments/assets/4b9f28e5-1a63-40fe-8ac4-15e05c534228" />
<img width="791" height="213" alt="image" src="https://github.com/user-attachments/assets/0fda7c4b-014f-4db2-9a5e-a6c65534e327" />
<img width="806" height="602" alt="image" src="https://github.com/user-attachments/assets/b4913394-91f7-48f2-97ab-943bfa6ff603" />
<img width="929" height="487" alt="image" src="https://github.com/user-attachments/assets/ddabb1f2-3be0-4ee2-b885-225283d0a715" />
<img width="731" height="850" alt="image" src="https://github.com/user-attachments/assets/30674d8c-194d-4dbe-9df3-2129931531b2" />
<img width="705" height="471" alt="image" src="https://github.com/user-attachments/assets/790f2a4e-cba2-4f86-ae27-3a5f0504cc45" />

| Expression        | Meaning                                            |
| ----------------- | -------------------------------------------------- |
| `len = n - i`     | Length of the remaining suffix of `s1`             |
| `pow(2, len)`     | Total number of subsequences (including empty)     |
| `pow(2, len) - 1` | Number of **non-empty** subsequences               |
| `dp[i][m]`        | Count of valid subsequences when `s2` is exhausted |


# RUN HERE:
https://ideone.com/m6bSu6
