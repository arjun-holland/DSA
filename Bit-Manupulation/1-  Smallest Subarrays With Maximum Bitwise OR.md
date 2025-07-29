# Problem
<img width="988" height="554" alt="image" src="https://github.com/user-attachments/assets/2beafc6e-741b-42e4-8018-fa5bff4009cd" />
<img width="999" height="792" alt="image" src="https://github.com/user-attachments/assets/b3fbbb2c-a5fb-41ff-bf5e-fc4ccdaa791f" />
<img width="917" height="211" alt="image" src="https://github.com/user-attachments/assets/8f15c65d-30e5-4070-9e49-3b03acda2b00" />

---

# Brute Force - Intuition
<img width="1100" height="164" alt="image" src="https://github.com/user-attachments/assets/177d84be-fd27-4a21-b7da-01353bc6e27b" />
<img width="745" height="285" alt="image" src="https://github.com/user-attachments/assets/bdf6bf64-6bfd-46b4-9a49-e4376d7654f8" />
<img width="934" height="240" alt="image" src="https://github.com/user-attachments/assets/fb16bef2-4c86-42da-a4a7-60a636020c70" />
<img width="1144" height="297" alt="image" src="https://github.com/user-attachments/assets/06b91d62-1343-46c7-ae34-ef1987c5c6b4" />

```
Observation:
      We need to calcuate the bitwise OR from i to n-1
            arr : x y x z m --- n
            ind : 0 1 2 3 4 ----n-1
      if i = 0 then we need bitwise OR from [0 to n-1]
      if i = 1 then we need bitwise OR from [1 to n-1]
      |
      |
      if i = n-1 then we need bitwise OR from [n-1 to n-1]
      The Above pattern can be solved in Suffix array technique

      Index      :  0     1     2     3     4
      nums[i]    : [ x  |  y  |  x  |  z  |  m ]
      
      suffixOR[] : [x|y|x|z|m,
                       y|x|z|m,
                            x|z|m,
                                z|m,
                                   m]

```
<img width="1169" height="625" alt="image" src="https://github.com/user-attachments/assets/c114c44a-520c-4978-9062-7f0cc4573278" />
write a loop to find the maxOR for i'th index which is equal to the suffixMaxOR[i] 

---

# Brute Force - Code
```
class Solution {
public:
    vector<int> smallestSubarrays(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n);

        vector<int> suffixOR(n);       // We'll compute OR from right to left
        suffixOR[n - 1] = nums[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            suffixOR[i] = suffixOR[i + 1] | nums[i];
        }

        for (int i = 0; i < n; i++) {
            int currOR = 0;
            for (int j = i; j < n; j++) {
                currOR |= nums[j];
                if (currOR == suffixOR[i]) {
                    ans[i] = j - i + 1;
                    break;
                }
            }
        }
        return ans;
    }
};
Time Complexity : O(n^2)
```

# Problem in Brute Force
<img width="702" height="185" alt="image" src="https://github.com/user-attachments/assets/b4dd8ef1-3676-4fec-a5e6-b05e43cc31cf" />

# Optimized - Intuition
<img width="1163" height="260" alt="image" src="https://github.com/user-attachments/assets/334ba761-d747-46e9-9ab4-40c8aecbff8c" />

```
Importand Insights:

    For array index is start from left to right:
             ar: 4 6 3 2 45 6
          index: 0 1 2 3 4  5
    For array index is start from right to left:
                          num = 11
          binart from of num :  1 0 1 1
                       index :  3 2 1 0         
```

<img width="1146" height="547" alt="image" src="https://github.com/user-attachments/assets/44ac6f73-105b-4e57-a777-fdd109a45678" />
<img width="1154" height="650" alt="image" src="https://github.com/user-attachments/assets/23b47995-7003-4a4a-bb2d-4e5727c63719" />

```
    >> : right shift
      => take x is a number then 
      => x >> n means x is divided with the 2^n
      -when n is 0 then take 0th index position from the x
      -when n is 1 then take 1st index position from the x   => x = 10 then in binary from it is 1010  i.e, 1st index is at 1  
         
      -when n is 4 then take 4th index position from the x

    lastSeen[bit] = i , at the bit position (bit) the i'th index is present
```

<img width="625" height="429" alt="image" src="https://github.com/user-attachments/assets/369751ab-8108-4953-9a69-d9e3d20177b2" />

```
  4 >> 2 means 4 / (2^2) => 4 / 4 => 1
  4: 100 two times right shift gives 1
  >> moves bits right like pushing them one position to the right.
  Each shift divides the number by 2.
  Leftmost bits are filled with 0.
  Rightmost bits are dropped (lost forever).
```

<img width="1133" height="703" alt="image" src="https://github.com/user-attachments/assets/bf9eadb5-8770-4acc-b8a0-886ff1391e9b" />
<img width="1134" height="256" alt="image" src="https://github.com/user-attachments/assets/337b1014-1502-477f-b201-46ae2ebad9d1" />
<img width="933" height="174" alt="image" src="https://github.com/user-attachments/assets/81e35acd-fa2a-44e1-9535-32a3039cd614" />

# Dry - Run
<img width="1113" height="618" alt="image" src="https://github.com/user-attachments/assets/0128b8e2-aacb-4d8f-96fd-37f9437e4f86" />


# Optimized - Code
```
class Solution {
public:
    vector<int> smallestSubarrays(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n);
        vector<int> lastSeen(32,-1);
        for(int i = n-1; i >= 0; i--){
            for(int bit = 0; bit < 32; bit++){
                if((nums[i] >> bit) & 1){
                    lastSeen[bit] = i;
                }
            }

            int farest = i;
            for(int bit = 0; bit < 32; bit++){
                if(lastSeen[bit] != -1){
                    farest = max(farest, lastSeen[bit]);
                }
            }
            ans[i] = (farest - i + 1);
        }
        return ans;
    }
};
```
🔗 [Smallest Subarrays With Maximum Bitwise OR](https://leetcode.com/problems/smallest-subarrays-with-maximum-bitwise-or/)

💡 Submission: [Click here](https://leetcode.com/problems/smallest-subarrays-with-maximum-bitwise-or/submissions/1715948079/)


