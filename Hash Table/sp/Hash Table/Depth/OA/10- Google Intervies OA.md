# Problem 
<img width="648" height="129" alt="image" src="https://github.com/user-attachments/assets/ba9f54b4-eff8-45d5-8c5c-f3eebbec6b45" />

# Intuition
```
Brute Force :  write 3 loops to know how many tuplets as A[i] > A[j] < A[k] ,
               TC : O(N^3):
                            -> n.
                            -> b[n+1]
                            
                            c = 0 
                            for(int i=1;i<=n;i++){
                                
                                for(int j=i+1;j<=n;j++){
                                    
                                    for(int k=j+1;k<=n;k++){
                                        
                                        if(b[i]>b[j] && b[j]<b[k]){
                                            c++;
                                        }
                                        
                                    }
                                    
                                }
                            }
                            print(c)

Optimal Intuoition :   Use prefix to know how many elements are A[i] > A[j] present between the {0 to j-1}
                       Use suffix to know how many elements are A[j] < A[k] present between the {j+1 to  n-1}
```

<img width="1600" height="754" alt="image" src="https://github.com/user-attachments/assets/f47d537f-4878-40fa-84dc-3ed7c1aa2997" />


# Run Code
https://ideone.com/fEZrTm
