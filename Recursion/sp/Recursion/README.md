# 🌀 Recursion 
## 📘 What is Recursion?

Recursion is a method of solving a problem where the solution depends on solving smaller instances of the same problem. 
A recursive function is a function that calls itself to break down problems into simpler sub-problems.

> “To understand recursion, one must first understand recursion.” – Anonymous

---

## 🧠 How It Works

A recursive function typically has:
1. **Base Case** – Condition under which the recursion ends.
2. **Recursive Case** – The part where the function calls itself.

## 🧾 Pseudo Code of Recursion (Generic Form)
```
function recursiveFunction(parameters):
    if (base condition is true):       //parameters reach the base condition
        return result
    else:
        perform some operation
        return recursiveFunction(modified parameters)
```
---
##  ✅ When to Use Recursion
When we need to know all possibilities in a problem to came up with final answer
- 📈 Good Use Cases: 
- Problems with sub-problems: Like divide and conquer (Merge Sort, Quick Sort).
- Tree and Graph traversals: e.g., DFS, Inorder/Preorder/Postorder traversal.
- Backtracking problems: Like N-Queens, Maze solving, Sudoku.
- Mathematical calculations: Factorial, Fibonacci, GCD, etc.


## 🧠 Core Concepts of Recursion
```
        int factorial(int n) {
          if (n == 0) return acc;
          return n * factorial(n - 1); 
        }
```
# 1. ✅ Base Case
```
The condition that stops the recursive calls.
Without it, you'll get an infinite loop → stack overflow.

`if (n == 0) return 1;`  // Example base case for  factorization
```
## 2. 🔁 Recursive Case
```
The function calls itself with a modified input.
This continues until the base case is hit.

`return n * factorial(n - 1);`  // Recursive case fro factorization
```
## 3. 🪜 Call Stack and Stack Frames
- Each recursive call is stored in the call stack.
- A stack frame holds the function's local variables and state
- The deeper the recursion, the more memory it uses.
🛑 Too many recursive calls = Stack Overflow

## 4. 🔄 Direct vs Indirect Recursion
```
`Direct`  	Function calls itself directly	func() → func()
`Indirect`	Function A calls B, B calls A	A() → B() → A()
```

## 5. 🪃 Tail Recursion
```
When the recursive call is the last operation in the function.
Tail-recursive functions can be optimized by compilers to reuse stack frames (called Tail Call Optimization, though not guaranteed in C++).

✅ Example (Tail-Recursive Factorial):
int factorialTail(int n, int acc = 1) {
    if (n == 0) return acc;
    return factorialTail(n - 1, n * acc);  // tail call
}

Compare this with the non-tail version:

int factorial(int n) {
    if (n == 0) return 1;
    return n * factorial(n - 1);  // not tail-recursive
}
```
## 6. 🧩 Memoization (Top-Down Dynamic Programming)
```
Store results of recursive calls to avoid redundant computation.
Especially useful in problems like Fibonacci or DP.

int fib(int n, vector<int>& memo) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];
    return memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
}
```
## 7. 📥 Recursion Tree
```
Visual representation of recursive calls branching out.
Helps in analyzing time complexity.

Example:
fib(4) calls fib(3) 
→ fib(3) calls fib(2) 
→ and so on… until base case
```
## 8. 🚨 When Recursion Is Bad
- Too deep? Risk of stack overflow.
- Too many repeat calls? Use memoization or switch to iteration.
- Tail recursion is not always optimized in C++, unlike languages like Haskell.

## 📋 Summary Table of Key Concepts
| Concept            | Description                             | Use Case / Tip                                 |
| ------------------ | --------------------------------------- | ---------------------------------------------- |
| Base Case          | Terminates recursion                    | Always needed to avoid infinite loop           |
| Recursive Case     | Problem reduces and function calls self | Logic that solves a part and recurses          |
| Tail Recursion     | Last action is the recursive call       | Optimizable (but not in all compilers)         |
| Indirect Recursion | Functions call each other recursively   | Used in complex mutual behaviors               |
| Memoization        | Cache results to avoid repeat work      | Boosts performance for overlapping subproblems |
| Call Stack         | Tracks function calls in memory         | Avoid deep recursions                          |
| Recursion Tree     | Shows how calls branch                  | Helps analyze complexity                       |


🔍 **Chart Tip:** When visualizing recursive calls, a call stack diagram (or tree) is incredibly helpful to trace the function execution and returns.
