# PROBLEM
<img width="942" height="419" alt="image" src="https://github.com/user-attachments/assets/da7ba7e7-058f-41fa-b76b-e9f1bfe890e2" />
<img width="857" height="789" alt="image" src="https://github.com/user-attachments/assets/713940a6-0013-4de5-9327-e6d49fe6362c" />
<img width="842" height="505" alt="image" src="https://github.com/user-attachments/assets/a75da2cb-199b-4734-8dd0-acf18fbb1896" />

# INTUITION
```
The question says that we need to check whether we can able to make exactly certain number of groups
such that each group contains unique values and those values are present in the given array and 
also given a value which is K and that K value tells that length of the array which we make

if given array size is 'n' and value is 'k' then
we need to make exactly 'n/k' groups such that each group containts exactly 'k' distant elements

so if (n % k != 0) then we cant make 'n/k' groups
otherwise
we need to say that each elemet can repeat exactly 'n/k' times
if an element repeat greater then 'n/k; times then return false

So now we just need to check the frequency of every element and
if you get a frequency of an element which is greater than 'N/K'
then we need to return false otherwise we need to return true
```


# CODE
```
class Solution {
public:
    bool partitionArray(vector<int>& nums, int k) {
        int n = nums.size();
        if(n % k != 0)return false;    // we need to create the n/k groups with size k exactly

        int nt = n/k;  //no.of times an elemet can repeat :  4/2=>2

        unordered_map<int,int> mp;
        for(int i=0;i<n;i++){
            mp[nums[i]]++;
        }
        for(auto [e,f] : mp){
            if(f > nt)return false;
        }
    
        return true;
    }
};
```
