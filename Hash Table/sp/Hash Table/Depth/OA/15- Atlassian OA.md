# General INtuition which has to applied when question asked like divide array into N equal parts
<img width="1599" height="769" alt="image" src="https://github.com/user-attachments/assets/e7c35ce3-1546-4107-a0df-9478f562698e" />



# Problem 
<img width="690" height="258" alt="image" src="https://github.com/user-attachments/assets/516c393b-9c70-4872-9655-a5bafe14551c" />

# Intuition
<img width="689" height="266" alt="image" src="https://github.com/user-attachments/assets/7345b929-ff90-4ec1-a52c-5f958e68cdf2" />
## Brute Force : O(n^2)

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<long long> arr(n);

    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    int ways = 0;

    // For each possible cut, compute LHS and RHS sums separately
    for (int cut = 0; cut < n - 1; cut++) {
        long long leftSum = 0, rightSum = 0;

        // Sum left part
        for (int i = 0; i <= cut; i++) {
            leftSum += arr[i];
        }

        // Sum right part
        for (int i = cut + 1; i < n; i++) {
            rightSum += arr[i];
        }
        if (leftSum == rightSum) {
            ways++;
        }
    }

    cout << ways << endl;
    return 0;
}
```

## Optimal Code 1: O(n)

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<long long> arr(n);

    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    // Step 1: Find total sum
    long long totalSum = accumulate(arr.begin(), arr.end(), 0LL);

    // Step 2: If total sum is odd, cannot divide equally
    if (totalSum % 2 != 0) {
        cout << 0 << endl;
        return 0;
    }

    long long halfSum = totalSum / 2;
    long long leftSum = 0;
    int ways = 0;

    // Step 3: Check partitions
    for (int i = 0; i < n - 1; i++) {     // stick can't be after last element
        leftSum += arr[i];
        if (leftSum == halfSum) {
            ways++;
        }
    }

    cout << ways << endl;
    return 0;
}
```

## Optimal code 2

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<long long> arr(n);

    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    // Step 1: Calculate prefix sums
    vector<long long> prefix(n), suffix(n);

    prefix[0] = arr[0];
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + arr[i];
    }

    suffix[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--) {
        suffix[i] = suffix[i + 1] + arr[i];
    }

    // Step 2: Total sum check
    if (prefix[n - 1] % 2 != 0) {
        cout << 0 << endl;
        return 0;
    }

    long long halfSum = prefix[n - 1] / 2;
    int ways = 0;

    // Step 3: Compare prefix[i] with suffix[i+1]
    for (int i = 0; i < n - 1; i++) { 
        if (prefix[i] == halfSum && suffix[i + 1] == halfSum) {
            ways++;
        }
    }

    cout << ways << endl;
    return 0;
}
```

---
# Follow Up Question 1
<img width="650" height="84" alt="image" src="https://github.com/user-attachments/assets/dac3b34d-cc18-482d-afd7-3100a1950370" />
# Intuition
<img width="676" height="318" alt="image" src="https://github.com/user-attachments/assets/f482b928-b648-486c-88fc-dbfd93e59fd8" />

## Code 

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<long long> arr(n);

    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    long long total = accumulate(arr.begin(), arr.end(), 0LL);

    // Total must be divisible by 3
    if (total % 3 != 0) {
        cout << 0 << endl;
        return 0;
    }

    long long target = total / 3;
    long long twoThirds = 2 * target;

    long long prefixSum = 0;
    long long countFirstPart = 0;
    long long ways = 0;

    // Traverse till n-1 because last part must be non-empty
    for (int i = 0; i < n - 1; i++) {
        prefixSum += arr[i];

        // If prefix sum so far is target, this could be the end of first part
        if (prefixSum == target) {
            countFirstPart++;
        }

        // If prefix sum so far is twoThirds, then we can form partitions
        // using any of the earlier positions that had sum == target
        if (prefixSum == twoThirds) {
            ways += countFirstPart;
        }
    }

    cout << ways << endl;
    return 0;
}

```

---
# Follow Up Question 2
<img width="665" height="165" alt="image" src="https://github.com/user-attachments/assets/ba82791f-c026-4963-bcda-0ed71575a718" />

# Intuition
<img width="1184" height="260" alt="image" src="https://github.com/user-attachments/assets/68376505-2780-492b-8834-68912673ae92" />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<long long> arr(n);

    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    long long total = accumulate(arr.begin(), arr.end(), 0LL);

    // Total must be divisible by 4
    if (total % 4 != 0) {
        cout << 0 << endl;
        return 0;
    }

    long long target = total / 4;          //every part value
    long long half = 2 * target;          //two Forth value
    long long threeFourth = 3 * target;

    long long prefixSum = 0;
    long long countFirstPart = 0;   // positions with sum == target
    long long countSecondPart = 0;  // positions with sum == half
    long long ways = 0;

    // Traverse till n-1 because last part must be non-empty
    for (int i = 0; i < n - 1; i++) {
        prefixSum += arr[i];

        // If sum == target, possible end of first part
        if (prefixSum == target) {
            countFirstPart++;
        }

        // If sum == half, then every earlier target can pair with this
        if (prefixSum == half) {
            countSecondPart += countFirstPart;
        }

        // If sum == 3*target, then every earlier half can pair with this
        if (prefixSum == threeFourth) {
            ways += countSecondPart;
        }
    }
    cout << ways << endl;
    return 0;
}
```

```
