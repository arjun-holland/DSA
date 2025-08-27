# PROBLEM
<img width="751" height="599" alt="image" src="https://github.com/user-attachments/assets/d0c4948d-8c61-40c6-9f0a-7b6cf6125ac9" />
<img width="757" height="533" alt="image" src="https://github.com/user-attachments/assets/10bb36c9-d0ec-4732-a3d6-525fc261924f" />

# INTUITION
```
Whenever we're at the i'th index we will consider that ith index as the 3rd side triangle and
we need to check indices from '0' to 'i-1' for two values such that addition of those two values will be greater than the ith value
if it is possible then we can make sure that we can the Y number of triangles with that which are possibly ending at the ith index
The reason for Y number of triangles is because we are choosing from the index 0 and i-1, let's say index
   i = 4 so (i-1) = 3 and we havea ranger from 0 to 3 when i = 4 the index
   if we can form triangle with index 0,3,4 then we can also form triangle with indices 1,3,4 and 2,3,4 as
   index 1,2 containts larger values then the index 0 ans we make the array as sorted array first
```

# CODE
```
class Solution {
  public:
    int countTriangles(vector<int>& arr) {
        sort(arr.begin(),arr.end()); //3 4 6 7 
        int ans = 0, n=arr.size();
        for(int i=n-1;i>=0;i--){
            int l=0,r=i-1;
            while(l < r){
                if(arr[l] + arr[r] > arr[i]){ //9 > 7
                    ans+= (r-l);  // iam having two traingles as r-l=>2-0=>2 such as 3 6 7, 4 6 7
                    r--;
                }else{
                    l++;
                }
            }            
        }
        return ans;
    }
};

```
