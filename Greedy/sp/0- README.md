# Greedy Algorithm 
## 📚 What is a Greedy Algorithm?

A **Greedy Algorithm** is an approach to solving problems by making the **locally optimal choice at each step** with the hope that this leads to the globally optimal solution.

Greedy algorithms are ideal for problems where choosing the best option at each step leads to an overall optimal result.

---

## 🧠 Key Concepts

- **Greedy Choice Property**: A global optimum can be arrived at by selecting a local optimum.
- **Optimal Substructure**: An optimal solution to the problem contains optimal solutions to subproblems.

---

## 🧪 Example Problems

| Problem Name                 | Description                                    |
|-----------------------------|------------------------------------------------|
| Activity Selection          | Choose max non-overlapping intervals          |
| Fractional Knapsack         | Maximize value with divisible items           |
| Huffman Coding              | Compression using greedy tree construction    |
| Job Sequencing with Deadlines | Maximize profit in job scheduling           |
| Coin Change (Greedy version)| Use fewest coins (not always optimal)         |

---

## ✅ Use a Greedy Algorithm When:
# Greedy Choice Property Holds
- Making a locally optimal choice at each step leads to a globally optimal solution.
- Example: In the Activity Selection Problem, choosing the earliest finishing activity at each step ensures the maximum number of non-overlapping activities.

#  Optimal Substructure Exists
- A problem has an optimal substructure if an optimal solution to the whole problem includes optimal solutions to its subproblems.
- Example: In the Fractional Knapsack Problem, taking the item with the highest value-to-weight ratio at every step leads to the optimal solution.

# 3. Problem Requires Fast, Approximate Solutions
- Even if the greedy algorithm doesn’t always give the best result, it’s often good enough and very fast.
- Example: In graph coloring or scheduling, greedy approaches provide fast heuristics for large data sets where optimal methods are too slow.

# 4. No Overlapping Subproblems
- If the problem doesn’t revisit the same subproblems multiple times (unlike DP), greedy may be preferable.

## ❌ When NOT to Use Greedy:
- When the greedy choice leads to a suboptimal global solution.
- Problems like 0/1 Knapsack, Longest Common Subsequence, or Matrix Chain Multiplication require dynamic programming.

## 🧪 How to Verify Greedy Applicability:
```
Ask yourself:
Can I make a series of local decisions that build toward a global solution?
Does this problem have greedy choice property and optimal substructure?
Can I prove that the greedy approach is always optimal for this problem?
If yes, greedy is likely a solid choice.
```
        ┌───────────────────────────────┐
        │ Does the problem have         │
        │ Optimal Substructure?         │
        └──────────────┬────────────────┘
                       │ Yes
                       ▼
        ┌───────────────────────────────┐
        │ Can you make a greedy choice  │
        │ at each step that feels       │
        │ locally best?                 │
        └──────────────┬────────────────┘
                       │ Yes
                       ▼
        ┌───────────────────────────────┐
        │ Is the greedy choice always   │
        │ part of an optimal solution?  │
        └──────────────┬────────────────┘
                       │ Yes
                       ▼
               ┌───────────────────────┐
               │✅Use Greedy Algorithm │
               └───────────────────────┘
                       │
                     No|
                       ▼
               ┌───────────────────────---- ┐
               │ ❌ Try Dynamic Programming│
               └───────────────────────---- ┘




