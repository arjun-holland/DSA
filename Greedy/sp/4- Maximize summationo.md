# Problem
Given two arrays a and b -> can contain negative elements. 
Maximize summation of a[i]*b[i] overall i -> you are allowed to re-arrange a and b in any order  

# Intuition
```
You are given two arrays a and b, both of size N.
You can rearrange both arrays however you like.
Your task: Maximize
     n-1
     ∑  {a[i]⋅b[i]} = Maximize
    i=0
✅ Greedy Intuition
Sort your first array in ascending order and second array in descending order -> or vice versa;
then find your answer it will be always Maximize.
i.e, To Maximize the total dot product:
Sort a in descending order
Sort b in descending order
```
# Why it works?
Pairing the largest a[i] with the largest b[i] (and so on) keeps products large as possible always compare than other pairinglike smallest and largest number, hence maximizing the total.

# code
```
#include <iostream>
#include <vector>
#include <algorithm>  // for sort()

using namespace std;

int MaximizeProductSum(vector<int>& a, vector<int>& b) {
    int n = a.size();

    sort(a.begin(), a.end(), greater<int>());   // Sort 'a' in descending order
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
    int result = MaximizeProductSum(a, b);
    cout << "Maximize Sum of Products: " << result << endl;
    return 0;
}
 ```

