# Problem
```
Given a string s, return the longest palindromic substring in s.

Example 1:
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.

Example 2:
Input: s = "cbbd"
Output: "bb"
 
Constraints:
1 <= s.length <= 1000
s consist of only digits and English letters.
```

# Intuition
```
Use 'Expand-Around-Center Method'
- When we are at the index 'i' (Takew that as a center) then go front and back from that 'i' until it satisfy the constraints.

```
# Get the substring in cpp 
## The Syntax : 
##       stringName.substr(start_index, length)
<img width="1464" height="1094" alt="image" src="https://github.com/user-attachments/assets/f0410ecc-ed3d-4f1e-a0d3-ae2cdb9d3007" />

# Code
```
class Solution {
public:
    string isPalindrome(string& s,int l,int r){    //Expand-Around-Center Method
        while(l >= 0 && r <= s.length() && s[l] == s[r]){
            l--;
            r++;
        }
        return s.substr(l+1,r-l-1);1        
    }
    string longestPalindrome(string s) { //O(n^2)
        if(s.length() <= 1) return s;
    
        int max_ans = 1;
        string ans = s.substr(0,1);
        
        for(int i=0; i < s.length(); i++){
            
            string oddSub = isPalindrome(s, i, i);
            string evenSub = isPalindrome(s, i, i+1);
            
            if(max_ans < oddSub.length()){
                ans = oddSub;
                max_ans = oddSub.length();
            }
            if(max_ans < evenSub.length()){
                ans = evenSub;
                max_ans = evenSub.length();
            }
        }
        return ans;
    }
};
```
