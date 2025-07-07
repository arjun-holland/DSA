# problem
```
During a break in the buffet of the scientific lyceum of the Kingdom of Kremland, there was formed a queue of n high school students
numbered from 1 to n. Initially, each student i is on position i. Each student i is characterized by two numbers — ai and bi.
Dissatisfaction of the person i equals the product of ai by the number of people standing to the left of his position, add the product bi
by the number of people standing to the right of his position. Formally, the dissatisfaction of the student i, which is on the position j,
equals ai⋅(j−1)+bi⋅(n−j).
The director entrusted Stas with the task: rearrange the people in the queue so that minimize the total dissatisfaction.
Although Stas is able to solve such problems, this was not given to him. He turned for help to you.
```
# Input
```
The first line contains a single integer n (1≤n≤10^5) — the number of people in the queue.
Each of the following n lines contains two integers ai and bi (1≤ai,bi≤10^8) — the characteristic of the student i,
initially on the position i.
```
# Output
Output one integer — minimum total dissatisfaction which can be achieved by rearranging people in the queue.

---


# Intuition :

![image](https://github.com/user-attachments/assets/06802aab-fbfe-4e35-85b2-1773699424af)

- When we have a formula or expression, the first goal is to simplify it.
- By simplifying the dissatisfaction formula:  ∑[j=1 to n] (aⱼ · (j - 1) + bⱼ · (n - j))
- it becomes: -∑aᵢ + n·∑bᵢ  → this part is a constant across all permutations
- So for example: sum = -a₁ - a₂ - a₃ + b₁*n + b₂*n + b₃*n
- Then, another important term comes from: ∑[j=1 to n] j · (aⱼ - bⱼ) which varies based on the ordering of students.

# Hence, the key greedy insight:
- Compute and store (aᵢ - bᵢ) for each student.
- Sort these values in descending order.
- Weight them with j (1 to n) to minimize dissatisfaction.

# code 
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main() {
    ll s = 0;              // This will store the total dissatisfaction
    vector<ll> a;          // Vector to store (aᵢ - bᵢ) for each student
    ll n;
    cin >> n;              // Read number of students

    // Step 1: Read input and compute initial sum offset
    for (int i = 0; i < n; i++) {
        int av, bv;
        cin >> av >> bv;   //  student i is characterized by two numbers

        // Accumulate constant value of total dissatisfaction: -∑aᵢ + n * ∑bᵢ
        s = s - av + bv * n;

        // Store (aᵢ - bᵢ) to decide ordering in greedy step
        a.push_back(av - bv);
    }

    // Step 2: Greedy ordering
    // Sort students by (aᵢ - bᵢ) in descending order
    // This ensures that students who suffer more from being later are placed earlier in the queue
    sort(a.rbegin(), a.rend());

    // Step 3: Accumulate final weighted dissatisfaction
    for (int j = 1; j <= n; j++) {
        // We already added -∑aᵢ + n∑bᵢ
        // Now add: ∑ j * (aᵢ - bᵢ)
        s = s + j * a[j - 1];
    }

    // Final output: total dissatisfaction
    cout << s;
    return 0;
}
```
#  what's constant and what's variable?
| Term              | Changes with student position (order)?  | Why?                                                                        |
| ----------------- | --------------------------------------  | --------------------------------------------------------------------------- |
| `-∑aᵢ`            | ❌ No                                   | Only depends on values of `a`, not their positions                          |
| `n * ∑bᵢ`         | ❌ No                                   | Only depends on values of `b`, not their positions                          |
| `∑ j · (aᵢ - bᵢ)` | ✅ Yes                                  | `j` depends on the student's **position**, which you are trying to optimize |

- aᵢ and bᵢ values vary per student ✅
- But -∑aᵢ + n·∑bᵢ is structurally constant across permutations ❌ like it does not chnage in all permutaions
- Only ∑ j · (aᵢ - bᵢ) changes with how you order the students 💡
- So we design the algorithm to minimize that variable part.

