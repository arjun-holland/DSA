# Probelm
<img width="500" height="643" alt="image" src="https://github.com/user-attachments/assets/d413e856-3aa8-47c3-8991-c1ddf4f27b48" />


# Brute Force
```
#include <iostream>
#include <cmath>

int main() {
    int n=5;
    int a[] = {1, 4, -1, 2, 2};
    int target=4;
    int c = 0;

    for(int i = 0; i <n; i++){
        for(int j = i+1; j < n; j++){
            if(abs(a[i] - a[j]) + abs(a[i] + a[j]) == target){
                c++;
            }
        }
    }
    cout << c << std::endl;
    return 0;
}
TC - O(N*N)
O(1) space. 
```

# Intutition For Optimal
<img width="557" height="187" alt="image" src="https://github.com/user-attachments/assets/f10bebf2-a7dc-41c5-8d44-283e17dd504b" />

<img width="1600" height="747" alt="image" src="https://github.com/user-attachments/assets/14b7aff8-a779-41ad-8fb8-1b972c63c5f7" />

## Counting pairs (Combinatorics)

<img width="1462" height="704" alt="image" src="https://github.com/user-attachments/assets/e3904800-e678-489c-9052-cdda7ba0a576" />


# Run Code 
https://ideone.com/VJ3iTt
