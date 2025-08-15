# Problme
<img width="642" height="207" alt="image" src="https://github.com/user-attachments/assets/0a693605-e7ae-4342-bcd4-e2c13841d0fa" />


# Code
## Brute Force : O(n^3)
`
Brute force :- Check all the subarray if its a valley increase the counter 
`

```
#include <iostream>
#include <cstdlib> // For abs function
using namespace std;

bool check(int i, int j, int* b) {
	
    int mv = b[i];
    int id = i;
    
    for (int l = i; l <= j; l++) {
        if (b[l] < mv) {
            mv = b[l];
            id = l;
        }
    }
    
    if(id == i){
    	
    	return false;
    	
    }

    int left = id;
    while (left >= i + 1) {
        if (b[left] < b[left - 1]) {
            // Do nothing
        } else {
            return false;
        }
        left--;
    }

    int right = id;
    while (right <= j - 1) {
        if (b[right] < b[right + 1]) {
            // Do nothing
        } else {
            return false;
        }
        right++;
    }
    return true;
}

int main() {
    int n;
    cin >> n;

    int* b = new int[n + 1];
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    int count = 0;
    for (int i = 1; i <= n; i++) {
        for (int j = i; j <= n; j++) {
            if (abs(i - j) >= 2 && check(i, j, b)) {
                // [i......j]--> valley
                // cout<<i<<" j is "<<j<<endl;
                count++;
            }
        }
    }
    cout << count << endl;
    return 0;
}

```


## Optimal
```
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n;
    cin >> n;

    vector<int> b(n + 2);            // 1-based indexing
    vector<int> left(n + 2, 1);      // Length of decreasing sequence ending at i
    vector<int> right(n + 2, 1);     // Length of increasing sequence starting at i

    // Input array
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    // Step 1: Compute decreasing streaks ending at each index
    for (int i = 2; i <= n; i++) {
        if (b[i - 1] > b[i]) {
            left[i] = left[i - 1] + 1;
        } else {
            left[i] = 1;
        }
    }

    // Step 2: Compute increasing streaks starting at each index
    for (int i = n - 1; i >= 1; i--) {
        if (b[i] < b[i + 1]) {
            right[i] = right[i + 1] + 1;
        } else {
            right[i] = 1;
        }
    }

    // Step 3: Count valid valley subarrays
    long long totalValleys = 0;

    for (int i = 1; i <= n; i++) {
        if (left[i] >= 2 && right[i] >= 2) {
            // Each valley of form [..decreasing..i..increasing..]
            // contributes (left[i]-1) * (right[i]-1) subarrays
            totalValleys += (long long)(left[i] - 1) * (right[i] - 1);
        }
    }

    cout << totalValleys << endl;
    return 0;
}

```
