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

## Optimla 2 : two Hashing
```
class Solution {
public:
    int maxOperations(vector<int>& nums, int k) {  // [1 2 3 4] and k = 2
        unordered_map <int,int> kk,gg; 
        int i = 0 ; 
        int n = nums.size();
        while(i<n){
            kk[nums[i]]=kk[nums[i]]+1;
            i=i+1;
        }
        int answer = 0 ; 
        for(i=0;i<n;i++){
            int number = nums[i] ;    //1
            int partner = k - number ;   // 4
            if(gg[number]==0 && gg[partner]==0){
                if(number==partner){
                    int yy = kk[number];   // 1 1 1 1 , k = 2 
                    answer = answer + (yy/2);  // 4/2 => 2 pairs
                }
                else{
                    answer = answer + min(kk[number],kk[partner]);
                }
            }
            gg[number]=1;
            gg[partner]=1;
        }
        return answer ; 
    }
};
```

## Rune Here
https://leetcode.com/problems/max-number-of-k-sum-pairs/submissions/1736871626/
