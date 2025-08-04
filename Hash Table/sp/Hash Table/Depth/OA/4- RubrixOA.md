# General QUestion
<img width="794" height="198" alt="image" src="https://github.com/user-attachments/assets/9deb0f1e-c587-4a9b-8c57-46b95eb52ba4" />

# Brute Force
```
int main() {
    int n, x, y;
    cin >> n >> x >> y;
    vector<int> b(n + 1, 0);  // Initialize the array with size n + 1
    // Input array
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }
    int c = 0;  // Count of valid subarrays

    // Brute-force approach
    for (int i = 1; i <= n; i++) {
        int cx = 0, cy = 0;  // Counters for x and y
        
        for (int j = i; j <= n; j++) {  // Iterate over subarrays
            if (b[j] == x) {
                cx++;
            }
            if (b[j] == y) {
                cy++;
            }
            if (cx == cy) {
                c++;  // Found a valid subarray
            }
        }
    }
    cout << c << endl;  // Print the result
    return 0;
}
```

# Optimal Code 1
```
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

int main() {
    int n, x, y;
    cin >> n >> x >> y; // Input size of the array and the two integers x and y
    vector<int> b(n);    // Array of size n

    // Input array and transform
    for (int i = 0; i < n; i++) {
        int temp;
        cin >> temp;
        b[i] = (temp == x) ? -1 : 1;  // Replace x with -1 and y with 1
    }

    unordered_map<int, int> prefixSumCount;  // Map to store prefix sums and their counts
    prefixSumCount[0] = 1;  // Initialize for subarrays that sum to 0 from the start
    int currentSum = 0;      // Current prefix sum
    int count = 0;           // Count of valid subarrays

    // Calculate the prefix sum and count the occurrences
    for (int i = 0; i < n; i++) {
        currentSum += b[i];  // Update the current sum
        count += prefixSumCount[currentSum];  // Add count of previous same prefix sums
        
        // Update the count of current prefix sum
        prefixSumCount[currentSum]++;
    }

    cout << count << endl;  // Print the result
    return 0;
}
//2 2 1 1 2 2
//5
//2 2 1 1 , 2 1 , 1 2, 2 1 1 2, 1 1 2 2
```
# Intution
<img width="1107" height="549" alt="image" src="https://github.com/user-attachments/assets/cda5e6a9-5e9a-4ba9-b824-6ef3d13d9cc1" />
<img width="1048" height="257" alt="image" src="https://github.com/user-attachments/assets/bde53a88-4829-497a-8c39-4dcc676c613a" />

📊 Step-by-step Table:

| i | b\[i] | cx | cy | d = cx - cy | freq\[d] (before) | count (+= freq\[d]) | freq\[d] (after) |
| - | ----- | -- | -- | ----------- | ----------------- | ------------------- | ---------------- |
| 1 | 2     | 1  | 0  | 1           | 0                 | 0                   | 1                |
| 2 | 2     | 2  | 0  | 2           | 0                 | 0                   | 1                |
| 3 | 1     | 2  | 1  | 1           | 1                 | 1                   | 2                |
| 4 | 1     | 2  | 2  | 0           | 1                 | 1                   | 2                |
| 5 | 2     | 3  | 2  | 1           | 2                 | 2                   | 3                |
| 6 | 2     | 4  | 2  | 2           | 1                 | 1                   | 2                |

<img width="896" height="218" alt="image" src="https://github.com/user-attachments/assets/5f33a33b-dfc0-4bab-8c84-077ca41ede08" />

<img width="594" height="188" alt="image" src="https://github.com/user-attachments/assets/f9974d9b-e93b-4402-8cc7-ee0f93783280" />

```
-> n
-> b[n+1] = {0} c = 0 
-> hashmap <c2-c1,count> f;

for(i=1;i<=n;i++){ cx = 0 cy = 0 
   d = cx - cy
   c = c + f[d] -> f[d] = how many times 'd' was achieved from 1 to j-1 
   
   f[d]++
}
print(c)
```

# Ooptimal Code 2 (clear)
```
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

int main() {
    int n, x, y;
    cin >> n >> x >> y;  // Input the size of the array and the two integers x and y
    vector<int> b(n + 1, 0);  // Array of size n + 1, initialized to 0

    // Input the array
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    long long count = 0;  // Count of valid subarrays
    unordered_map<int, int> freq;  // HashMap to store the frequency of d values
    freq[0] = 1;  // Base case: d = 0 has been achieved once

    int cx = 0, cy = 0;  // Counters for x and y

    // Loop through the array
    for (int i = 1; i <= n; i++) {
        // Update counters based on the value of b[i]
        if (b[i] == x) {  // Check if b[i] is equal to x
            cx++;
        } else if (b[i] == y) {  // Check if b[i] is equal to y
            cy++;
        }

        int d = cx - cy;  // Calculate d
        count += freq[d];  // Increment count based on how many times d was achieved
        freq[d]++;  // Update frequency of d
    }

    cout << count << endl;  // Output the count
    return 0;
}
```
# Run code
Op1 : https://www.jdoodle.com/ga/NPlN7eyS7oX8qKN4oXMQ%2Fg%3D%3D

