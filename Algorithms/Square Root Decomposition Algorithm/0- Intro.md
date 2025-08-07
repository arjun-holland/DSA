<img width="1060" height="333" alt="image" src="https://github.com/user-attachments/assets/aa6bb7f4-291a-4514-b50b-6635a8f640a2" />
<img width="914" height="410" alt="image" src="https://github.com/user-attachments/assets/976cf9c8-86f5-4119-bac2-2b860da896fc" />
<img width="984" height="223" alt="image" src="https://github.com/user-attachments/assets/49777969-79b0-4e2b-9d14-e5b4d7bcb02b" />

<img width="885" height="493" alt="image" src="https://github.com/user-attachments/assets/c3b55491-466b-45a9-b30b-64f21a5cd7df" />
<img width="939" height="242" alt="image" src="https://github.com/user-attachments/assets/7924da46-8e6c-48d9-bdfc-5af10c7687a3" />
<img width="1049" height="684" alt="image" src="https://github.com/user-attachments/assets/2fea620e-5270-4b15-897b-7fc82c04e46b" />
<img width="1065" height="608" alt="image" src="https://github.com/user-attachments/assets/cd6a606e-f626-4e9c-be3a-7d07e023fb52" />

<img width="907" height="236" alt="image" src="https://github.com/user-attachments/assets/dd415c9f-bc8e-419b-8756-83c771dac9ce" />
<img width="1054" height="454" alt="image" src="https://github.com/user-attachments/assets/f11ee6db-5d9b-4f29-b3c1-08df616b4b36" />

---
# Range SUm Query Dry Run 

<img width="1053" height="623" alt="image" src="https://github.com/user-attachments/assets/27450ffe-a794-4257-ad09-bdd38bba05ac" />

```
      arr =        [ 1 |  3 ]   [ 5 |  7 ]   [ 9 | 11 ]  ans we need sum [1,4] inclusive
      index =         0   1        2    3       4    5
                          └──┐        └────────┐ └───┐      
                              │                │     │
                         Partial left         Full  Partial right
                           element             Block     element
                              (3)              (5+7)      (9)

```

<img width="1080" height="682" alt="image" src="https://github.com/user-attachments/assets/3ea59d0e-bccf-43e1-b58b-a46671f956ed" />


<img width="1068" height="728" alt="image" src="https://github.com/user-attachments/assets/e050c838-7b1c-4f3e-a7c2-c44e0d3fb081" />
<img width="1045" height="513" alt="image" src="https://github.com/user-attachments/assets/5eed770e-37b9-4a01-bcc2-f9ef207116b1" />

# Code
```
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

class SqrtDecomposition {
    vector<int> arr;      // Original array
    vector<int> blocks;   // Block sums
    int blockSize;

public:
    SqrtDecomposition(const vector<int>& input) {
        arr = input;
        int n = arr.size();
        blockSize = sqrt(n) + 1;
        blocks.resize(blockSize, 0);

        // Precompute block sums
        for (int i = 0; i < n; i++) {
            blocks[i / blockSize] += arr[i];
        }
    }

    // 🔍 Range Sum Query: O(√n)
    int rangeSum(int L, int R) {
        int sum = 0;

        while (L <= R && L % blk_sz != 0) { // Partial left
            sum += arr[L++];
        }

        while (L + blk_sz - 1 <= R) { // Full blocks
            sum += block[L / blk_sz];
            L += blk_sz;
        }

        while (L <= R) { // Partial right
            sum += arr[L++];
        }

        return sum;
    }

   // int query(int l, int r) {
   //     int sum = 0;
   //     int startBlock = l / blockSize;
   //     int endBlock = r / blockSize;
   //     if (startBlock == endBlock) {
   //        for (int i = l; i <= r; i++)
   //             sum += arr[i];
   //     } else {
   //         // Left partial block
   //         for (int i = l; i < (startBlock + 1) * blockSize; i++)
   //             sum += arr[i];
   //         // Full blocks in between
   //         for (int b = startBlock + 1; b < endBlock; b++)
   //             sum += blocks[b];
   //         // Right partial block
   //         for (int i = endBlock * blockSize; i <= r; i++)
   //             sum += arr[i];
   //     }
   //    return sum;
   // }

    // ✏️ Point Update: O(1)
    void update(int index, int value) {
        int blockIndex = index / blockSize;
        blocks[blockIndex] += value - arr[index];
        arr[index] = value;
    }
};

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11};
    SqrtDecomposition sqrtDS(arr);

    cout << "Sum of [1, 4] = " << sqrtDS.query(1, 4) << endl;  // Output: 3+5+7+9 = 24

    sqrtDS.update(2, 10);  // arr[2] = 10
    cout << "After update: Sum of [1, 4] = " << sqrtDS.query(1, 4) << endl;  // Output: 3+10+7+9 = 29

    return 0;
}

```
