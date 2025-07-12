# Problem
Given a string s, find the longest palindromic subsequence's length in s.
A subsequence is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.


# Intuition
```
🧠 Intuition:
To find the longest palindromic subsequence:
Definition: A palindromic subsequence is a sequence that reads the same forward and backward, formed by deleting zero or more characters (not rearranging) from the original string.

Key Insight: The longest palindromic subsequence in a string s is the Longest Common Subsequence (LCS) between:
- The string s, and
- Its reverse s'.
Why? Because if a sequence is a palindrome, reading it from both ends gives the same result—so any common subsequence between s and reverse(s) that preserves order will be a palindromic subsequence.

```

# Code
```
class Solution {
public:
    int lcsHelper(string& s1, string& s2, int i, int j, vector<vector<int>>& dp) {
        if (i == s1.size() || j == s2.size()) return 0;

        if (dp[i][j] != -1) return dp[i][j];

        if (s1[i] == s2[j]) {         //char is same in both strings
            dp[i][j] = 1 + lcsHelper(s1, s2, i + 1, j + 1, dp);    //try shifting both the first and second string character to get next equal char 
        } else {
            dp[i][j] = max(lcsHelper(s1, s2, i + 1, j, dp),       //try shifting only the first string character 
                            lcsHelper(s1, s2, i, j + 1, dp));      //try shifting only the second string character 
        }
        return dp[i][j];
    }

    int LCS(string text1, string text2) {
        int n = text1.size(), m = text2.size();
        vector<vector<int>> dp(n, vector<int>(m, -1));
        return lcsHelper(text1, text2, 0, 0, dp);
    }

    int longestPalindromeSubseq(string s) {
        string rs = s;
        reverse(s.begin(),s.end());
        return LCS(s,rs);
    }
};
```
