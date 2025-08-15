# PROBLEM 1
<img width="685" height="204" alt="image" src="https://github.com/user-attachments/assets/cbcfc002-c29a-4742-970e-2463d7039b2b" />

## Intuition
          ```
          -> answer[1] = a[1] 
          -> answer[2] = max(a[2] or a[2] + answer[1])
          -> answer[3] = max(a[3] or a[3] + answer[2])
          .
          .
          .
          -> answer[i] = max(a[i], a[i] + answer[i-1]) 
          
          Algorithm ➖
          -> n 
          -> b[n+1]
          -> p[n+1]={0}
          
          p[1] = b[1]
          for(int i=2;i<=n;i++){
              p[i] = max(b[i],b[i] + p[i-1])
              print(p[i])
          }
          
          TC : 0(N)
          SC : O(N)
          ```
          
          ```
          We can do this in O(1) space as well
          int n;
          cin >> n;
          vector<int> b(n + 1);
          for (int i = 1; i <= n; i++) cin >> b[i];
          
          int currentSum = b[1];         // p[1]
          int maxSum = b[1];             // Store the overall max
          
          for (int i = 2; i <= n; i++) {
              currentSum = max(b[i], b[i] + currentSum);  // p[i] = max(b[i], b[i] + p[i-1])
              maxSum = max(maxSum, currentSum);           // Track the global max
              cout << currentSum << endl;                 // Print p[i] if needed
          }
          
          cout << "Max subarray sum: " << maxSum << endl;
          ```
---

# PROBLEM 2
```
Find the maximum sum of two non overlapping subarrays. 
```

## Intuition
```
      -> Let's fix the first subarray :->
      
      Either it might be ending at first index ;
      
      Or 2nd index ; 
      Or 3rd index ; 
      Or 4th index ; 
      .
      .
      .
      .
      .
      N-1 index. 
            
      We iterate through all pairs (i,j) ;

      Where p[i] tells us best sum possible of first subarray ending at index “i” ; and s[j] tells us best possible sum of second subarray starting at index “j” -> p[i] + s[j]
      
      > n 
      -> b[n+1]
      
      -> p[n+1]={0}  //preffix
      -> s[n+1] = {0}  //suffix
      
      p[1] = b[1]
      
      for(int i=2;i<=n;i++){
          p[i] = max(b[i],b[i] + p[i-1])
          print(p[i])
      }
      
      
      s[n] = b[n] 
      for(int j = n-1;j>=1;j--){
          s[j] = max(b[j],b[j] + s[j+1])
      }
      
      
      answer = 0 
      for(i=1; i<=n-1; i++){
          for(j=i+1; j<=n; j++){  //we dobnt know where the second subarray it be in the range {i+1 to n}
              u = p[i] + s[j]
              answer = max(answer,u)
          }
      }
      
      print(answer)


  it gives the .......... TC O(N^2) ,   SC O(1)
```

## Optimize above Code
```
        -> n 
        -> b[n+1]
        
        -> p[n+1]={0}
        -> s[n+1] = {0}
        -> max_s[n+1] = {0}
        
        p[1] = b[1]
        for(int i=2;i<=n;i++){
            p[i] = max(b[i],b[i] + p[i-1])
            print(p[i])
        }
        
        
        s[n] = b[n] 
        for(int j = n-1;j>=1;j--){
            s[j] = max(b[j],b[j] + s[j+1])
            max_s[j] = max(s[j],max_s[j+1])   // helps us to find the max of suffix subarray at the j'th index
        }
        
        
        answer = 0 
        for(i=1;i<=n-1;i++){
                u = p[i] + max_s[i+1]
                answer = max(answer,u)
        }
        
        print(answer)
        
        it gives........TC : O(N), SC : O(N)

```

----

# PROBLEM 3 : Extension of the PROBLEM 2

```
Second subarray should be strictly increasing 
```

## Intuition

<img width="966" height="138" alt="image" src="https://github.com/user-attachments/assets/f64cfa2f-adbe-4419-90d7-d695386ee888" />

```
      #include <iostream>
      #include <vector>
      #include <algorithm>
      using namespace std;
      
      typedef long long ll;
      
      int main() {
          int n;
          cin >> n;
          
          vector<ll> b(n + 2);         // Input array (1-based indexing)
          vector<ll> p(n + 2, 0);      // p[i] = max subarray sum ending at index i
          vector<ll> s(n + 2, 0);      // s[i] = sum of longest increasing subarray starting at i
          vector<ll> u(n + 2, 0);      // u[i] = max(b[i], s[i]) — helper to simplify combining
          vector<ll> max_s(n + 2, 0);  // max_s[i] = max value of u[j] for j >= i
      
          // Input
          for (int i = 1; i <= n; i++) {
              cin >> b[i];
          }
      
          // Step 1: Calculate p[i] — max subarray sum ending at i using Kadane's
          p[1] = b[1];
          for (int i = 2; i <= n; i++) {
              p[i] = max(b[i], b[i] + p[i - 1]);     // cout << "p[" << i << "] = " << p[i] << endl;
          }
      
          // Step 2: Calculate s[i], u[i], and max_s[i] from right to left
          s[n] = b[n];          // Last element's increasing sum is itself
          u[n] = s[n];          // Same for u
          max_s[n] = u[n];      // Base case for max suffix
      
          for (int j = n - 1; j >= 1; j--) {
              if (b[j] < b[j + 1]) {
                  s[j] = b[j] + s[j + 1];  // Continue increasing
              } else {
                  s[j] = b[j];             // Restart increasing subarray
              }
      
              u[j] = max(b[j], s[j]);      // Best starting at j
              max_s[j] = max(u[j], max_s[j + 1]); // Build max suffix array
          }
      
          // Step 3: Combine prefix max (p[i]) with max increasing suffix starting at i+1
          ll answer = 0;
          for (int i = 1; i <= n - 1; i++) {
              ll l = p[i] + max_s[i + 1];
              answer = max(answer, l);
          }
      
          // Output final result
          cout << answer << endl;
      
          return 0;
      }

      TC : O(N)
      SC : O(N)

```

```
            Instead of using u[] we can
    
    max_s[j] = max({b[j], s[j], max_s[j + 1]}); // using initializer list
    
                      or 
    
    max_s[j] = max(max(b[j], s[j]), max_s[j + 1]);
```
