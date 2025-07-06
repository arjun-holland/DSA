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
i.e, To minimize the total dot product:
Sort a in ascending order
Sort b in descending order
```

# How to know if it is correct ?

 To minimize the total dot product:
Sort a in ascending order : a1 <= a2 <= a3 <= .... >= an
Sort b in descending order : b1 >= b2 >= b3 >= .... >= bn

# Method of Contraductcion
```
To prove our statement true
let's assume that it's false and try to prove that its false,
if we fail then our contraduction is false,
so our statement is true.

-> Try to prove it false -> if you fail to do so -> it means your original argument is correct 

If this is correct sum1 = a1*b1 + a2*b2 + a3*b3 + a4*b4 + a5*b5 
                                    = g + a2*b2 + a4*b4 

Attack argument (to prove its false) :- It will be best only if you swap (a2,a4) {Two elements swap}

Sum 2 = a1*b1 + a4*b2 + a3*b3 + a2*b4 + a5*b5  = g + a4*b2 + a2*b4

If sum1 <= sum2 ; it means even doing 1 swap will destroy your minimum answer hence proved your original argument is correct 

=> d = sum2 - sum1 if it >=0 then your original argument is correct

-> d = (a4-a2)*(b2-b4) >=0

that even if u attack u can not reduce the sum than the initial sum. 
```
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
