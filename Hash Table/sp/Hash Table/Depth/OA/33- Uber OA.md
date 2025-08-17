<img width="920" height="281" alt="image" src="https://github.com/user-attachments/assets/3d8dab2b-6ef2-4778-942a-b38f77a71a31" /># PROBLEM
<img width="798" height="122" alt="image" src="https://github.com/user-attachments/assets/0489c81e-cf5a-4483-9377-42a7daba5038" />

---
# Understanding the abs()
<img width="877" height="443" alt="image" src="https://github.com/user-attachments/assets/01ac0aec-f0c3-463c-899f-4e6da9506770" />


# solve easy version first

<img width="779" height="306" alt="image" src="https://github.com/user-attachments/assets/5ff7ae45-d147-4a20-bdf5-bb931f2921a3" />
<img width="924" height="526" alt="image" src="https://github.com/user-attachments/assets/2a3fec3a-b1f1-4760-8b14-1b061e66191b" />

## BRUTE FORCE : O(n^2) try all possibilities
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;
    vector<int> a(n);
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }
    int maxVal = 0;  // stores maximum value

    // Check all pairs (i, j)
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            int value = abs(a[i] - a[j]) + abs(i - j);
            maxVal = max(maxVal, value);
        }
    }

    cout << maxVal << endl;
    return 0;
}
```
<img width="1001" height="536" alt="image" src="https://github.com/user-attachments/assets/7b0c0bdd-48c3-4517-affd-d892880593a7" />

## Optimal : Use abs() concept
<img width="889" height="384" alt="image" src="https://github.com/user-attachments/assets/3dbcbef6-633f-45f5-82db-50dcaed571a7" />
<img width="1028" height="443" alt="image" src="https://github.com/user-attachments/assets/9cdae2ee-dba1-4643-af02-a69633a675cf" />

`combine the i'th values and j'th values we get eq's as below`

<img width="901" height="449" alt="image" src="https://github.com/user-attachments/assets/f015779c-fce1-4481-a0b8-99fc8114e739" />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; 
    cin >> n;
    vector<int> a(n);
    for (int i = 0; i < n; i++) cin >> a[i];

    long long ans = 0;

    // We consider 4 cases by rewriting |a[i] - a[j]| + |i - j|
    // Each absolute value combination can be transformed into
    // one of these linear forms:
    //
    // Case 1 (i > j),(a[i] > a[j]):  (a[i]−a[j])+(i−j) => (a[i]+i)−(a[j]+j)  // we treat it as max - min to get the max
    // Case 2 (j > i),(a[i] > a[j]):  (a[i]−a[j])+(j−i) => (a[i]−i)−(a[j]−j)
    // Case 3 (a[j] > a[i]),(i > j):  (a[j]−a[i])+(i−j) => (−a[i]+i)−(−a[j]+j)
    // Case 4 (a[j] > a[i]),(j > i):  (a[j]−a[i])+(j−i) => (−a[i]−i)−(−a[j]−j)
    //
    // So the problem reduces to finding the maximum difference
    // between max and min values of these expressions.

    vector<long long> mx(4, LLONG_MIN), mn(4, LLONG_MAX);

    // Iterate over all elements and compute the 4 linear forms
    for (int i = 0; i < n; i++) {
        long long v1 = a[i] + i;     // Case 1
        long long v2 = a[i] - i;     // Case 2
        long long v3 = -a[i] + i;    // Case 3
        long long v4 = -a[i] - i;    // Case 4

        // Update max and min for each case
        mx[0] = max(mx[0], v1);  mn[0] = min(mn[0], v1);
        mx[1] = max(mx[1], v2);  mn[1] = min(mn[1], v2);
        mx[2] = max(mx[2], v3);  mn[2] = min(mn[2], v3);
        mx[3] = max(mx[3], v4);  mn[3] = min(mn[3], v4);
    }

    // For each case, best answer = max - min
    for (int k = 0; k < 4; k++) {
        ans = max(ans, mx[k] - mn[k]);
    }

    cout << ans << "\n";
}

```


---

# MAIN PROBLEM INTUITION
## BRUTE FORCE : O(n^3)
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n);
    for (int i = 0; i < n; i++) cin >> a[i];

    long long ans = LLONG_MIN;

    // Try all triplets (i, j, k)
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            for (int k = j; k < n; k++) {
                long long val = abs(a[i] - a[j] - a[k]) + abs(i - j - k);
                ans = max(ans, val);
            }
        }
    }
    cout << ans << "\n";
    return 0;
}
```

