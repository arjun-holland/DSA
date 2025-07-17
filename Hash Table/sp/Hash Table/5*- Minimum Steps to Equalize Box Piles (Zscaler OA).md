# 📦 Minimum Steps to Equalize Box Piles (Amazon OA)
## 🔍 Problem Statement
```
Alex has n piles of boxes with varying heights. In each step, Alex can remove any number of boxes from the tallest pile to
reduce its height to match the next tallest pile.
Determine the minimum number of steps required to make all piles equal in height.

🧾 Function Signature
        long pilesOfBoxes(vector<int> boxesInPiles);

Returns:
    long: the minimum number of steps required to make all piles the same height
```
## 📘 Constraints
```
1 ≤ n ≤ 2×10^5
1 ≤ boxesInPiles[i] ≤ 2×10^6
```
 
## ✅ Sample Input
```
5
4 5 5 2 4
Which forms:
boxesInPiles = [4, 5, 5, 2, 4]
```
## 📤 Sample Output
6
## 🧾 Explanation
```
Step-by-step breakdown:
Lower both 5s to 4 → [4, 4, 4, 2, 4] -> 2 steps
Lower three 4s to 2 → [2, 2, 2, 2, 2] -> 4 steps
Lower four 2s to match smallest 2 → all equal
✅ Final array = [2, 2, 2, 2, 2]
✅ Total Steps = 6
```
## //Brute force solution :-> 
```
-> Find largest element of array and second largest element of array -> O(N.) 
-> Let say largest element is at index “i” -> b[i] = second largest 
-> Keep doing this until all array elements become equal 
-> O(N*N.)  

-> u = 0
while(u==0){
  -> largest(b) 
  -> second_largest(b) 
  -> b[i] = second_largest 

  -> if all array elements are equal u = 1  
}
```
## //Optimal way:
```
int main() {
    int n;
    cin >> n;     // Input size of the array (excluding b[0])   as 1 based index
    
    vector<int> b(n + 1, 0);    // Initialize the b array of size n + 1, with all elements 0
    map<int, int> k;     // Map to store frequency of elements

    // Input array b (index 1 to n) as 1 based index
    for (int i = 1; i <= n; i++) {
        cin >> b[i];  
    }

    // Count frequency of each element in b
    for (int i = 1; i <= n; i++) {
        k[b[i]] += 1;  // Increment frequency of b[i] in map k
    }

    // Create a vector of pairs to store (element, frequency)
    vector<pair<int, int>> g;
    for (auto u : k) {
        g.push_back({u.first, u.second});  // Insert element and its frequency into vector g
    }

    int size = g.size();
    int step = 0;     // Initialize step variable to 0

    // Traverse the vector g backward and calculate the steps
    for (int i = size - 1; i >= 1; i--) {
        g[i - 1].second += g[i].second;        // Add frequency of g[i] to g[i-1]
        step += g[i].second;               // Increment step by the frequency of g[i]
        g[i].second = 0;                 // Reset frequency of g[i] to 0
    }

    // Output the result
    cout << step << endl;

    return 0;
}
```

TC - O(N*logn) -> SortedMap 
Takes O(N.) size space. 





