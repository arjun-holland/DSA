# Problem
<img width="1066" height="566" alt="image" src="https://github.com/user-attachments/assets/152ac82a-7855-454e-af96-20924a388f45" />
<img width="997" height="505" alt="image" src="https://github.com/user-attachments/assets/7e15e4e1-9ee9-4e2c-9c1b-615fd41de6c0" />


# Intuition
```
Brute Force : Simply write 4-for loops to get the i,j,k and l indices whose values in nums1,nums2,nums3,nums4 repectively gives 0 O(n^4)
                        class Solution {
                        public:
                            int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
                                int ans = 0;
                                for(int i=0;i<nums1.size();i++){
                                    for(int j=0;j<nums2.size();j++){
                                        for(int k=0;k<nums3.size();k++){
                                            for(int l=0;l<nums4.size();l++){
                                                if(nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0)ans++;
                                            }
                                        }    
                                    }
                                }
                        
                                return ans;
                            }
                        };

Optimal : to reduce the one for loop we need to us the hashmap to check whether the remaining ele is present in that or not, O(n^3)

                                     nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0
                                                      |
                                                      |
                                      nums4[l] == 0 - (nums1[i] + nums2[j] + nums3[k])
                                     so now we need to check if the nums4 has resqired value or not
                                        which is one in O(1) with hashtable

                        class Solution {
                            public:
                                int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
                                    unordered_map<int,int> mp;

                                    for(int i = 0; i < nums4.size(); i++) {     // Store counts of elements from nums4
                                        mp[nums4[i]]++;
                                    }
                                    
                                    int ans = 0;
                                    for(int i = 0; i < nums1.size(); i++) {
                                        for(int j = 0; j < nums2.size(); j++) {
                                            for(int k = 0; k < nums3.size(); k++) {
                                                int rs = 0 - (nums1[i] + nums2[j] + nums3[k]);    
                                                if(mp.count(rs)) ans += mp[rs];      // add all occurrences
                                            }
                                        }
                                    }
                            
                                    return ans;
                                }
                            };

Very Optimal : break the equation in below form , O(n^2)
                                      nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0
                                                          |
                                                          |
                                     nums1[i] + nums2[j]  == 0 - (nums4[l] + nums3[k])
                            so now we need to check if the nums1 and nums2  has resqired value or not
                                             which is one in O(1) with hashtable


                            class Solution {
                            public:
                                int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
                                    unordered_map<int,int> mp;
                                    
                                    // Step 1: store all sums of nums1 and nums2
                                    for (int a : nums1) {
                                        for (int b : nums2) {
                                            mp[a + b]++;
                                        }
                                    }
                                    
                                    int ans = 0;
                                    
                                    // Step 2: check sums of nums3 and nums4
                                    for (int c : nums3) {
                                        for (int d : nums4) {
                                            int target = -(c + d);
                                            if (mp.count(target)) {
                                                ans += mp[target];
                                            }
                                        }
                                    }
                                    
                                    return ans;
                                }
                            };

```

# Run Code
https://leetcode.com/problems/4sum-ii/