<img width="956" height="228" alt="image" src="https://github.com/user-attachments/assets/60c9b94b-ce79-40ff-aabc-885aae6028c3" />
<img width="1101" height="392" alt="image" src="https://github.com/user-attachments/assets/d262c044-8b86-4604-b503-dae794b7b0f4" />
<img width="1060" height="137" alt="image" src="https://github.com/user-attachments/assets/2ff54739-0bd3-45e7-9f28-c4ea19b02c6c" />

## OPTIMAL 1  : O(n^2)
<img width="950" height="638" alt="image" src="https://github.com/user-attachments/assets/470b34e4-f113-4c52-be7a-9f30dd8cdda5" />
<img width="951" height="446" alt="image" src="https://github.com/user-attachments/assets/fd6911c2-a5f5-4fa0-9bbd-656fb7b125d1" />
<img width="1060" height="290" alt="image" src="https://github.com/user-attachments/assets/e78dea65-4995-4d3d-b060-f20bedec1a60" />

<img width="949" height="600" alt="image" src="https://github.com/user-attachments/assets/7972189a-d2a1-4c62-9612-e8b29330df58" />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;
    vector<long long> a(n);
    for (int i = 0; i < n; i++) cin >> a[i];

    long long maxPlus = LLONG_MIN, minPlus = LLONG_MAX;
    long long maxMinus = LLONG_MIN, minMinus = LLONG_MAX;

    for (int i = 0; i < n; i++) {
        maxPlus = max(maxPlus, a[i] + i);
        minPlus = min(minPlus, a[i] + i);
        maxMinus = max(maxMinus, a[i] - i);
        minMinus = min(minMinus, a[i] - i);
    }

    long long ans = LLONG_MIN;

    for (int j = 0; j < n; j++) {
        for (int k = 0; k < n; k++) {
            long long S = a[j] + a[k];
            long long T = j + k;

            ans = max(ans, maxPlus - (S + T));
            ans = max(ans, (S + T) - minPlus);
            ans = max(ans, maxMinus - (S - T));
            ans = max(ans, (S - T) - minMinus);
        }
    }

    cout << ans << "\n";
}
```


## OPTIMAL 2 : O(n)
<img width="979" height="677" alt="image" src="https://github.com/user-attachments/assets/67998986-9d4a-4542-bcdc-dc5446cb8887" />
<img width="926" height="350" alt="image" src="https://github.com/user-attachments/assets/70a891f8-3b91-4c23-8e3f-88e2e0749787" />
<img width="920" height="281" alt="image" src="https://github.com/user-attachments/assets/51a642bb-3c9f-4c12-a82e-7e62f651f93e" />

<img width="911" height="162" alt="image" src="https://github.com/user-attachments/assets/0d2cc2f4-f686-4be3-a98d-523cca3cc7d6" />

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main() {
    int n; cin >> n;
    vector<ll> a(n);
    for (int i = 0; i < n; i++) cin >> a[i];

    // Track min/max for each transformed form
    ll max1 = LLONG_MIN, min1 = LLONG_MAX; // a[i] + i
    ll max2 = LLONG_MIN, min2 = LLONG_MAX; // a[i] - i
    ll max3 = LLONG_MIN, min3 = LLONG_MAX; // -a[i] + i
    ll max4 = LLONG_MIN, min4 = LLONG_MAX; // -a[i] - i

    for (int i = 0; i < n; i++) {
        max1 = max(max1, a[i] + i);
        min1 = min(min1, a[i] + i);

        max2 = max(max2, a[i] - i);
        min2 = min(min2, a[i] - i);

        max3 = max(max3, -a[i] + i);
        min3 = min(min3, -a[i] + i);

        max4 = max(max4, -a[i] - i);
        min4 = min(min4, -a[i] - i);
    }

    // Each case corresponds to max(pos) - 2*min(neg) etc.

    ll ans1 = max1 - 2*min1; // case 1:  (a[i]+i) - ((a[j]+j)+(a[k]+k))
    ll ans2 = max2 - 2*min2; // case 2:  (a[i]-i) - ((a[j]-j)+(a[k]-k))
    ll ans3 = max3 - 2*min3; // case 3:  (-a[i]+i) - ((-a[j]+j)+(-a[k]+k))
    ll ans4 = max4 - 2*min4; // case 4:  (-a[i]-i) - ((-a[j]-j)+(-a[k]-k))
    
    ll result = max({ans1, ans2, ans3, ans4});
    cout << result << "\n";
}
```





