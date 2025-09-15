# PROBLEM
<img width="727" height="598" alt="image" src="https://github.com/user-attachments/assets/41261426-ba77-4572-8019-cf2ea6830a97" />
<img width="715" height="244" alt="image" src="https://github.com/user-attachments/assets/57671132-086a-4fca-8bd4-0bac5ad340d3" />
<img width="557" height="204" alt="image" src="https://github.com/user-attachments/assets/6d4aec02-cc6e-4f16-8289-a8a98dc7fa82" />

# CODE
```
#include <iostream>
using namespace std;

// Function to calculate the factorial using recursion
int factorial(int n) {
    if (n == 0) {
        return 1; // Base case: 0! and 1! are both 1
    } 
    else {
        return n * factorial(n - 1); // Recursive case
    }
}

int main() {
    int n;
    cin >> n;
    if (n < 0) {
        cout << "Factorial is not defined for negative numbers." << std::endl;
    } else {
        int result = factorial(n);
        cout << "Factorial of " << n << " is " << result << std::endl;
    }
    return 0;
}
```
