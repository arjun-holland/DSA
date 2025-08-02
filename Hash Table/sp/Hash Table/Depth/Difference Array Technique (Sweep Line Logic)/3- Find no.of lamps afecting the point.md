# Problem

<img width="576" height="408" alt="image" src="https://github.com/user-attachments/assets/dae76dae-5f20-437c-a710-113e509a0e28" />
<img width="574" height="458" alt="image" src="https://github.com/user-attachments/assets/831584a2-1fa4-47e9-aa2a-adea260d563c" />
<img width="557" height="349" alt="image" src="https://github.com/user-attachments/assets/0d1660ef-461c-482b-858c-8a68911c5ddf" />
<img width="588" height="569" alt="image" src="https://github.com/user-attachments/assets/051802ba-e1f4-4398-a107-883c2b7ad244" />
<img width="593" height="570" alt="image" src="https://github.com/user-attachments/assets/a4cd9df5-2025-4a11-b1fd-704591378913" />

---
<img width="1073" height="483" alt="image" src="https://github.com/user-attachments/assets/9bb4fff3-fdcd-487b-bae9-66342db8fc27" />

# Brute Force  : Enough for 10^5 only
```
#include <bits/stdc++.h>
using namespace std;

int main(){
    int n;
    cin >> n;
    // vector<pair<int,int>> lamps(n);
    // for(int i=0; i<n;i++){
    //     int s,e;
    //     cin >> s >> e;
    //     lamps[i].push_back({s,e});
    // }
    // int q;cin >> q;
    // vector<int> points(q);
    // for(int &e : points)cin >> e;
    
    vector<int> ans(100000);
    for(int i=0;i<n;i++){
        int s,e;
        cin >> s >> e;
        ans[s] += 1;
        if(e + 1 <= 100000){
            ans[e+1] -= 1;
        }
    }
    for(int i=1;i<=100000;i++){
        ans[i] = ans[i] + ans[i-1];
    }
    
    int q;cin >> q;
    for(int i=0;i<q;i++){
        int p;
        cin >> p;
        cout << ans[p] << " ";
    }
}
```

# Intuition
<img width="1073" height="483" alt="image" src="https://github.com/user-attachments/assets/6e0b320a-3fed-48f9-84b0-1c72681c0689" />
<img width="1019" height="455" alt="image" src="https://github.com/user-attachments/assets/566bfc4f-9020-4c5f-b5ce-94218125d4f9" />
<img width="1064" height="408" alt="image" src="https://github.com/user-attachments/assets/e6ed88b3-e6f7-47f2-91fa-c9ce63223c93" />
<img width="1041" height="410" alt="image" src="https://github.com/user-attachments/assets/03b822e3-9479-4717-adb8-dea43eb7ad0e" />

| `pos` | `delta[pos]` | `curr` (cumulative) | `prefix` entry |
| ----- | ------------ | ------------------- | -------------- |
| 1     | +1           | 1                   | {1, 1}         |
| 3     | +1           | 2                   | {3, 2}         |
| 6     | -1           | 1                   | {6, 1}         |
| 8     | -1           | 0                   | {8, 0}         |
| 10    | +1           | 1                   | {10, 1}        |
| 14    | -1           | 0                   | {14, 0}        |

<img width="1042" height="203" alt="image" src="https://github.com/user-attachments/assets/f7553b9a-b6ac-4bb4-b71c-6a1a5076caa0" />
<img width="1055" height="575" alt="image" src="https://github.com/user-attachments/assets/49045340-01fd-4ce3-b400-54728e245c3e" />
<img width="1023" height="462" alt="image" src="https://github.com/user-attachments/assets/9055e989-bd1a-44bd-905c-203a39791d2c" />
<img width="1059" height="439" alt="image" src="https://github.com/user-attachments/assets/57be9078-252f-468f-9743-acc547b1dfee" />

✅ Visual Timeline Summary
```
Number Line:

0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
    [=======]       ← Lamp 1: 1 to 5
      [========]     ← Lamp 2: 3 to 7
                   [=========]     ← Lamp 3: 10 to 13

Queries:
p=3 → in Lamp 1 & 2 → 2 lamps
p=5 → in Lamp 1 & 2 → 2 lamps
p=10 → in Lamp 3 → 1 lamp
p=15 → after all lamps → 0
```

# Code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    map<int, int> delta;

    // Step 1: Mark +1 at start and -1 at end+1
    for (int i = 0; i < n; ++i) {
        int s, e;
        cin >> s >> e;
        delta[s] += 1;
        delta[e + 1] -= 1;
    }

    // Step 2: Convert to prefix sum
    vector<pair<int, int>> prefix;
    int curr = 0;
    for (auto &[pos, val] : delta) {
        curr += val;
        prefix.emplace_back(pos, curr);
    }

    int q;
    cin >> q;
    while (q--) {
        int p;
        cin >> p;

        // Step 3: Use upper_bound to find greatest pos <= p
        auto it = upper_bound(prefix.begin(), prefix.end(), make_pair(p, INT_MAX));
        if (it == prefix.begin()) {
            cout << 0 << " ";
        } else {
            --it;
            cout << it->second << " ";
        }
    }
    return 0;
}

```




# Submission Link
https://www.jdoodle.com/ga/3%2B8ihQHt%2FMhzqpRR5xUwlA%3D%3D
