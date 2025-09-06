# PROBLEM
<img width="694" height="216" alt="image" src="https://github.com/user-attachments/assets/65720b5c-e525-441d-a7f6-07edeb422328" />

# BRUTE INTUITION
<img width="700" height="299" alt="image" src="https://github.com/user-attachments/assets/90fd7298-c6ad-480a-9778-521126cac8eb" />
## BRUTE FORCE CODE
```
function countValidSubstrings(s):
    n = length(s)
    totalCount = 0

    for i from 0 to n-1:
        # frequency counters for each character
        fa = fb = fc = fd = fu = ft = 0  

        for j from i to n-1:
            # update frequency of current character
            if s[j] == 'a': fa += 1
            if s[j] == 'b': fb += 1
            if s[j] == 'c': fc += 1
            if s[j] == 'd': fd += 1
            if s[j] == 'u': fu += 1
            if s[j] == 't': ft += 1

            # check validity of substring s[i…j]
            if (fa == fb) and (fc == fd) and (fu == ft):
                totalCount += 1
    return totalCount
```

# OPTIMAL CODE INTUITION : Use prefix-difference hashing technique

`Lets us take the problem is find count of subarrays such that freq(a) = freq(b) where array contains only a,b`

`Take the subarray i--j is valid, that means the freq(a) = freq(b)`
![WhatsApp Image 2025-09-06 at 06 46 02_36be22f7](https://github.com/user-attachments/assets/9e8d1cdb-3dc0-412b-b33f-75be656aa06f)

```M1athimatically the freq(a)[i--j] = freqA(j) - freqA(i-1)
                       freq(b)[i--j] = freqB(j) - freqB(i-1)
              we have , freq(a) = freq(b)
          freqA(j) - freqA(i-1) = freqB(j) - freqB(i-1)
          freqA(j) - freqB(j) = freqA(i-1) - freqB(i-1)  [place the commen terms on one side]
          the above equation says that
              freqA() - freqB() at j'th index = freqA() - freqB() at (i-1)'th index
``` 

![WhatsApp Image 2025-09-06 at 06 46 02_6d7846ca](https://github.com/user-attachments/assets/91b8f653-38cd-4927-97d5-35c6e754f50f)
![WhatsApp Image 2025-09-06 at 06 46 02_55d29ae2](https://github.com/user-attachments/assets/ce718fd9-3e25-44cd-92a0-ff947889e556)

# CODE 1
```
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of substrings (prefix-based) 
// where freq(a)=freq(b), freq(c)=freq(d), and freq(u)=freq(t)
int solve(string s) {
    // Map to store frequency differences as key and count as value
    map<tuple<int,int,int>,int> mp;

    // Initial state: frequency differences are zero
    mp[{0,0,0}] = 1;

    int ans = 0;

    // Frequency counters for the characters of interest
    int fa = 0, fb = 0, fc = 0, fd = 0, fu = 0, ft = 0;

    // Iterate over the string to build prefix frequency differences
    for(int i = 0; i < s.size(); i++) {
        // Update frequency counts based on the current character
        if(s[i] == 'a') fa++;
        else if(s[i] == 'b') fb++;
        else if(s[i] == 'c') fc++;
        else if(s[i] == 'd') fd++;
        else if(s[i] == 'u') fu++;
        else if(s[i] == 't') ft++;

        // Calculate the differences: these represent our "state"
        int d1 = fa - fb; // balance between 'a' and 'b'
        int d2 = fc - fd; // balance between 'c' and 'd'
        int d3 = fu - ft; // balance between 'u' and 't'

        // Pack differences into a tuple to use as a map key
        tuple<int,int,int> p = make_tuple(d1, d2, d3);

        // Add the number of previous times this state occurred
        // If the same state has been seen before, all substrings 
        // between that earlier index and current one are valid
        ans += mp[p];

        // Record that we've seen this state one more time
        mp[p]++;
    }

    return ans;
}

int main() {
    string s;
    cin >> s; // Read input string

    cout << solve(s); // Output the answer
    return 0;
}
```

# CODE 2
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    string s;
    cin >> s;

    unordered_map<string, ll> freq;

    int fa = 0, fb = 0, fc = 0, fd = 0, fu = 0, ft = 0;
    ll ans = 0;

    // Initial state
    freq["0#0#0"] = 1;

    for (char ch : s) {
        if (ch == 'a') fa++;
        else if (ch == 'b') fb++;
        else if (ch == 'c') fc++;
        else if (ch == 'd') fd++;
        else if (ch == 'u') fu++;
        else if (ch == 't') ft++;

        int d1 = fb - fa;
        int d2 = fd - fc;
        int d3 = ft - fu;

        string key = to_string(d1) + "#" + to_string(d2) + "#" + to_string(d3);

        ans += freq[key];
        freq[key]++;
    }

    cout << ans << "\n";
    return 0;
}

```

# CODE 3
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

// custom key for 3 integers
struct Key {
    int x1, x2, x3;
    bool operator==(const Key &other) const {   //for key in map required == operator as it checks the cur ele is is present in map with it
        return x1==other.x1 && x2==other.x2 && x3==other.x3;
    }
};

// custom hash function
struct KeyHash {
    size_t operator()(const Key &k) const {  // combine three ints into one hash
        return ((size_t)k.x1 * 1315423911u) ^ ((size_t)k.x2 * 2654435761u) ^ ((size_t)k.x3 * 104395301u);
    }
};

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    string s;
    cin >> s;
    int n = s.size();

    unordered_map<Key, ll, KeyHash> freq;

    int fa=0, fb=0, fc=0, fd=0, fu=0, ft=0;
    ll ans = 0;

    // initial state (before string starts)
    freq[{0,0,0}] = 1;

    for (int j=0; j<n; j++) {
        char ch = s[j];
        if (ch=='a') fa++;
        else if (ch=='b') fb++;
        else if (ch=='c') fc++;
        else if (ch=='d') fd++;
        else if (ch=='u') fu++;
        else if (ch=='t') ft++;

        int x1 = fb - fa;
        int x2 = fd - fc;
        int x3 = ft - fu;

        Key key = {x1, x2, x3};

        ans += freq[key];   // count valid substrings ending at j
        freq[key]++;        // update frequency
    }

    cout << ans << "\n";
    return 0;
}
```
# 🔍 COMPARISON TABLE of above three codes
| Feature                        | ✅ Code 1 (Map + `tuple`)   | ⚡ Code 2 (`unordered_map<string>`) | 🚀 Code 3 (`unordered_map<Key, custom_hash>`) |
| ------------------------------ | -------------------------- | ---------------------------------- | --------------------------------------------- |
| **Map type**                   | `map<tuple>` (ordered)     | `unordered_map<string>` (hash)     | `unordered_map<Key, ..., KeyHash>` (fastest)  |
| **Time Complexity (avg)**      | `O(log N)` per access      | `O(1)` avg (string hash)           | `O(1)` avg (custom hash)                      |
| **Space usage**                | Moderate                   | High (strings use more memory)     | Low (just integers)                           |
| **Ease of coding**             | Easiest (no custom struct) | Easy (string operations only)      | Hardest (requires `struct` and hash function) |
| **Hash collisions**            | ❌ Not applicable           | ⚠️ Possible (poor string hashing)  | ✅ Low (well-mixed custom hash)                |
| **Speed (practical)**          | 🐢 Slowest                 | 🐇 Faster than map                 | 🚀 Fastest (if hash well distributed)         |
| **Portability (C++ versions)** | ✅ C++11+                   | ✅ C++11+                           | ✅ C++11+                                      |
| **Flexibility**                | ✅ Very                     | ⚠️ Hard to extend beyond 3 keys    | ✅ Easy to extend (add `x4`, `x5`...)          |
