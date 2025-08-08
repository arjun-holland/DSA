# Problem
<img width="682" height="430" alt="image" src="https://github.com/user-attachments/assets/29d4d73c-6ddc-40be-a4dd-677bfc134f97" />
<img width="662" height="634" alt="image" src="https://github.com/user-attachments/assets/86b8be3c-77d6-44da-8028-bc501962d6ff" />
<img width="618" height="555" alt="image" src="https://github.com/user-attachments/assets/2b9f1690-28e9-48af-8af2-feaa2775ff78" />
<img width="657" height="125" alt="image" src="https://github.com/user-attachments/assets/e064dd9b-bffd-413f-b5ee-47c1baf8240a" />


# Intuition
## Brute Force : Simple Simulation : Makes Space comp :O(n^2)
```
#include <iostream>
#include <vector>
#include <string>

int matching(const std::string &a, const std::string &b) {
    int matchCount = 0;
    for (size_t i = 0; i < std::min(a.size(), b.size()); ++i) {
        if (a[i] == b[i]) {
            matchCount++;
        } else {
            break;
        }
    }
    return matchCount;
}

int main() {
    int n = 3;
    std::vector<std::string> g = {"abc", "ade", "abc"};
    std::vector<int> final_answer(n, 0);

    for (int i = n - 1; i >= 0; --i) {
        int answer = 0;
        if (i != n - 1) {
            for (int j = i + 1; j < n; ++j) {
                int count = matching(g[i], g[j]);
                answer += count;
            }
        }
        final_answer[i] = answer;
    }

    for (int i = 0; i < n; ++i) {
        std::cout << final_answer[i] << " ";
    }

    return 0;
}

```
<img width="647" height="183" alt="image" src="https://github.com/user-attachments/assets/f3b94f58-1bbd-49c6-b3b7-940b5377a14e" />

## Optimla Intuition : Makes Space comp : O(1)

```
As we need only the char count which is at i'th index os string s1
such that the count is only start from the strings s1+1 to sn string
Observe the below diagram for more clarity.....
```
<img width="719" height="414" alt="Screenshot 2025-08-08 182958" src="https://github.com/user-attachments/assets/1ff4bce5-cca3-4adb-8ed9-6e69870b4de9" />

<img width="722" height="409" alt="Screenshot 2025-08-08 183330" src="https://github.com/user-attachments/assets/36b55838-9e8c-457b-ac7c-4bdc2fade197" />

```
as we need to know the char at every index probably 0 to 100001 indices and we have total 16 characters in english alphabets
it is better to creta a 2D vector, so that tracking is very easy
      arr[y][i] => y is the character and i is the index os that y'th character

we can write it as

      arr[i][y] => it means i'th character is y 
```

<img width="731" height="409" alt="Screenshot 2025-08-08 184915" src="https://github.com/user-attachments/assets/5acce2e1-3bbc-44c3-8876-6d0fdc239fd8" />

<img width="720" height="399" alt="Screenshot 2025-08-08 185126" src="https://github.com/user-attachments/assets/d430c6bf-94ba-48f4-9889-bb92865e344a" />


<img width="622" height="135" alt="image" src="https://github.com/user-attachments/assets/4507e3d6-363e-421b-bbbe-ba468ac34385" />

```
class Solution {
public:
    vector<int> matchingCnt(int n, vector<string>& X) {
        vector<vector<int>> g(100001, vector<int>(26, 0));
        vector<int> p(n, 0);
 
        for (int i = n - 1; i >= 0; i--) {
            string u = X[i];
            int c = 0;
            int d = u.size();
            for (int j = 0; j < d; j++) { // j --> column number
                int y = u[j] - 'a'; // get index of char
                c = c + g[j][y]; // g[j][y] : tells you the frequency of y in col "j"
                g[j][y] = g[j][y] + 1;
            }
            p[i] = c;
        }
 
        return p;
    }
};
 
int main() {
    Solution sol;
    int n = 3;
    vector<string> X = {"abc", "ade", "abc"};
    vector<int> result = sol.matchingCnt(n, X);
 
    for (int i = 0; i < n; ++i) {
       cout << result[i] << " ";
    }
 
    return 0;
}
```

# Run Optimal Code
https://ideone.com/xDX3RF
