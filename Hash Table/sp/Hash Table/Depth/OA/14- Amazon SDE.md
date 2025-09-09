# Problem
<img width="647" height="339" alt="image" src="https://github.com/user-attachments/assets/d8ddffc3-da37-48a3-bfa9-38e499b57a4f" />
 

# Intuition
## Brute Force : - Iterate through all the triplets : T : O(n^3)
```
          function => {
          ->n.
          ->b[n]. 
          for(i=0;i<n;i++){
              for(j=i+1;j<n;j++){
                  for(k=j+1;k<n;k++){
                      if(b[i]<b[j] && b[j]<b[k]){
                          return true;
                      }
                  }
                  
              }
          }
          return false;
          }
```

## Optimal Code : O(n)
```
After understanding the question we get that we want to know weather the array contains a subsequence of size 3 such that
                a[i] < a[j] < a[k]
so when we are at the j'th index we want to know the smallest element in the range {0, j-1} [used prefix for this]and
   we want to know the largest element in the range {j+1, n-1} [used suffix for this]and
and we need to check that
      g = a[j]
      if(p[i-1] < g && g < s[i+1] ){
             //->return true; 
      }

```
```
#include <bits/stdc++.h>
using namespace std;

bool hasValidTriplet(vector<int> &b) {
    int n = b.size();
    if (n < 3) return false;

    vector<int> p(n), s(n);

    // p[i] = smallest number in range (0, i)
    p[0] = b[0];
    for (int i = 1; i < n; i++) {
        p[i] = min(p[i - 1], b[i]);
    }

    // s[i] = biggest number in range (i, n-1)
    s[n - 1] = b[n - 1];
    for (int i = n - 2; i >= 0; i--) {
        s[i] = max(s[i + 1], b[i]);
    }

    // Check for valid triplet
    for (int j = 1; j < n - 1; j++) {
        int g = b[j];
        if (p[j - 1] < g && g < s[j + 1]) {
            return true;     // found valid triplet
        }
    }
    return false; // no triplet found
}

int main() {
    vector<int> b = {5, 1, 4, 3, 6}; // example
    if (hasValidTriplet(b)) {
        cout << "Valid triplet exists\n";
    } else {
        cout << "No valid triplet\n";
    }
    return 0;
}

```

---

# Follow up Question
```
Same as above question but the triplet should be of the form:- (b[i]+1==b[j] && b[j]+1==b[k]) => b[i]<b[j]<b[k]
i.e chcek whether the consicutive triplets exist or not
```
# Intuition
<img width="1019" height="398" alt="image" src="https://github.com/user-attachments/assets/13fecb4f-c297-4166-a454-6ab8e0757250" />
<img width="811" height="183" alt="image" src="https://github.com/user-attachments/assets/8fc502c1-3817-40e6-b47a-bd8b798c4c65" />

# Code : O(n)
```
#include <bits/stdc++.h>
using namespace std;

bool hasConsecutiveTriplet(vector<int> &b) {
    int n = b.size();
    if (n < 3) return false;

    unordered_set<int> left;             // stores elements before j
    unordered_map<int, int> rightFreq;    // freq of elements after j

    // Initialize rightFreq with all elements
    for (int num : b) {
        rightFreq[num]++;
    }

    for (int j = 0; j < n; j++) {
        // Current b[j] is the middle element of the triplet , Remove it from right side
        if (--rightFreq[b[j]] == 0) {
            rightFreq.erase(b[j]);
        }

        // Check condition: left has b[j]-1, right has b[j]+1
        if (left.count(b[j] - 1) && rightFreq.count(b[j] + 1)) {
            return true;
        }

        // Add current element to left set
        left.insert(b[j]);
    }

    return false;
}

int main() {
    vector<int> b = {4, 5, 6, 3, 2};
    if (hasConsecutiveTriplet(b)) {
        cout << "Triplet of consecutive numbers exists\n";
    } else {
        cout << "No such triplet\n";
    }
    return 0;
}

```

# code :+ O(nlog n) -> this approach is wrong 
```
as we need only the triplets that means we are dealing witrh subsequences so its better to sort
```

<img width="1163" height="287" alt="image" src="https://github.com/user-attachments/assets/f6dd90b0-8ab5-483e-9bfb-05ca89e52041" />

```
#include <bits/stdc++.h>
using namespace std;

bool hasConsecutiveTriplet(vector<int> b) {
    int n = b.size();
    if (n < 3) return false;

    sort(b.begin(), b.end()); // O(N log N)

    // Scan for consecutive triplet
    for (int i = 0; i <= n - 3; i++) {
        if (b[i] + 1 == b[i + 1] && b[i + 1] + 1 == b[i + 2]) {
            return true;
        }
    }
    return false;
}

int main() {
    vector<int> b = {7, 5, 8, 6, 1, 3};
    if (hasConsecutiveTriplet(b)) {
        cout << "Triplet of consecutive numbers exists\n";
    } else {
        cout << "No such triplet\n";
    }
    return 0;
}

```
