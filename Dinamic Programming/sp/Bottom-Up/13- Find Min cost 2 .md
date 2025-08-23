# PROBLEM
<img width="1070" height="317" alt="image" src="https://github.com/user-attachments/assets/64dff14d-4293-4b18-90a0-f810756d81f3" />

# INTUITION


# OPTIMAL CODE 1
```
#include <bits/stdc++.h>
using namespace std;

int minStepsToOne(int N) {
    vector<int> dp(N + 1, 0);
    dp[1] = 0;    // Base case: 1 already requires 0 steps
    
    for (int i = 2; i <= N; i++) {
        int p1 = 1 + dp[i - 1];  // Step: subtract 1
        int p2 = INT_MAX, p3 = INT_MAX;
        
        if (i % 2 == 0) {
            p2 = 1 + dp[i / 2];  // Step: divide by 2
        }
        if (i % 3 == 0) {
            p3 = 1 + dp[i / 3];  // Step: divide by 3
        }
        
        dp[i] = min(p1, min(p2, p3));
    }
    
    return dp[N];
}

int main() {
    int N;
    cin >> N;
    cout << minStepsToOne(N) << endl;
    return 0;
}

```


# OPTIMAL CODE 2
```
After observation we came to a conclusion :
      If the number is even you can divide it by 2. 
      If the number is odd you can do +1 or -1 
```
```
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

int main() {
    int n = 5;
    int dp[n+1]={0};
    dp[1] = 0 ; 

    int i = 2 ; 
    while(i <= n){    	
    	if(i % 2 == 0){
    		dp[i] = 1 + dp[i/2];
    	}
    	else{	
    		dp[i] = min(1 + dp[i-1], 2 + dp[(i+1)/2]);
    	}
      i++;
    }
    cout<<dp[n];
    return 0 ; 
}
```
