# Problme
<img width="667" height="529" alt="image" src="https://github.com/user-attachments/assets/970fe423-ca46-4b99-886a-0dee0b7f0c95" />


# Intuition
## Brute Forec
```
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n = 2; // Assuming n is 2 as per provided arrays
    int a[] = {2, 5};
    int b[] = {3, 8};
    int c[] = {-5, 8};
    int d[] = {5, 10};
    int e[] = {-10, 100};

    int count = 0;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            for (int k = 0; k < n; k++) {
                for (int l = 0; l < n; l++) {
                    for (int m = 0; m < n; m++) {
                        if (a[i] + b[j] + c[k] + d[l] + e[m] == 0) {
                        	// cout<<i<<j<<k<<l<<m<<endl;
                            count++;
                        }
                    }
                }
            }
        }
    }

    cout << count << std::endl;

    return 0;
}

```

## Optimal
```
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    int n = 2; // Assuming n is 2 as per provided arrays
    int a[] = {2, 5};
    int b[] = {3, 8};
    int c[] = {-5, 8};
    int d[] = {5, 10};
    int e[] = {-10, 100};

    unordered_map<int, int> hashmap;

    for (int l = 0; l < n; l++) {
        for (int m = 0; m < n; m++) {
            int sum = d[l] + e[m];
            hashmap[sum]++;
        }
    }

    int count = 0;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            for (int k = 0; k < n; k++) {
                int required_sum = 0-(a[i] + b[j] + c[k]);
                count += hashmap[required_sum];
            }
        }
    }

    cout << count << endl;

    return 0;
}

```
