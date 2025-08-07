# Problem
<img width="1036" height="414" alt="image" src="https://github.com/user-attachments/assets/8a292666-fc1c-4304-a0d7-8084434333e0" />
<img width="1018" height="701" alt="image" src="https://github.com/user-attachments/assets/9a7bcede-a689-4c81-8738-19a4e1d66f82" />
<img width="876" height="170" alt="image" src="https://github.com/user-attachments/assets/1a0d8382-7331-4d6c-b087-c01a658c09db" />

# Intuition
<img width="1025" height="472" alt="image" src="https://github.com/user-attachments/assets/fa411327-7a3c-46bf-91ba-f823e77657f7" />
<img width="893" height="323" alt="image" src="https://github.com/user-attachments/assets/b90ea814-802f-4e8b-b649-cd428a9e8ee0" />


![WhatsApp Image 2025-08-06 at 19 15 36_21b96887](https://github.com/user-attachments/assets/527350e0-82f2-4539-8348-e7be22207bf4)


# Code
```
class Solution {
public:
    int numOfUnplacedFruits(std::vector<int>& fruits, std::vector<int>& baskets) {
        int n = baskets.size();
        int m = static_cast<int>(sqrt(n));  //squrt of n = no.of blocks does section contain
        int section = (n + m - 1) / m;     //total no.of sections
        int count = 0;
        vector<int> maxV(section, 0);

        // Initialize max values for each section
        for (int i = 0; i < n; i++) {
            maxV[i / m] = max(maxV[i / m], baskets[i]);
        }

        for (int fruit : fruits) {
            bool placed = false;
            for (int sec = 0; sec < section; ++sec) {
                // If max basket in section can't hold fruit, skip
                if (maxV[sec] < fruit) continue;

                // Search block for suitable basket
                maxV[sec] = 0;
                for (int i = 0; i < m; ++i) { //each section has m - blocks
                    int pos = sec * m + i;
                    if (pos >= n) break;

                    if (!placed && baskets[pos] >= fruit) {
                        baskets[pos] = 0;
                        placed = true;
                    }
                    maxV[sec] = max(maxV[sec], baskets[pos]);
                }
                if (placed) break;
            }
            if (!placed) ++count;
        }

        return count;
    }
};

```
