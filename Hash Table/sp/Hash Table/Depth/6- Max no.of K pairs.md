# Problem
<img width="1020" height="762" alt="image" src="https://github.com/user-attachments/assets/d0f3011c-1ad6-4e47-b3ef-2d31c748aa4e" />
<img width="801" height="199" alt="image" src="https://github.com/user-attachments/assets/11cb56b4-1224-40cb-943a-e090f130bd0e" />

# Intuition
## Brute Force : O(n^2) 
```
for(int i -> n){
  for(int j = i+1 -> n){
    check all possible pairs which give the  `nums[i] + nums[j] = k` then increment ans
  }
}
```
## Optimal 1 : sorting -> TC : O(nlogn)
```
class Solution {
public:
    int maxOperations(vector<int>& nums, int k) {
        int op = 0;
        sort(nums.begin(),nums.end());

        int l=0,r=nums.size()-1;
        while(l < r){
            int vl = nums[l] + nums[r];
            if(vl == k){
                op++;
                l++;
                r--;
            }else if(vl > k){
                r--;
            }else {
                l++;
            }
        }

        return op;
    }
};
```

## Optimal 2 : Hashmap -> TC : O(n), SP : O(n)
```
class Solution {
public:
    int maxOperations(vector<int>& nums, int k) {
        unordered_map<int, int> freq;
        int op = 0;

        for (int x : nums) {
            int y = k - x;
            if (freq[y] > 0) {   // found a pair
                op++;
                freq[y]--;    // use one occurrence of y
            } else {
                freq[x]++;    // store x for future pairing
            }
        }
        return op;
    }
};
```
