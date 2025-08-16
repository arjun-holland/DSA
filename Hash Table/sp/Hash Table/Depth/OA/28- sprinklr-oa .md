# Problem
<img width="298" height="500" alt="image" src="https://github.com/user-attachments/assets/50dc758f-41d1-4394-8c86-fa9f7ce0edf3" />

<img width="326" height="582" alt="image" src="https://github.com/user-attachments/assets/132cd1ac-53a1-4208-bfda-e22ee10ac14c" />

```


```

# Code
## Brute Force
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s;
    cin >> s;
    int n = s.length();

    int q;
    cin >> q;

    while(q--) {
        int l, r;
        cin >> l >> r;

        // frequency array for [l..r]
        vector<int> freq(26, 0);

        for(int i = l-1; i < r; i++) {
            freq[s[i] - 'a']++;
        }

        int ans = 0;
        for(int c = 0; c < 26; c++) {
            ans += (freq[c] * (freq[c] + 1)) / 2;
        }

        cout << ans << endl;
    }

    return 0;
}

```
<img width="675" height="199" alt="image" src="https://github.com/user-attachments/assets/90ed1881-a5f1-4d5d-a598-344954ce78d3" />

## OPtimal Code

<img width="948" height="378" alt="image" src="https://github.com/user-attachments/assets/26ff10c8-b3f8-41a4-a7a4-8929b1c67fc4" />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s;
    cin >> s;
    int n = s.length();
    
    // pref[i][c] = number of times character 'c' appears in s[0...i-1] 
    vector<vector<int>> pref(n+1, vector<int>(26,0));
    
    for(int i = 0; i < n; i++){
        int ci = s[i] - 'a';          // char index for current letter
        for(int j = 0; j < 26; j++){
           // carry forward previous counts and add 1 if current char matches
            pref[i+1][j] = pref[i][j] + (ci == j);
        }
    }
    
    int q;
    cin >> q;
    
    while(q--){
        int l, r;
        cin >> l >> r;
        
        int ans = 0;
        for(int c = 0; c < 26; c++){
            // frequency of char 'c' in substring [l, r]
            int freq = pref[r][c] - pref[l-1][c];

            // number of substrings from these freq letters = nC2 + singles
            ans += (freq * (freq + 1)) / 2;
        }
        cout << ans << endl;
    }
    
    return 0;
}

```

<img width="946" height="534" alt="image" src="https://github.com/user-attachments/assets/5f45681b-2b0b-427b-9b72-2e4df784b3ee" />
<img width="951" height="438" alt="image" src="https://github.com/user-attachments/assets/5381e554-6d5d-44dc-b1ef-fc95345d05bf" />

