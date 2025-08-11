# Problem
<img width="599" height="672" alt="image" src="https://github.com/user-attachments/assets/8f20ed9a-8321-4e85-8413-5a93c2fb4e49" />

# Intuition

```
Understanding -  For all pairs (i,j) such that i < j calculate F(i,j) and find sum of all the F(i,j) 
1 <=N <= 100000 | 1<=B[i]<=100000
```

## Brute Force : TC - O(N*N*(2L)) = O(N*N*12) 
```
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Function to concatenate integers i and j and convert to an integer
int f(int i, int j) {
    string s1 = to_string(i);
    string s2 = to_string(j);
    string l = s1 + s2;
    int r = stoi(l);
    return r;
}

int main() {
    int n;
    cout << "Enter n: ";
    cin >> n;
    vector<int> b(n + 1);
    
    cout << "Enter " << n + 1 << " elements of array b: ";
    for (int i = 1; i <= n; ++i) {
        cin >> b[i];
    }

    int sum = 0;
    for (int i = 1; i <= n; ++i) {       //O(n^2)
        for (int j = i + 1; j <= n; ++j) {
            sum += f(b[i], b[j]);
        }
    }

    cout << "Sum: " << sum << endl;
    return 0;
}

```

## Optimal : TC - O(N*L) = O(N*6)
` when we are at index j we need to find all valid pair sum from 0 to j-1 ♦`

<img width="705" height="396" alt="image" src="https://github.com/user-attachments/assets/7c3f8bdd-4ca9-4ebd-aa24-b1c36b608f6f" />

``` 
multiply the no.of digit_count of a[j] to all nums before a[j]
that is 10 ^ digit_count(a[j]) is multiplied to all sum(i...j-1) and
a[j] is multiplied to (j-1) times
```

<img width="724" height="410" alt="image" src="https://github.com/user-attachments/assets/bd4839c7-1a8c-4697-9f92-bbe1ab442752" />

<img width="726" height="375" alt="image" src="https://github.com/user-attachments/assets/1681c214-70e9-4ec6-9fd9-8e4e8d4e4a2a" />

<img width="726" height="408" alt="image" src="https://github.com/user-attachments/assets/f00291db-1798-40a3-87de-2cb8a65b6bdd" />

<img width="710" height="377" alt="image" src="https://github.com/user-attachments/assets/8d97c07b-9c88-471c-8dc4-699d03c28cbc" />

<img width="1599" height="781" alt="image" src="https://github.com/user-attachments/assets/73c9ba36-cfd8-4057-b3f5-37e4c13a7f72" />


```
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

// Function to count the number of digits in an integer
// This matches the need to know how many digits 'Y' has
// in order to compute F(X, Y) = X * (10^len(Y)) + Y
int digit_count(int num) {
    return to_string(num).length();
}

int main() {
    int n = 3;  
    // n = size of array A (from problem: "single integer N")

    // Array b is made 1-based for convenience
    // Problem: "second line contains N space separated integers"
    // Example input: A = [1, 20, 30]
    // Index 0 is unused
    vector<int> b = {0, 1, 20, 30};

    long long sum = 0; // sum of all previous elements A[1..j-1]
    long long ans = 0; // final sum of all F(A[i], A[j]) for i < j
    
    // Loop over j from 1 to N
    // Each iteration: calculate contribution of all pairs (i, j) where i < j
    for (int j = 1; j <= n; ++j) {

        // y = number of digits in A[j]
        int y = digit_count(b[j]);

        // For all pairs (i, j), F(A[i], A[j]) = A[i] * 10^len(A[j]) + A[j]
        // sum holds Σ A[i] for i < j  → so sum * 10^len(A[j]) gives Σ A[i]*10^len(A[j])
        // (j - 1) * A[j] gives Σ A[j] repeated (j - 1) times (one for each i < j)
        long long vl = (j - 1) * b[j] + pow(10, y) * sum;

        // Add this total contribution for index j
        ans += vl;

        // Update sum for next iteration: include current A[j] in prefix sum
        sum += b[j];
    }

    // Output the final sum (in problem, mod 998244353 is required)
    cout << "Sum: " << ans << endl;
    return 0;
}
```

## RUN HERE
https://ideone.com/AKROv2
