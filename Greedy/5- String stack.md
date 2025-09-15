# PROBLEM
<img width="923" height="613" alt="image" src="https://github.com/user-attachments/assets/aab674b6-4e33-46f2-aad9-222f826bdce9" />
<img width="917" height="543" alt="image" src="https://github.com/user-attachments/assets/2bb4d6a7-ed87-4d84-a893-4bcbed57ef20" />


# RECURSSION CODE : BRUTE FORCE
```
class Solution {
public:
    bool dfs(int i, string& pat, string& tar, string s) {
        // Base case: if we have processed all characters in pat
        if (i == pat.size()) {
            return s == tar;
        }

        bool res = false;

        // Option 1: Append pat[i] to the string
        s.push_back(pat[i]);
        res = dfs(i + 1, pat, tar, s);
        if (res) return true;

        // Option 2: Use pat[i] as a delete operation
        s.pop_back();  // Undo the append above
        if (!s.empty()) {
            char last = s.back();
            s.pop_back();  // Perform delete
            res = dfs(i + 1, pat, tar, s);
            // Backtrack: restore the character
            s.push_back(last);
        } else {
            // If string is empty, just move to next step
            res = dfs(i + 1, pat, tar, s);
        }
        return res;
    }

    bool stringStack(string &pat, string &tar) {
        string s = "";
        return dfs(0, pat, tar, s);
    }
};

```

# # RECURSSION + MEMOIZATION CODE : BRUTE FORCE 
```

class Solution {
public:
    // Memoization map: key = (index in pat, current length of string s)
    unordered_map<string, bool> memo;

    bool dfs(int i, string& pat, string& tar, string& s) {
        // Base case: processed all characters in pat
        if (i == pat.size()) {
            return s == tar;
        }

        // Key for memoization: index and current string
        string key = to_string(i) + "|" + s;
        if (memo.count(key)) return memo[key];

        bool res = false;

        // Option 1: Treat pat[i] as an append
        s.push_back(pat[i]);
        res = dfs(i + 1, pat, tar, s);
        s.pop_back();  // backtrack

        if (res) return memo[key] = true;

        // Option 2: Treat pat[i] as a delete operation
        char last = '\0';
        bool hasChar = false;
        if (!s.empty()) {
            hasChar = true;
            last = s.back();
            s.pop_back();
        }

        res = dfs(i + 1, pat, tar, s);

        // Backtrack
        if (hasChar) {
            s.push_back(last);
        }

        return memo[key] = res;
    }

    bool stringStack(string &pat, string &tar) {
        string s = "";
        memo.clear();
        return dfs(0, pat, tar, s);
    }
};
```

# OPTIMAL CODE 
```
class Solution {
public:
    bool stringStack(const string &pat, const string &tar) {
        int i = pat.size() - 1;
        int j = tar.size() - 1;
        
        while (i >= 0 && j >= 0) {
            if (pat[i] == tar[j]) {
                // Match: use this character
                i--;
                j--;
            } else {
                // Mismatch: simulate delete -> skip this char, plus skip one more (to remove last appended)
                i -= 2;
            }
        }
        
        // If we've matched all of tar
        return (j < 0);
    }
};
```
