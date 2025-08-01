# Problem
<img width="957" height="570" alt="image" src="https://github.com/user-attachments/assets/00268ba1-b0b2-43a4-b2f2-9e0baaf8e783" />
<img width="950" height="387" alt="image" src="https://github.com/user-attachments/assets/d1c4668a-0a60-43d4-baf6-7a896d67e3bb" />

# Brute Force
```
 class Solution {
   public:
     int countBalanced(vector<string>& arr) {
         vector<int> vol;
         vector<int> con;
         int n = arr.size();
        
         for(string w : arr){
             int v = 0,co = 0;
             for(char c : w){
                 if(c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u'){
                     v++;
                 }else co++;
             }
             vol.push_back(v);
             con.push_back(co);
         }
         int ct = 0;
         for(int i=0; i<n; i++){
             int v = 0, c = 0;
             for(int j=i; j<n;j++){
                 v += vol[j];
                 c += con[j];
                 if(v == c){
                     ct++;
                 }
             }
         }
         return ct;
     }
 };

```

# Optimal Code
```
#include <unordered_map>
#include <vector>
#include <string>
using namespace std;

class Solution {
public:
    int countBalanced(vector<string>& arr) {
        unordered_map<int, int> freq;
        freq[0] = 1;  // Base diff (v-c) = 0

        int result = 0;
        int diff = 0;

        for (string& word : arr) {
            int v = 0, c = 0;
            for (char ch : word) {
                if (isVowel(ch)) v++;
                else c++;
            }

            diff += (v - c);  //  Net change
            result += freq[diff]; // If diff seen before, we found balanced subarrays
            freq[diff]++;
        }
        return result;
    }

private:
    bool isVowel(char ch) {
        return ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u';
    }
};

```
