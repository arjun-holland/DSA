# Problem 
![image](https://github.com/user-attachments/assets/4c769542-6561-4099-b325-2c56ded7c15d)
```
Context: You’re working on a simulation tool at Atlassian that manages a network of islands connected by bridges. Initially, every island is connected to every other island. Each island has an "importance value" associated with it.
A malicious agent, Alex (an Atlassian engineer), can destroy some bridges between islands, but only if the total destruction cost remains within a given budget. The cost to destroy the bridge between island i and island j is importance[i] * importance[j].
Your colleague Jordan (an Atlassian employee) lives on island 1 and enjoys visiting other islands. After Alex destroys some bridges optimally to disconnect the network, we want to determine how many islands Jordan can still access, including his own.

🧩 Problem Statement: You are given:
An integer N — the number of islands.
An array A of length N, where A[i] is the importance of the i-th island (1-indexed).
A long integer C — the maximum total cost Alex can spend to destroy bridges.
Each island is initially connected to every other island. Your task is to compute the minimum number of islands (including island 1) that Jordan can access after Alex destroys bridges optimally (to minimize the size of the connected component that contains island 1).

🧾 Input:
First line: integer T — number of test cases.
For each test case:
Line 1: Two integers N and C.
Line 2: N integers A[1] A[2] ... A[N] — importance values.

📤 Output: For each test case, output the minimum number of islands (including island 1) Jordan can visit
```

# Intuition
# To Remove one Node
![image](https://github.com/user-attachments/assets/50d41bba-a144-48ed-af6c-cf05cf80dbd5)

# To Remove two Nodes
![image](https://github.com/user-attachments/assets/a348b21c-587a-4788-bbb9-42fa7efe2eca)
```
🧩 Key Insight:
To disconnect Jordan from as many islands as possible, Alex should aim to isolate certain islands (cut all their bridges),
as cheaply as possible, while respecting the budget C.
We simulate this as follows:
```

![image](https://github.com/user-attachments/assets/36b8395d-267d-4d0b-ab3b-d328ddc6fbf6)

![image](https://github.com/user-attachments/assets/799380d2-aa8e-4719-966d-dbbb0e77d686)

```
     (Disconnected nodes sum) * ((Total nodes sum) - (Disconnected nodes sum))
i.e:  y * (x - y) where x is constant
      => yx - y^2
  This is a quadratic function in (y), opening downward (since -y² is the dominating term).
  So the curve is a parabola with a maximum at y = x/2.
```
![image](https://github.com/user-attachments/assets/552e1c8e-427c-4eca-9f68-f84424dd363f)

![image](https://github.com/user-attachments/assets/a5150593-4948-40b3-9d8d-cec372420414)


![image](https://github.com/user-attachments/assets/bc2bfa78-95ea-4f0d-86c4-0a81ead7eb30)
```
🔵 What’s the graph trying to tell you?
    It draws a hill (like a mountain 🏔️):
    At y = 5, the top of the hill → the expression is maximum ❌
    (BAD! You want to avoid this area)
    At y = 0 or y = 10, the expression is at the bottom → value is minimum ✅
    (GOOD! You want to aim for this!)

✨ Now the key question:
“How do I find such a 'y' from my array?”
    Trying all possible y means trying all groups of elements — which is slow!
    But the graph gives you a clue:
    🤔 “Hey, the best values are at the two ends (y near 0 or y near x). Why not just try there?”
    That's the greedy aha! moment.

✅ So the greedy idea from the graph is:
Instead of checking all possible groups (which gives many y values between 0 and x):
    Just try the values of y that are close to the ends of the curve — like:
    Smallest sum group → y near 0
    Largest sum group → y near x
Those will give small expression values, because they’re at the bottom of the hill.

🔁 For code:
Your greedy steps are:
    Sort the array
    Try taking the smallest do_it elements → gives y near 0
    Try taking the largest do_it elements → gives y near x
    Check if either gives a product ≤ c
This is exactly what the graph suggests! 🎯

```
![image](https://github.com/user-attachments/assets/f225acb2-e4fc-43f1-94c4-849e40b4ae52)

---
# Dry Run

![image](https://github.com/user-attachments/assets/d559a5ef-5ae2-42c2-9d19-ec11b54b2cb3)

![image](https://github.com/user-attachments/assets/fb586729-d7c3-4ea1-b6d2-8f52ac2f74f7)

# Code
```
#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

int main() {
    ll t;
    cin >> t;  // Number of test cases

    while (t--) {
        ll n, c;
        cin >> n >> c;  // n = number of islands, c = destruction budget

        ll b[n + 1] = {0};  // 1-indexed array to store importance of each island (Value of node)
        ll sum = 0;         // To store total sum of all importances

        // Read importance values for each island and calculate total sum
        for (ll i = 1; i <= n; i++) {
            cin >> b[i];
            sum += b[i];
        }

        // We sort only islands from 2 to n (excluding island 1) Jordan is present at 1 and observe islans what he can see so we never disconnect island 1
        sort(b + 2, b + n + 1);

        ll answer = 0;  // This keeps track of the maximum number of islands Alex can remove

        // Try to disconnect 1, 2, ..., up to n-1 islands
        for (ll do_it = 1; do_it <= n - 1; do_it++) {  // can remove from 1 to n-1  nodes cus we cant remove node 1
            ll sum2 = 0;

            // Case 1: Try removing the `do_it` smallest islands (excluding island 1)
            for (ll j = 2; j <= 2 + do_it - 1; j++) {
                sum2 += b[j]; //disconnected node value sum 
            }

            // Calculate the cost of removing these nodes: (sum2)*(sum of rest) => (sum2)*(sum - sum2) 
            ll u1 = (sum2) *  (sum - sum2) ;

            sum2 = 0;  // Reset sum2 for next case

            // Case 2: Try removing the `do_it` largest islands
            for (ll j = n; j >= n - do_it + 1; j--) {
                sum2 += b[j];
            }

            // Calculate cost again for this set
            u1 = min(u1, (sum2) * (sum - sum2));  // Pick the cheaper of the two cases

            // If the cost is within the allowed budget, update answer
            if (u1 <= c) {
                answer = do_it;
            }
        }

        // Final result = total islands - number of islands Alex can optimally disconnect Because those are the ones Jordan can still access
        cout << (n - answer) << "\n";
    }

    return 0;
}
T.C : O(NlogN * N^2)
```
