# PROBLEM
<img width="1063" height="909" alt="image" src="https://github.com/user-attachments/assets/e328a522-211c-4668-9f0c-e201421348df" />
<img width="1017" height="943" alt="image" src="https://github.com/user-attachments/assets/d0f1a4d5-428a-4e1d-926c-22a42bc53c45" />
<img width="780" height="818" alt="image" src="https://github.com/user-attachments/assets/bcb086c9-282d-45b9-9eba-8a28642fce82" />
<img width="820" height="658" alt="image" src="https://github.com/user-attachments/assets/e5337c38-890c-459d-81a9-ed5f889fa79f" />


# INTUITION
<img width="867" height="269" alt="image" src="https://github.com/user-attachments/assets/bb8f5a2d-72fb-4704-9a33-e51a5fe36104" />
<img width="1060" height="548" alt="image" src="https://github.com/user-attachments/assets/daca9328-fd4a-4f72-b80c-8dd270da6805" />
<img width="924" height="308" alt="image" src="https://github.com/user-attachments/assets/051d3f0d-5273-412c-b241-f4e1a7a37f57" />

<img width="1142" height="559" alt="image" src="https://github.com/user-attachments/assets/83ae7a17-2108-45ea-952e-b099b17a1778" />
<img width="1135" height="524" alt="image" src="https://github.com/user-attachments/assets/8c42b761-9627-4734-ab19-4476d881aa53" />

<img width="797" height="901" alt="image" src="https://github.com/user-attachments/assets/5d05d199-4547-4b72-8a67-ba8417bb1d97" />
<img width="784" height="310" alt="image" src="https://github.com/user-attachments/assets/8d6eadba-ae6f-4aea-aab0-409ca4ed1642" />


# CODE
```
#include <bits/stdc++.h>
using namespace std;

long getMinimumCost(vector<int> product, int k) {
    int n = product.size();

    // Step 1: Count total number of 1s
    int total_c_1 = accumulate(product.begin(), product.end(), 0);

    // Step 2: Find minimum sum subarray of length k
    int window_sum = 0;
    for (int i = 0; i < k; i++) {
        window_sum += product[i];
    }
    int min_sum = window_sum;

    for (int i = k; i < n; i++) {
        window_sum += product[i] - product[i - k];
        min_sum = min(min_sum, window_sum);
    }

    int y = min_sum;

    // Step 3: Apply formula
    long ans = (1LL * y * (y + 1)) / 2 + (total_c_1 - y);
    return ans;
}

int main() {
    vector<int> product = {1, 1, 1, 0, 1};
    int k = 4;
    cout << getMinimumCost(product, k) << endl; // Expected Output: 7
    return 0;
}
```
