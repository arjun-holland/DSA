# Problem
Given two arrays a and b -> can contain negative elements. 
Minimize summation of a[i]*b[i] overall i -> you are allowed to re-arrange a and b in any order  

# Intuition
```
You are given two arrays a and b, both of size N.
You can rearrange both arrays however you like.
Your task: Minimize
     n-1
     ∑  {a[i]⋅b[i]} = minimum
    i=0
✅ Greedy Intuition
Sort your first array in ascending order and second array in descending order -> or vice versa;
then find your answer it will be always minimum.
i.e, To minimize the total dot product:
Sort a in ascending order
Sort b in descending order
```
# Why it works?
Pairing the smallest a[i] with the largest b[i] (and so on) keeps products small or negative,then pairing largest and largest number, hence minimizing the total.

# code
```
#include <iostream>
#include <vector>
#include <algorithm>  // for sort()

using namespace std;

int minimizeProductSum(vector<int>& a, vector<int>& b) {
    int n = a.size();

    sort(a.begin(), a.end());                    // Sort 'a' in ascending order
    sort(b.begin(), b.end(), greater<int>());   // Sort 'b' in descending order

    int total = 0;
    for (int i = 0; i < n; ++i) {
        total += a[i] * b[i];
    }
    return total;
}

int main() {
    int n;
    cout << "Enter size of arrays (N): ";
    cin >> n;
    vector<int> a(n), b(n);
    cout << "Enter elements of array A:\n";
    for (int i = 0; i < n; ++i) {
        cin >> a[i];
    }
    cout << "Enter elements of array B:\n";
    for (int i = 0; i < n; ++i) {
        cin >> b[i];
    }
    int result = minimizeProductSum(a, b);
    cout << "Minimum Sum of Products: " << result << endl;
    return 0;
}
 ```
# 🔍 Greedy Property Justification
The pairing ensures that large positive/negative values are dampened when paired with small values of opposite sign.
This follows the greedy choice property and leads to the global minimum.
