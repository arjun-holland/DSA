# 📦 Black Box: "Count All Pairs"
```
✅ Problem Pattern
Given multiple independent groups of sizes:  Arr = [a, b, c, d, ...]

You want to count all pairs (i, j) such that:
  i and j are from different groups
  Order doesn’t matter: (i, j) and (j, i) are same (i.e., undirected)

```
<img width="871" height="410" alt="image" src="https://github.com/user-attachments/assets/1d5e63c3-a672-471c-90ea-ece40dd176df" />
<img width="853" height="111" alt="image" src="https://github.com/user-attachments/assets/819ffde3-d8d8-48bb-b21d-ba6fef8fd725" />

---

<img width="879" height="464" alt="image" src="https://github.com/user-attachments/assets/94994353-7112-4cd9-ab37-cfcdfd8a99a1" />
<img width="870" height="285" alt="image" src="https://github.com/user-attachments/assets/6c824b2f-58c5-4427-89b5-b98f3155a430" />
<img width="867" height="356" alt="image" src="https://github.com/user-attachments/assets/69f42f99-9925-483a-bdb6-a33540efb151" />
<img width="837" height="99" alt="image" src="https://github.com/user-attachments/assets/bb56febc-510f-463c-8de7-06888ce91ef7" />

---

<img width="769" height="432" alt="image" src="https://github.com/user-attachments/assets/de812c7b-be16-4578-82eb-c5d783f6cfeb" />
<img width="726" height="422" alt="image" src="https://github.com/user-attachments/assets/55f84fbc-a25f-417e-8cfc-0863896d9259" />
<img width="760" height="319" alt="image" src="https://github.com/user-attachments/assets/170045b7-5e0b-43bd-b59e-1d70e8dd4f7b" />
<img width="755" height="512" alt="image" src="https://github.com/user-attachments/assets/26cddf43-dc9d-468d-bce5-09a9571cd991" />
<img width="769" height="346" alt="image" src="https://github.com/user-attachments/assets/dc393a11-1235-44e9-ac88-322399be2c50" />


---
🛠️ Use Cases

| Scenario                       | Can You Use This Trick?  |
| ------------------------------ | ------------------------ |
| Tree with node partitions      | ✅ Yes                    |
| Graph components               | ✅ Yes                    |
| Disjoint sets of people/groups | ✅ Yes                    |
| DP on separate groups          | ✅ Yes                    |
| Groups overlap (non-disjoint)  | ❌ No                     |
| Counting within same group     | ❌ No                     |
| Counting **ordered** pairs     | ⚠️ Use `2 * c * cur_sum` |
