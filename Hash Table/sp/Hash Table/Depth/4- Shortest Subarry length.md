# Problem
<img width="674" height="332" alt="image" src="https://github.com/user-attachments/assets/efeccff9-c818-4f5f-b7ce-7db2d79700ee" />

# Intuition
<img width="1086" height="407" alt="image" src="https://github.com/user-attachments/assets/22866140-8255-4e2b-b690-0996635c512e" />
<img width="993" height="435" alt="image" src="https://github.com/user-attachments/assets/95067eda-788d-484d-a57b-3baa09c052e7" />
<img width="1011" height="353" alt="image" src="https://github.com/user-attachments/assets/f24694de-88b1-4015-af95-7d14db105d04" />


![WhatsApp Image 2025-08-04 at 09 57 16_3505ba21](https://github.com/user-attachments/assets/55018d5c-df7f-4cfe-96bc-1776d16536bd)

## Understand the Dry Run
![WhatsApp Image 2025-09-05 at 10 07 23_252882c7](https://github.com/user-attachments/assets/8d438052-53d9-4a45-8a47-fcbec6573a2e)


# Code
```
#include <iostream>
#include <vector>
#include <unordered_map>
#include <climits>
using namespace std;

int main() {
    int n;
    cin >> n;             // Input size of array
    vector<int> a(n);     // Declare array of size n

    for (int i = 0; i < n; i++) {
        cin >> a[i];      // Input elements of array
    }

    int k;
    cin >> k;             // Target sum

    unordered_map<int, int> mp; // Map to store prefix sum and its index
    int sum = 0;
    int mini = INT_MAX;        // Store the shortest subarray length
    mp[0] = -1;                // To handle the case when subarray starts from index 0

    // First pass to find the minimum length
    for (int i = 0; i < n; i++) {
        sum += a[i];
        if (mp.find(sum - k) != mp.end()) {
            mini = min(mini, i - mp[sum - k]);
        }
        // Store the first occurrence of a prefix sum only
        if (mp.find(sum) == mp.end()) {
            mp[sum] = i;
        }
    }

    // Second pass to count how many subarrays have that minimum length and sum = k
    //int count = 0;
    //for (int i = 0; i <= n - mini; i++) {       //O(n^2)
    //    int current_sum = 0;
    //    for (int j = i; j < i + mini; j++) {
    //        current_sum += a[j];
    //    }
    //    if (current_sum == k) {
    //        count++;
    //    }
    //}

    int current_sum = 0;     //sliding windows
    for (int i = 0; i < mini; i++) {
        current_sum += a[i];
    }
    if (current_sum == k) count++;
    for (int i = mini; i < n; i++) {
        current_sum += a[i] - a[i - mini];
        if (current_sum == k) count++;
    }
    cout << count << endl; // Output the result
    return 0;
}

```

# Optimal Code
```
#include <iostream>
#include <vector>
#include <unordered_map>
#include <climits>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n);

    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }

    int k;
    cin >> k;

    unordered_map<int, int> mp;     // prefix sum → index
    mp[0] = -1;     // prefix sum 0 at index -1

    int sum = 0;
    int minLen = INT_MAX;
    int count = 0;

    for (int i = 0; i < n; i++) {
        sum += a[i];

        // Check if there's a previous prefix with sum = (sum - k)
        if (mp.find(sum - k) != mp.end()) {
            int len = i - mp[sum - k];

            if (len < minLen) {
                minLen = len;
                count = 1; // found a shorter one
            } else if (len == minLen) {
                count++; // same shortest length
            }
        }

        // Store only the earliest index for this sum to ensure minimum length
        if (mp.find(sum) == mp.end()) {
            mp[sum] = i;
        }
    }

    cout << count << endl;
    return 0;
}

```
