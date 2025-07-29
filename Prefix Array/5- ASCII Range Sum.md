# Problem
<img width="903" height="881" alt="image" src="https://github.com/user-attachments/assets/5251f064-7377-4854-bf8b-886c95822374" />

# Intuition
```
As we require the sum in a range : use the prefx sum to reducxe the time complexity
```

# Code
```
class Solution {
  public:
    vector<int> asciirange(string& s) {
        vector<pair<int,int>> ans(26,{-1,-1});
        int n = s.length();
        
        for(int i=0;i<n;i++){
            int ci = s[i] - 'a';
            if(ans[ci].first == -1){        
                ans[ci].first = i;
            }else{
                ans[ci].second = i;  
            } 
        }
        vector<int> pr(n,0);
        pr[0] = (int)s[0];
        for(int i=1;i<n;i++){
            pr[i] = pr[i-1]+(int)s[i];
        }
        
        vector<int> res;
        for(int i=0;i<26;i++){
            int f = ans[i].first;
            int se = ans[i].second;
            //se > f + 1) : There is at least one character between f and se.
            if(f != -1 && se != -1 && se > f + 1){
                int cs = pr[se] - pr[f] - (int)s[se];   //exclute the f , se indices
                res.push_back(cs);
            }
        }
        
        return res;
    }
};

```

**Problem Link:** [ASCII Range Sum](https://www.geeksforgeeks.org/problems/ascii-range-sum/1)

**Approach:**
- Track first and last occurrence of each character.
- Use prefix sums to calculate ASCII sum between those indices.

**Time Complexity:** O(n + 26)
