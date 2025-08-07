# Problem
<img width="1099" height="556" alt="image" src="https://github.com/user-attachments/assets/9c95184a-fdfa-42a5-ac56-910fd78b21d3" />
<img width="996" height="570" alt="image" src="https://github.com/user-attachments/assets/253d5633-bb20-41c5-b802-78e8a80ef1d4" />
<img width="816" height="151" alt="image" src="https://github.com/user-attachments/assets/953b1e89-2da8-4a91-9dac-47fbcd982757" />

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
