# Problem
<img width="736" height="958" alt="image" src="https://github.com/user-attachments/assets/5a2f7edd-afd0-413d-9c51-1af4ae166205" />
<img width="734" height="755" alt="image" src="https://github.com/user-attachments/assets/7acbf4b4-93bd-4604-b23e-c775df398dc5" />

# Intuition
<img width="1182" height="604" alt="image" src="https://github.com/user-attachments/assets/d82c9bf0-d49f-49b4-8780-ca00efe9dd94" />
<img width="959" height="655" alt="image" src="https://github.com/user-attachments/assets/cafd9ab0-eb66-4e21-8382-a3113bf004fc" />
<img width="1128" height="480" alt="image" src="https://github.com/user-attachments/assets/8a7edf51-c2b1-439f-b994-08b71acc6304" />



<img width="1135" height="394" alt="image" src="https://github.com/user-attachments/assets/609fae86-2662-4ce8-a77f-41ae4a55dcf2" />
<img width="1140" height="722" alt="image" src="https://github.com/user-attachments/assets/a21ad8ef-55d7-406e-9d93-aeb7c7e897a9" />

✅ Correct Behavior:
| `s`      | `t`    | Explanation                       | Output |
| -------- | ------ | --------------------------------- | ------ |
| "a"      | "aa"   | Need 2 'a's, only 1 available     | `0`    |
| "aabbcc" | "abc"  | One of each in `t`, enough in `s` | `2`    |
| "abcabc" | "aabb" | Need 2 'a', 2 'b', have 2 each    | `1`    |



# Code
```
#include <bits/stdc++.h>
using namespace std;
#define ll long long
 
int main() {
 
    string s, t; 
    cin >> s >> t;
 
    unordered_map<char, ll> mp1, mp2;  // for s & t
 
    for(int i=0; i<s.size(); i++) mp1[s[i]]++;
    for(int i=0; i<t.size(); i++) mp2[t[i]]++; 

    ll cnt=1e9; 
 
    for(int i=0; i<t.size(); i++) 
    {
        if(mp1.find(t[i])==mp1.end()) 
        {
            // it means t[i] is not present in s hence we will not get any subset 
            return 0; 
        }
        ll val =  mp1[t[i]]/mp2[t[i]];
        cnt = min(cnt, val); 
    }
    cout<<cnt<<" ";
    return 0;
}
```
