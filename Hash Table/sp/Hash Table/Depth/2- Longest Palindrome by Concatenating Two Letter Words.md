# Problem
<img width="1138" height="237" alt="image" src="https://github.com/user-attachments/assets/59720492-996b-43d5-aeb0-2a969d52d77d" />

<img width="1158" height="611" alt="image" src="https://github.com/user-attachments/assets/cfba29bf-b090-48da-91e9-006345896e45" />

<img width="836" height="198" alt="image" src="https://github.com/user-attachments/assets/be215aed-c144-497c-b0bf-b6245fee3572" />

---
# Intuition

<img width="976" height="512" alt="image" src="https://github.com/user-attachments/assets/344e3bb0-f3ad-4e9a-93cf-f808c2a131cb" />

<img width="924" height="483" alt="image" src="https://github.com/user-attachments/assets/b835c813-5681-4f96-874d-7fb2700cd87a" />

---


# code
```
class Solution {
public:
    int longestPalindrome(vector<string>& words) {
        unordered_map<string, int> mp;
        int result = 0;

        for(string &word : words) {
            string reversedWord = word;
            swap(reversedWord[0], reversedWord[1]);

            if(mp[reversedWord] > 0) {
                result += 4;
                mp[reversedWord]--;
                if(mp[reversedWord] == 0)mp.erase(reversedWord);
            } else {
                mp[word]++;
            }
        }

        //Check equal character words. Use only one
        for(auto &it : mp) {
            string word = it.first;

            if(word[0] == word[1]) {
                result += 2;
                break;
            }
        }

        return result;
    }
};
```
