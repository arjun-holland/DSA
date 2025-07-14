# Problem
<img width="1185" height="728" alt="image" src="https://github.com/user-attachments/assets/9ba2ca89-f2c0-422a-b65f-e6b532eba5ac" />
<img width="1064" height="175" alt="image" src="https://github.com/user-attachments/assets/ee91d180-1c72-4fa4-8ef8-229f1ed99d51" />

# Code
```
class Solution {
public:
    int matchPlayersAndTrainers(vector<int>& players, vector<int>& trainers) {
        int n = players.size();
        int m = trainers.size();
        sort(players.begin(),players.end());
        sort(trainers.begin(),trainers.end());
        int ans = 0;
        int i=0,j=0;
        while(i < n && j < m){
            if(players[i] <= trainers[j]){
                i++;
                j++;
                ans++;
            }else{
                j++;
            }
        }
        return ans;
    }
};
```
