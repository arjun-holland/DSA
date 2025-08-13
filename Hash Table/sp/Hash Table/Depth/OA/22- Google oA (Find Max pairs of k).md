# Problem
<img width="480" height="107" alt="image" src="https://github.com/user-attachments/assets/48ef41d8-3af9-459b-9bf6-a505781902d5" />

# Intuition
## Extension of 6 th prob from Depth folder
## Optimal 1
<img width="516" height="532" alt="image" src="https://github.com/user-attachments/assets/4f726367-fc99-4709-80a6-04a6bf075b55" />

```
-->n
--->b

leetcode(vector<int>& nums, int k) {     
        unordered_map <int,int> kk,gg; 
        int i = 0 ; 
        int n = nums.size();
        while(i<n){
            kk[nums[i]]=kk[nums[i]]+1;
            i=i+1;
        }
        int answer = 0 ; 
        for(i=0;i<n;i++){
            int number = nums[i] ; 
            int partner = k - number ; 
            if(gg[number]==0 && gg[partner]==0){
                if(number==partner){
                    int yy = kk[number];
                    answer = answer + (yy/2);
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

k = 0 
final_answer = 0 
while(k <= 2000000000){   //we can directly run k from {sum of two smallest numbers in nums , sum of two largest nums in nums}
    answer = leetcode(b,k)
    final_answer = max(final_answer,answer)
    k=k+1
}

---> final_answer
```

## Optimal 2

```
-->n
--->b

leetcode(vector<int>& nums, int k) {
        unordered_map <int,int> kk,gg; 
        int i = 0 ; 
        int n = nums.size();
        while(i<n){
            kk[nums[i]]=kk[nums[i]]+1;
            i=i+1;
        }
        int answer = 0 ; 
        for(i=0;i<n;i++){
            int number = nums[i] ; 
            int partner = k - number ; 
            if(gg[number]==0 && gg[partner]==0){
                if(number==partner){
                    int yy = kk[number];
                    answer = answer + (yy/2);
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


i = 0 
while(i<n){ //O(N)
    j = 0 
    while(j<n){ //O(N)
        
        k = b[i] + b[j] 
        answer = leetcode(b,k) //O(N)
        final_answer = max(final_answer,answer)
        
        j=j+1
    }
    i=i+1
}
-> O(N^3) = N = 100 ; O(1000000)
---> final_answer

```
