# PROBLEM
<img width="844" height="741" alt="image" src="https://github.com/user-attachments/assets/451e81bf-6085-4fda-b85b-14ff5455d918" />
<img width="762" height="493" alt="image" src="https://github.com/user-attachments/assets/42ee0850-42bd-400d-a6c1-ae1818fee252" />

# INTUITION
```
//GCD in recurssion
     int GCD(int a, int b){
         if(b == 0)return a;
         return GCD(b, a % b);
     }
//GCD in Iteration
     int GCD(int e, int o){
         int ans = 1;
         for(int i=1;i<=(min(e,o)); i++){
             if((e % i == 0) && (o % i == 0))ans = i;
         }
         return ans;
     }
```

# Code
```
class Solution {
public:
    int gcdOfOddEvenSums(int n) {

        int se = (n)*(n+1);   //sum of 'n' even numbers
        int so = (n)*(n);     //sum of 'n' odd numbers

        return n;   // GCD(n*n , n*(n-1)) => n
        // int ans = GCD(se,so);
        // return ans;
    }
};©leetcode
```