Op2 : https://www.jdoodle.com/ia/1ozk

---

# Original Problem
<img width="798" height="221" alt="image" src="https://github.com/user-attachments/assets/1f43cf15-7b74-460f-be80-5a02c484515a" />

# Intuition

## General Rule
![WhatsApp Image 2025-08-04 at 08 43 42_c97850fd](https://github.com/user-attachments/assets/119b647d-3629-4be9-8e80-1948e32ef07b)

<img width="673" height="165" alt="image" src="https://github.com/user-attachments/assets/75e0b0c2-5031-4f5c-bc76-2825f467de9e" />
<img width="818" height="175" alt="image" src="https://github.com/user-attachments/assets/401adf8f-b4f0-4d40-983a-ffd8ff2f6208" />

```
-> n
-> b[n+1] = {0} c = 0 
-> hashmap <pair<c2-c1,c3-c2>,c> f;

for(i=1;i<=n;i++){ cx = 0 cy = 0 cz = 0 
   d1 = cy - cx d2 = cz - cy 
   c = c + f[{d1,d2}] -> f[{d1,d2}] = how many times 'd1' , 'd2' occured in same index from 1 to j-1 

   f[{d1,d2}]++
}
print(c)
```

![WhatsApp Image 2025-08-04 at 08 48 34_d6109a2d](https://github.com/user-attachments/assets/9edfefa5-5dd2-4a49-b5f1-41ed09721120)



# Easy version Code

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, x, y, z;
    cin >> n >> x >> y >> z;  // Input the size of the array and the three integers x, y, z
    vector<int> b(n + 1, 0);  // Array of size n + 1

    // Input the array
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    long long count = 0;  // Count of valid subarrays
    map<pair<int, int>, int> freq;  // HashMap to store frequencies of pairs
    freq[{0, 0}] = 1;  // Base case: (d1, d2) has been achieved once

    int cx = 0, cy = 0, cz = 0;  // Counters for x, y, and z

    // Loop through the array
    for (int i = 1; i <= n; i++) {
        if (b[i] == x) {    // Update counters based on the value of b[i]
            cx++;
        } else if (b[i] == y) {
            cy++;
        } else if (b[i] == z) {
            cz++;
        }

        int d1 = cy - cx;  // First condition difference
        int d2 = cz - cy;  // Second condition difference

        count += freq[{d1, d2}];  // Increment count based on how many times (d1, d2) was achieved
        freq[{d1, d2}]++;  // Update frequency of (d1, d2)
    }

    cout << count << endl;  // Output the count
    return 0;
}
```

Run Here: https://www.jdoodle.com/ia/1ozr

# Final Code

```
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int countValidSubarrays(int n, int x, int y, int z, int w, int b) {
        int count = 0;  // Count of valid subarrays
        map<tuple<int, int, int, int>, int> freq;  // Frequency map to store counts of (d1, d2, d3, d4)
        freq[{0, 0, 0, 0}] = 1;  // Base case: (d1, d2, d3, d4) has been achieved once

        int cx = 0, cy = 0, cz = 0, cw = 0, cb = 0;  // Counters for x, y, z, w, b

        for (int i = 0; i < n; i++) {
            int val;
            cin >> val;  // Taking input for each element of the array

            // Update counters based on the value
            if (val == x) cx++;
            else if (val == y) cy++;
            else if (val == z) cz++;
            else if (val == w) cw++;
            else if (val == b) cb++;

            // Compute differences
            int d1 = cy - cx;  // First condition difference
            int d2 = cz - cy;  // Second condition difference
            int d3 = cw - cz;  // Third condition difference
            int d4 = cb - cw;  // Fourth condition difference

            // Increment count based on how many times (d1, d2, d3, d4) was achieved
            count += freq[{d1, d2, d3, d4}];

            // Update frequency of (d1, d2, d3, d4)
            freq[{d1, d2, d3, d4}]++;
        }

        return count;
    }
};

int main() {
    int n, x, y, z, w, b;
    cin >> n >> x >> y >> z >> w >> b;  // Input the size and the distinct integers
    Solution sol;
    cout << sol.countValidSubarrays(n, x, y, z, w, b) << endl;  // Output the result
    return 0;
}

```

Run Here : [https://www.jdoodle.com/ia/1ozC](https://www.jdoodle.com/ga/sd%2F%2FBIngkLBr%2BWlX8hbSjQ%3D%3D)
