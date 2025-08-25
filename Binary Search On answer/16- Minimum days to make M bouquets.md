# PROBLEM
<img width="895" height="576" alt="image" src="https://github.com/user-attachments/assets/328faa29-13b2-418d-836f-9bdffc9d251e" />
<img width="914" height="693" alt="image" src="https://github.com/user-attachments/assets/b3d23280-9709-487b-82fa-d3afc1473f9c" />


# CODE
```
class Solution {
  public:
  
    bool possible(int mid,vector<int>&arr,int k,int m)
    {
        int count=0;
        int b=0;
        for(auto it:arr)
        {
            if(it<=mid)
            {
                count++;
            }
            else{
                b+=count/k;   //for every k days there ia flower blooms
                count=0;
            }
        }
        b+=(count/k);
        return (b>=m);
    }
  
    int minDaysBloom(vector<int>& arr, int k, int m) {
        // Code here
        int l = *min_element(arr.begin(),arr.end());
        int r = *max_element(arr.begin(),arr.end());
        int ans = -1;
        while(l<=r)
        {
            int mid=l+(r-l)/2;
            if(possible(mid,arr,k,m))
            {
                ans=mid;
                r=mid-1;
            }
            else{
                l=mid+1;
            }
        }
        return ans;
    }
};
```
