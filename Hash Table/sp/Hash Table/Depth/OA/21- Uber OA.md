# Problem
<img width="731" height="675" alt="image" src="https://github.com/user-attachments/assets/54e01cb9-11ec-4de2-bf6e-2989f9ee34c0" />
<img width="684" height="753" alt="image" src="https://github.com/user-attachments/assets/e300e20f-62bc-4057-876e-9b1a95cee2bb" />
```
            1 <= N <= 10000
            1 <= element of array <= 10000
```

# Intuition
## Brute Force : TC :- O(N^2*2*|S|) = O(N^2*2*6) = O(N^2*12) = O(N^2) : SC-> O(2*|S|) = O(12) = O(1)  

```
        -> n. 
        -> b[n+1]
        tot = 0 
        for(i=1;i<=n;i++){
            for(j=1;j<=n;j++){
                v1 = to_string(b[i])
                v5 = to_string(b[j])
                g = v1 + v5 
                r = int(g) 
                tot = tot + r 
            }
        }
```

## Optimal
<img width="714" height="399" alt="image" src="https://github.com/user-attachments/assets/651d2ab2-4faf-48cc-bab8-2427ef1c4e5e" />
<img width="723" height="401" alt="image" src="https://github.com/user-attachments/assets/67b75a17-fe60-4980-a6d4-7c48d3fae115" />

```
For evry index 'i' num we need all no.of digits(1 to 6 digits according to constraints) types from '1' to 'n'

let digit[u] = count of numbers in the array which has 'u' number of digits.
```

<img width="718" height="401" alt="image" src="https://github.com/user-attachments/assets/44ba74b2-f4aa-4afe-92e4-cfc63af89969" />
<img width="730" height="402" alt="image" src="https://github.com/user-attachments/assets/1ae97f2d-f354-4473-9b31-be5cd05d1a5a" />
<img width="704" height="395" alt="image" src="https://github.com/user-attachments/assets/dc72d3d5-2a89-458d-b947-f0eae95a8037" />
<img width="956" height="534" alt="image" src="https://github.com/user-attachments/assets/2180b5f0-9b48-4499-a482-5e9e5a4e0772" />
<img width="852" height="528" alt="image" src="https://github.com/user-attachments/assets/cf116ac9-f4b5-4052-acda-7e65e4301d95" />

## Code
```
#include <bits/stdc++.h>
using namespace std;

int no_of_digit(int num) {
    int count = 0;
    while (num > 0) {
        num /= 10;
        count++;
    }
    return count;
}

int main() {
    int n;
    cin >> n;

    int b[n + 1];
    int right = 0;     // Calculate right in advance

    for (int i = 1; i <= n; i++) {
        cin >> b[i];
        right += b[i];
    }

    int tot = 0;
    int digit[10] = {0};

    for (int i = 1; i <= n; i++) {
        int u = no_of_digit(b[i]);
        digit[u] = digit[u] + 1;   //digit[u] = count of numbers in the array which has 'u' number of digits.
    }

    int g = 0;
    for (int i = 1; i <= n; i++) {
        int l = 1, y = 0;
        while (l <= 6) {
            y += b[i] * pow(10, l) * digit[l];
            l++;
        }

        int lt = y;
        int v = lt + right;
        g = g + v;
    }

    cout << g << endl;

    return 0;
}
```

## Final Optimized : Precompute 10 powers
```
#include <bits/stdc++.h>
using namespace std;

int no_of_digit(long long num) {
    int count = 0;
    while (num > 0) {
        num /= 10;
        count++;
    }
    return count;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    long long n;
    cin >> n;

    vector<long long> b(n + 1);
    long long right = 0;

    for (long long i = 1; i <= n; i++) {
        cin >> b[i];
        right += b[i];
    }

    // Precompute powers of 10 up to 10^6
    long long p10[7];
    p10[0] = 1;
    for (int i = 1; i <= 6; i++) {
        p10[i] = p10[i - 1] * 10;
    }

    long long digit[10] = {0};
    for (long long i = 1; i <= n; i++) {
        int u = no_of_digit(b[i]);
        digit[u]++;
    }

    long long g = 0;
    for (long long i = 1; i <= n; i++) {
        long long y = 0;
        for (int l = 1; l <= 6; l++) {
            y += b[i] * p10[l] * digit[l];
        }
        long long v = y + right;
        g += v;
    }

    cout << g << "\n";
    return 0;
}
```

