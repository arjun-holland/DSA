# Problem
<img width="679" height="603" alt="image" src="https://github.com/user-attachments/assets/24679c6e-8f93-4f6c-9d35-305592d88213" />
<img width="689" height="347" alt="image" src="https://github.com/user-attachments/assets/bc569a93-3106-446d-93a6-3d680c56fd72" />

# Intuition
<img width="1066" height="158" alt="image" src="https://github.com/user-attachments/assets/175ed7b6-e417-4ef2-968c-de09d36ded46" />


<img width="874" height="466" alt="image" src="https://github.com/user-attachments/assets/12f8a226-8bfa-4d2f-a0bc-fbaa1f55f7b8" />
<img width="1006" height="346" alt="image" src="https://github.com/user-attachments/assets/79ed97b8-6569-4814-8ea5-d72a74e44615" />
<img width="840" height="231" alt="image" src="https://github.com/user-attachments/assets/9b437dbb-f212-4d3a-86f5-e1bd47ee4243" />

<img width="681" height="180" alt="image" src="https://github.com/user-attachments/assets/33957cb1-bbec-4314-a16f-902e54dcc231" />

![WhatsApp Image 2025-08-19 at 21 08 49_1577b6a6](https://github.com/user-attachments/assets/0f8837c8-142c-459a-bfe3-2e7d0a1501a4)


# Code
```
class Solution {
public:
    vector<int> farMin(vector<int>& arr) {
        int n = arr.size();
        vector<int> ans(n, -1);

        // Step 1: build suffix minimum array
        vector<int> sufMin(n), sufIdx(n);
        sufMin[n-1] = arr[n-1];
        sufIdx[n-1] = n-1;
        for (int i = n-2; i >= 0; i--) {
            if (arr[i] < sufMin[i+1]) {
                sufMin[i] = arr[i];
                sufIdx[i] = i;
            } else {
                sufMin[i] = sufMin[i+1];
                sufIdx[i] = sufIdx[i+1];
            }
        }

        // Step 2: for each i, binary search in suffix min
        for (int i = 0; i < n-1; i++) {
            int l = i+1, r = n-1, best = -1;
            while (l <= r) {
                int mid = (l+r)/2;
                if (sufMin[mid] < arr[i]) {
                    best = sufIdx[mid];
                    l = mid+1; // try to go farther
                } else {
                    r = mid-1;
                }
            }
            ans[i] = best;
        }

        return ans;
    }
};

```
