# PROBLEM
<img width="716" height="672" alt="image" src="https://github.com/user-attachments/assets/af41f9fd-afdf-4606-9ea0-689a0d8d6ce7" />
<img width="628" height="349" alt="image" src="https://github.com/user-attachments/assets/efaddef7-6218-484e-9fb1-048488a0c72b" />


# INTUITION

```
Understanding : We are given an array B of size “N”; Divide the array into 4 continuous parts
such that g = part1 -part2 +part3 -part4 is maximized. 
Any part is allowed to be empty as well ; but collectively they should cover the whole array

G = p1 + p3 - (p2 + p4)
If you want to make G bigger what should you do ?

==> To maximize G, we should maximize p1 and p3 and minimize p2 and p4
```

## BRUTE FORCE
```
   sum(0,i)−sum(i,j)+sum(j,k)−sum(k,n) where the indices satisfy  0 ≤ i ≤ j ≤ k ≤ n.
```

<img width="1010" height="261" alt="image" src="https://github.com/user-attachments/assets/18cc7dc2-7f9a-4be9-9557-1b3f8035724e" />
<img width="840" height="179" alt="image" src="https://github.com/user-attachments/assets/c70e878b-6c38-4b10-a344-616fcde9734b" />

```
int maxSubarraySumBruteForce(const vector<int>& arr) {
    int n = arr.size();
    
    // Compute prefix sums for O(1) sum queries
    vector<int> prefixSum(n+1, 0);
    for(int i = 0; i < n; i++) {
        prefixSum[i+1] = prefixSum[i] + arr[i];
    }
    
    int maxValue = INT_MIN;
    
    // Try all i, j, k with 0 <= i <= j <= k <= n
    for(int i = 0; i <= n; i++) {
        for(int j = i; j <= n; j++) {
            for(int k = j; k <= n; k++) {
                // sum(0, i)
                int sum1 = prefixSum[i] - prefixSum[0];
                // sum(i, j)
                int sum2 = prefixSum[j] - prefixSum[i];
                // sum(j, k)
                int sum3 = prefixSum[k] - prefixSum[j];
                // sum(k, n)
                int sum4 = prefixSum[n] - prefixSum[k];
                
                int value = sum1 - sum2 + sum3 - sum4;
                if(value > maxValue) {
                    maxValue = value;
                }
            }
        }
    }
    
    return maxValue;
}

int main() {
    vector<int> arr = {-3, 4, -5, 2, 6, -5};
    int result = maxSubarraySumBruteForce(arr);
    cout << result << endl; // output the max value
    
    return 0;
}
```
<img width="970" height="322" alt="image" src="https://github.com/user-attachments/assets/cd40311f-5cb4-44e5-9469-fbc067e9c228" />

## Run Here
https://ideone.com/WRx82j


## OPTIMAL 
<img width="745" height="391" alt="image" src="https://github.com/user-attachments/assets/d75bd8fa-52f5-4c07-a803-9d4cb89bb285" />
<img width="1034" height="557" alt="image" src="https://github.com/user-attachments/assets/eb92bbb3-740e-4c0e-b18e-5b1dd04607e5" />

<img width="473" height="365" alt="image" src="https://github.com/user-attachments/assets/c5c45127-aafb-4846-a46a-1d9f1945a402" />


```
int maxGValue(vector<int>& arr) {
    int n = arr.size();
    vector<int> prefix(n+1, 0);
    for (int i = 0; i < n; i++) {
        prefix[i+1] = prefix[i] + arr[i];
    }

    // Total sum of the array
    int totalSum = prefix[n];

    // Step 1: Compute min prefix subarray sum ending at or before i (P2)
    vector<int> minP2(n, INT_MAX);
    int minSum = INT_MAX;
    int currentSum = 0;
    // int start = 0;


    //This is a variation of Kadane’s algorithm, but instead of finding maximum subarray sum, we're tracking the minimum subarray sum ending at or before i.
    for (int i = 0; i < n; i++) {
        currentSum += arr[i];
        minSum = min(minSum, currentSum);
        minP2[i] = minSum;
        if (currentSum > 0) currentSum = 0; // reset if subarray becomes positive
    }

    // Step 2: Compute min suffix subarray sum starting at or after i+1 (P4)
    vector<int> minP4(n+1, INT_MAX);
    currentSum = 0;
    minSum = INT_MAX;
    for (int i = n - 1; i >= 0; i--) {
        currentSum += arr[i];
        minSum = min(minSum, currentSum);
        minP4[i] = min(minP4[i+1], minSum);
        if (currentSum > 0) currentSum = 0;
    }

    // Step 3: Try each i as end of P2 and i+1 as start of P4
    int result = INT_MIN;
    for (int i = 0; i < n; i++) {
        int p2 = minP2[i];
        int p4 = (i + 1 < n) ? minP4[i + 1] : 0;
        int g = totalSum - 2 * (p2 + p4);
        result = max(result, g);
    }

    return result;
}

int main() {
    vector<int> arr = {1, 2, 1, -5}; // Example from your notes
    cout << maxGValue(arr) << endl; // Should output 9

    return 0;
}

```

## DRY RUN
<img width="975" height="765" alt="image" src="https://github.com/user-attachments/assets/ef6ce545-81fb-464f-880e-c1d74b1c5b70" />


<img width="1049" height="470" alt="image" src="https://github.com/user-attachments/assets/99a2d730-dd27-4004-a77f-e511fe65b48c" />
<img width="1078" height="183" alt="image" src="https://github.com/user-attachments/assets/90beede8-4650-4599-b680-67c51c8e0380" />
<img width="1072" height="488" alt="image" src="https://github.com/user-attachments/assets/fc260a93-2b59-403e-9c44-d88883dd6ff3" />
<img width="982" height="713" alt="image" src="https://github.com/user-attachments/assets/2ee911f3-ea7d-4074-a25c-1b01617ac44a" />

| i | p2 = minP2\[i] | p4 = minP4\[i+1] or 0 if out of range | Calculation of `g`                             | `g` Result | `result` (max so far) |
| - | -------------- | ------------------------------------- | ---------------------------------------------- | ---------- | --------------------- |
| 0 | 1              | minP4\[1] = -5                        | `-1 - 2 * (1 + (-5)) = -1 - 2 * (-4) = -1 + 8` | 7          | 7                     |
| 1 | 1              | minP4\[2] = -5                        | `-1 - 2 * (1 + (-5)) = 7`                      | 7          | 7                     |
| 2 | 1              | minP4\[3] = -5                        | `-1 - 2 * (1 + (-5)) = 7`                      | 7          | 7                     |
| 3 | -5             | minP4\[4] = 0                         | `-1 - 2 * (-5 + 0) = -1 - 2 * (-5) = -1 + 10`  | 9          | 9                     |

so ans = 9


