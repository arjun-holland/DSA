# 📄 Problem Statement (K-Interspace Substring)
A string is said to be a k-interspace string if the absolute difference of the ASCII values of every pair of adjacent characters is at most k.
For example: "abac" is a 2-interspace string for k = 2 since the absolute difference between every adjacent character of it is at most 2.
A substring is any group of contiguous characters in a string. For example, the substrings of abc = [abc, ab, bc, a, b, c].
A substring of a string is said to be a k-interspace substring if the substring is a k-interspace string.

## ✅ Problem:
Given a string, word, and an integer, k, find the longest k-interspace substring within word.
If there are multiple substrings of the longest length, return the one that occurs first in word.

## 🧪 For Example:
word = wedding
k = 0
The first occurring longest 0-interspace substring is dd.

word = ababbacaabbbb
k = 1
There are two 1-interspace substrings of length 6: ababb a and aabbbb.
The one that occurs first is ababba.

## 🧠 Function Description:
Complete the function longestKInterspaceSubstring in the editor below.

longestKInterspaceSubstring has the following parameter(s):

string word: the string to analyze  
int k: maximum difference in character values

## Returns:  
string: the first occurring longest k-interspace substring of the word

## ✅ Constraints:
1 ≤ |word| ≤ 10⁶,
0 ≤ k ≤ 25,
Each character of word ∈ ascii[a-z]

## 📥 Input Format For Custom Testing:
The first line contains a string, word.
The second line contains an integer, k.


## 🧠 Intuition & Approach

We use **Dynamic Programming** to solve the problem efficiently in **O(n)** time.

### Key Idea:
Let `dp[i]` = length of the **longest valid substring ending at index `i`**.

- If the previous character `s[i-1]` and current character `s[i]` differ by ≤ `k`, then:
  ```
  if(abs(s[i-1]-s[i])<=k){
    -> dp[i] = 1 + dp[i-1]  //increment the length
  }else{
    -> dp[i] = 1   //length not incremented, it reset to 1
  }
  ```

- result =  Max(dp[1],dp[2],dp[3],..................dp[n]) because we longest string may eng at any index

Final Answer:
Track the maximum value in dp[] → this is the length of the longest valid substring.

Then go backward to find where it ends, and extract the substring using:
start_index = max_index - max_len + 1;

# 🧪 Example
Input:
n = 8
k = 1
s = abccbdde
Explanation:
- "bccb" is valid (c-b = 1, c-c = 0, b-c = 1)
- "dde" is valid too
- "bccb" appears first, and has a max length 4 ✅
Output:
bccb

# ✅ C++ Code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, k;
    cin >> n >> k;       // Read length of string and max allowed diff
    string s;
    cin >> s;

    vector<int> dp(n, 1);  // dp[i] = length of valid substring ending at i
    //initially dp[0] = s[0] is only one char i.e valid sunstring

    int max_len = 1;  //initial valid substring
    int max_index = 0;  //initial valid substring start index

    for (int i = 1; i < n; i++) {
        if (abs(s[i] - s[i - 1]) <= k) {
            dp[i] = dp[i - 1] + 1;
        } else {
            dp[i] = 1;
        }

        if (dp[i] > max_len) {
            max_len = dp[i];
            max_index = i;
        }
    }

    int start_index = max_index - max_len + 1;
    cout << s.substr(start_index, max_len) << endl;

    return 0;
}
```
