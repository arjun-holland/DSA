# Problem 
<img width="1158" height="539" alt="image" src="https://github.com/user-attachments/assets/9531a3d8-053b-4c37-b81e-5f66beb604db" />
<img width="1045" height="568" alt="image" src="https://github.com/user-attachments/assets/e9f7c732-6081-4fe2-8ff8-c3dcf0c6eb5e" />
<img width="899" height="155" alt="image" src="https://github.com/user-attachments/assets/a4a49e5b-2131-4fee-8275-0ae18e3c98a8" />

# Code
```
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        unordered_map<int,int> mp;
        int i=0,j=0,s=0,n=fruits.size();
        int ans = 0;
        while(j < n){
            if(mp.find(fruits[j]) == mp.end())s++; //taking new fruit
            while(s > 2 && i < j){  //we have to reomve 1 fruit type
                mp[fruits[i]]--;
                if(mp[fruits[i]] == 0){
                    mp.erase(fruits[i]);
                    s--;
                }
                i++;
            }
            mp[fruits[j]]++;
            ans = max(ans, j-i+1);
            j++;
        }
        return ans;
    }
};
```
