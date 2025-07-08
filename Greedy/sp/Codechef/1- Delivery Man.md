# Problem
```
Andy and Bob are the only two delivery men of Pizza-chef store. Today, the store received N orders.
It's known that the amount of tips may be different when handled by different delivery man. More specifically,
if Andy takes the ith order, he would be tipped Ai dollars and if Bob takes this order, the tip would be Bi dollars.
They decided that they would distribute the orders among themselves to maximize the total tip money.
One order will be handled by only one person. Also, due to time constraints Andy cannot take more than X orders and Bob cannot
take more than Y orders. It is guaranteed that X + Y is greater than or equal to N, which means that all the orders can be
handled by either Andy or Bob.
Please find out the maximum possible amount of total tip money after processing all the orders.

Input
The first line contains three integers N, X, Y.
The second line contains N integers. The ith integer represents Ai.
The third line contains N integers. The ith integer represents Bi.

Output
Print a single integer representing the maximum tip money they would receive.

Constraints
All test:
1 ≤ N ≤ 10^5
1 ≤ X, Y ≤ N;
X + Y ≥ N
1 ≤ Ai, Bi ≤ 10^4
```

# Brute Force Intuition
```
💥 Brute Force Intuition – Complete Version
We’re given: N orders Andy can take at most X orders,Bob can take at most Y orders
Tip for each order differs based on who delivers:
      Andy's tips = A[0...N-1]
      Bob's tips = B[0...N-1]
Our goal: Assign each order to either Andy or Bob such that: No one exceeds their max limit and Every order is assigned and
The total tips are maximized
```
✅ Brute Force Plan:
![image](https://github.com/user-attachments/assets/dd09e407-d232-47bf-8919-9a81bda101e6)

# Brute Force Code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);

    int n, x, y;
    cin >> n >> x >> y;

    vector<int> a(n), b(n);
    for (int &val : a) cin >> val;
    for (int &val : b) cin >> val;

    int max_tip = 0;

    for (int i = 0; i <= n; ++i) {
        if (i <= x && (n - i) <= y) {
            // Step 1: compute gain for Andy taking each order
            vector<pair<int, int>> gain_with_index;
            for (int j = 0; j < n; ++j) {
                gain_with_index.push_back({a[j] - b[j], j});
            }

            // Step 2: sort by gain descending (max gain for Andy comes first)
            sort(gain_with_index.rbegin(), gain_with_index.rend());

            vector<bool> assigned(n, false); // track who gets the order
            int total_tip = 0;

            // Step 3: Assign top i orders to Andy
            for (int k = 0; k < i; ++k) {
                int idx = gain_with_index[k].second;
                total_tip += a[idx];
                assigned[idx] = true;
            }

            // Step 4: Assign rest to Bob
            for (int j = 0; j < n; ++j) {
                if (!assigned[j]) {
                    total_tip += b[j];
                }
            }

            // Step 5: track the max tip value
            max_tip = max(max_tip, total_tip);
        }
    }
    cout << max_tip << "\n";
    return 0;
}

```


# Optimal Intuition
```
We have: N orders.
Two people: Andy and Bob.
For each order product i:
If Andy delivers → we get A[i] tips.
If Bob delivers → we get B[i] tips.

✅ Goal:
Maximize total tips, but: Andy can take at most X orders and Bob can take at most Y orders.
X + Y ≥ N → All orders will be delivered, just need to choose wisely who does which.

💡 Core Idea
We want to assign orders in such a way that we maximize the tip difference (gain) by selecting the better person for each order.
But we're constrained by X and Y.
```
```
Let's Build the Intuition:
- Base Case: Suppose Bob delivers all orders → total tips = sum(B).
- Now for each order, check:
      If Andy delivers instead, how much extra tip do we get? → diff[i] = A[i] - B[i]
              sum(B) + A[i] - B[i] as in total bobs tips we add the specific i'th product tip of andy and remove that product bob's tip
      If diff[i] is positive, it’s better to give that order to Andy.
        Highest positive gain = Andy is much better
        Negative gain = Bob is better
        If gain is high → Andy should deliver
        If gain is low → Bob should deliver

- But we can only give X orders to Andy.
- So, sort diff[] in descending order:
- Take top X values (the largest gains from switching Bob → Andy) Add those gains to base case (sum(B)).
```
![image](https://github.com/user-attachments/assets/4dda262a-42c1-4091-b7dc-19beaffa4480)

# Code
```
#include <bits/stdc++.h>              // Includes all standard libraries
using namespace std;
typedef long long int ll;            // Defines 'll' as shorthand for long long int

int main() {
    ios::sync_with_stdio(false);     // Speeds up input/output by unsyncing with C I/O
    cin.tie(0);                      // Unties cin from cout for faster I/O

    int n, x, y;                     // n = total orders, x = max Andy can take, y = max Bob can take
    cin >> n >> x >> y;             // Read input values

    vector<int> a(n), b(n);          // a = Andy's tips per order, b = Bob's tips per order
    for (int &i : a) cin >> i;       // Read all of Andy's tips
    for (int &i : b) cin >> i;       // Read all of Bob's tips

    int sum = 0;                     // Initialize base total tip assuming all orders handled by Bob
    vector<int> dif(n);              // dif[i] = a[i] - b[i] → benefit of assigning i-th order to Andy instead of Bob

    for (int i = 0; i < n; i++) {
        sum += b[i];                 // Add Bob's tip for every order to base sum
        dif[i] = a[i] - b[i];        // Calculate tip difference if Andy took the order
    }

    sort(dif.rbegin(), dif.rend()); // Sort differences in descending order (max gain by giving to Andy comes first)

    vector<int> prf(n + 1, 0);       // Prefix sum array to store sum of top i differences
    for (int i = 1; i <= n; i++) {
        prf[i] = prf[i - 1] + dif[i - 1]; // prf[i] = sum of top i differences (Andy gains)
    }

    int max_amt = 0;                 // To track maximum total tip amount possible

    for (int i = 0; i <= n; i++) {   // Try all values where Andy takes 'i' orders
        // i = number of tasks Andy takes
        // n - i = tasks Bob takes
        if (i <= x && (n - i) <= y) {         // Check if this split is valid (Andy ≤ x and Bob ≤ y)
            int cur_tot = sum + prf[i];       // Total tip = Bob's base sum + Andy's extra gain on top i orders
            max_amt = max(max_amt, cur_tot);  // Update max if this combination gives better total
        }
    }
    cout << max_amt;                 // Output the maximum total tip amount
}

```
