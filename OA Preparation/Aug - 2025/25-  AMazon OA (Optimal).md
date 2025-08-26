# PROBLEM
<img width="604" height="504" alt="image" src="https://github.com/user-attachments/assets/9e12336a-b520-4327-be42-4104595ba038" />
<img width="543" height="542" alt="image" src="https://github.com/user-attachments/assets/761d3ed6-7492-41e5-9462-8ae528572c8e" />

# Intuition
<img width="1007" height="571" alt="image" src="https://github.com/user-attachments/assets/476ba355-f60f-4520-a811-57f414efe4db" />


# Optimal CODE
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    string data;
    cin >> data;

    // Make string 1-indexed (to match multiset positions)
    data = '0' + data;

    // 26 multisets (for each character)
    // g[1] = positions of 'a', g[2] = positions of 'b', ..., g[26] = 'z'
    multiset<int> g[27];
    for (int i = 1; i <= n; i++) {
        int u = data[i] - 'a' + 1;   //b-a+1 = 2 as we follow 1-based index
        g[u].insert(i);    //contains wher u character is present in data
    }

    int k;
    cin >> k;
    while (k--) {
        int type;
        cin >> type;

        if (type == 1) {
            // Update query: change character at position "pos" to new character
            int pos, y;
            cin >> pos >> y;

            // Remove old character from its multiset
            int oldChar = data[pos] - 'a' + 1;  //old char 1 based index , c-a+1 =>3 : a, b, c
            g[oldChar].erase(g[oldChar].find(pos));

            // Update string
            data[pos] = char('a' + y - 1);  //new char follows 0 based index so -1

            // Insert new character position in its multiset
            g[y].insert(pos);
            
            //cout << data << endl;
        } 
        else {
            // Count distinct characters in substring [l, r]
            int l, r;
            cin >> l >> r;
            int distinctCount = 0;

            // Check each character a..z (1..26)
            for (int ch = 1; ch <= 26; ch++) {
                // Find position <= r
                auto it = g[ch].upper_bound(r);
                if (it == g[ch].begin()) continue; // no positions <= r

                --it; // last occurrence <= r
                int pos = *it;
                if (pos >= l) {
                    distinctCount++; // character ch exists in [l,r]
                }
            }
            cout << distinctCount << "\n";
        }
    }

    return 0;
}
```
# RUN HERE
https://ideone.com/XEfR0f

# Time Complexity : O(log n)
# Space Complexity : O(n)
