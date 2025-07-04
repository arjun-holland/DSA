# 🌲 DP on Trees — Concepts & Tricks

---

## 🚀 How to Solve DP on Tree Problems?

Dynamic Programming (DP) on trees is all about processing **Bottom-Up-Traversal**. This means:

- ✅ Start with the **leaf nodes**.
- 🪜 Then move **upward** using recursion.
- 🧠 The **answer for a node** depends on the **answers from its children**.

---

## 🔐 Trick 1 — Bottom-Up Calculation

> "Always calculate the answer for bottom nodes first. Then start moving up."

- This is because **answers from children** are **required** to compute answers for the parent.
- Avoid computing parent node values **before** children are solved.

---

### 📜 Tanvir Singh's Law

> “The answer to a node can only be calculated **after** the answers of all its children have been calculated.”

---

## 🧩 Sample Problem — Compute Height of Each Node in a Tree

> Given a tree with **N** nodes (rooted at Node `1`), calculate the **height of each node**.

### 📘 Definition:

- **Height of a node `x`** = Longest path from node `x` **down to any leaf**.
- Leaf node → Height = `0` (in **edges**).

---

### 🧠 Tiju's Law

> “Height of a node is the longest distance from the current node to any leaf.”

---

### 📐 Height Formula

```text
Height[i] = 1 + max(height[c1], height[c2], ..., height[ck])
