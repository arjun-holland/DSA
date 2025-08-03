// ✅ LeetCode Problem 628: Maximum Number of Subsequences After One Inserting
 
---
// 🔗 Submission: https://leetcode.com/problems/maximum-number-of-subsequences-after-one-inserting/submissions/1716438576/
// Optimal SUbmission : https://leetcode.com/problems/maximum-number-of-subsequences-after-one-inserting/submissions/1721814952/

# Problem
<img width="1237" height="308" alt="image" src="https://github.com/user-attachments/assets/209a0c73-52bd-4aed-b37b-ab37ededd780" />
<img width="1241" height="878" alt="image" src="https://github.com/user-attachments/assets/2025e180-23b5-4061-94c0-4c9042ffb0f8" />
<img width="873" height="152" alt="image" src="https://github.com/user-attachments/assets/762eaa21-e060-407a-93e8-c7465a8d2437" />

# Intuition
```
 1️⃣ First Pass: Count how many "LCT" subsequences already exist
 2️⃣ Create prefix array LCcount[i]: number of "LC" pairs from start to index i
 3️⃣ Create suffix array CTcount[i]: number of "CT" pairs from index i to end
 4️⃣ Try all positions to insert one of L, C, or T and track max gain
      => to insert L at i check  CTcount[i] (suffixCT[i]) , => to insert T at i check LCcount[i] (prefixLC[i])
 5️⃣ Return original + best insertion gain
```

# Code
```
#define ll long long

class Solution {
public:
    long long numOfSubsequences(string s) {
        ll ans = 0;

        // These are counters for 'L', 'C', 'T' characters
        ll lC = 0, cC = 0, tC = 0;

        // uC = number of "LC" subsequences
        // uT = number of "LCT" subsequences formed so far
        ll uC = 0, uT = 0;

        // 1️⃣ First Pass: Count how many "LCT" subsequences already exist
        for (char c : s) {
            if (c == 'L') {
                lC++;  // Track number of L's seen so far
            } else if (c == 'C') {
                cC++;
                uC += lC;  // For every 'C', it can form "LC" with all previous 'L'
            } else if (c == 'T') {
                tC++;
                uT += uC;  // For every 'T', it can form "LCT" with all previous "LC" pairs
            }
        }

        ans = uT;  // Save the number of original "LCT" subsequences

        ll n = s.length();

        // 2️⃣ Create prefix array LCcount[i]: number of "LC" pairs from start to index i
        vector<ll> LCcount(n, 0);
        // 3️⃣ Create suffix array CTcount[i]: number of "CT" pairs from index i to end
        vector<ll> CTcount(n, 0);

        ll lC2 = 0, cC2 = 0, LC = 0;  // Helper variables to compute LCcount
        for (ll i = 0; i < n; i++) { // Left to Right → Prefix for LC
            char c = s[i];
            if (c == 'L') {
                lC2++;
            } else if (c == 'C') {
                cC2++;
                LC += lC2;  // For every 'C', pair with all previous 'L's
            }
            LCcount[i] = LC;
        }

        // Reset for CTcount
        cC2 = 0;
        ll tC2 = 0, CT = 0;
        for (ll i = n - 1; i >= 0; i--) {   // Right to Left ← Suffix for CT
            char c = s[i];
            if (c == 'T') {
                tC2++;
            } else if (c == 'C') {
                cC2++;
                CT += tC2;  // For every 'C', pair with all later 'T's
            }
            CTcount[i] = CT;
        }

        // 4️⃣ Try all positions to insert one of L, C, or T and track max gain
        ll inc = 0;
        lC2 = 0;
        cC2 = 0;

        // Note: tC2 is already last total count of 'T' from previous loop
        for (ll i = 0; i < n; i++) {
            ll c = s[i];

            // Maintain prefix counts of 'L' and 'C'
            if (c == 'L') lC2++;
            else if (c == 'C') cC2++;
            else if (c == 'T') tC2--;  // Reduce remaining 'T's

            // Try inserting 'C' at index i → adds lC2 * tC2 subsequences
            inc = max(inc, lC2 * tC2);

            // Try inserting 'L' before index i → pair with CT suffix
            inc = max(inc, CTcount[i]);

            // Try inserting 'T' after index i → pair with LC prefix
            inc = max(inc, LCcount[i]);
        }

        // 5️⃣ Return original + best insertion gain
        return ans + inc;
    }
};

```

# Optimla code
```
#define ll long long
class Solution {
public:
    long long numOfSubsequences(string s) {
        int n = s.length();
        vector<ll> preL(n,0),preLC(n,0);
        ll l=0,lc=0,ans=0;
        for(int i=0;i<n;i++){
            if(s[i] == 'L')l++;
            else if(s[i] == 'C')lc += l;
            else if(s[i] == 'T')ans += lc;
            preL[i] = l;
            preLC[i] = lc;
        }
        vector<ll> sufT(n,0),sufCT(n,0);
        int t=0,ct=0;
        for(int i=n-1;i>=0;i--){
            if(s[i] == 'T')t++;
            else if(s[i] == 'C')ct += t;
            sufT[i] = t;
            sufCT[i] = ct;
        }

        ll insertL = sufCT[0]+ans;
        ll insertT = preLC[n-1]+ans;
        ll insertC = 0;
        for(int i=0;i<n-1;i++){
            insertC = max(insertC,preL[i]*sufT[i+1]);
        }
        insertC += ans;
        return max({insertL,insertC,insertT});
    }
};
```
