# Problem
<img width="921" height="533" alt="image" src="https://github.com/user-attachments/assets/46f8f193-f619-4fed-ab8d-745d9602ceb1" />
<img width="967" height="713" alt="image" src="https://github.com/user-attachments/assets/71b60eb7-b3bd-4811-98c9-627e9fc73230" />
<img width="798" height="173" alt="image" src="https://github.com/user-attachments/assets/a65191a0-5b4b-4406-a277-5c217e6c9fdd" />


# Code
```
class Solution {
public:
    int numOfUnplacedFruits(vector<int>& fruits, vector<int>& baskets) {
        int ans = 0;
        for(int j=0;j<fruits.size();j++){
            int ft = fruits[j];
            bool v = true;
            for(int i=0;i<baskets.size();i++){
                if(ft <= baskets[i]){
                    baskets[i] = 0;
                    v = false;
                    break;
                }
            }
            if(!v)fruits[j] = 0;
            else ans++;
        }
        return ans;
    }
};
```
