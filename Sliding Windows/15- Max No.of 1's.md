# PROBLEM
<img width="892" height="882" alt="image" src="https://github.com/user-attachments/assets/403c16b6-8031-4c25-b416-fb4abdf0e95d" />

# CODE
```
class Solution {
  public:
    int maxOnes(vector<int>& arr, int k) {
        int res = 0;
        int i=0,l=0,r=arr.size();
        int oneCount = 0, zeroCount = 0;
        while(l<r){
            if(arr[l] == 0){
                zeroCount++;
            }else{
                oneCount++;
            }
            
            while(i <= l && zeroCount > k){
                if(arr[i] == 0){
                    zeroCount--;
                }else{
                    oneCount--;
                }
                i++;
            }
            res = max(res, oneCount + zeroCount);
            l++;
        }
        return res;
    }
};
```
