# Problem
![image](https://github.com/user-attachments/assets/31d79794-12ca-4e76-862d-ce787c7d38f8)

![image](https://github.com/user-attachments/assets/571d842f-0958-4119-911e-03a98d46705e)

![image](https://github.com/user-attachments/assets/6ef12d5d-8108-4d1a-a2e6-03c954e7886f)

![image](https://github.com/user-attachments/assets/dc0c5c1a-598a-4084-8909-e3db2cebb5dc)

# Intuition
![image](https://github.com/user-attachments/assets/3172338c-bee8-493a-885c-ed926ae52f36)
![image](https://github.com/user-attachments/assets/89280c6e-13e3-4835-a1c2-e1bc0cc8927a)
![image](https://github.com/user-attachments/assets/05fe6adb-d574-4b6b-84ee-2f4606c59574)
```
for k = 1, i.e 1 shit = we merge 2 spaces
```
![image](https://github.com/user-attachments/assets/92858e7a-3784-4391-84f0-dbdec871ea18)
```
for k = 2, i.e 2 shit = we merge 3 spaces
```
```
for k = n, i.e n shit = we merge [n+1] spaces
```

# code
```
class Solution {
public:
    int maxFreeTime(int eventTime, int k, vector<int>& startTime, vector<int>& endTime) {
        // Vector to store free time between events
        vector<int> freeTime;

        // First free slot is before the first event
        freeTime.push_back(startTime[0]);

        // Calculate free time between each consecutive event
        for(int i = 1; i < startTime.size(); i++) {
            freeTime.push_back(startTime[i] - endTime[i - 1]);   //startTime of curevent - endTime of prevevent
        }

        // Add free time after the last event until the end of the day
        freeTime.push_back(eventTime - endTime[startTime.size() - 1]);

        // Sliding window approach to find the max sum of at most (k+1) freeTime intervals
        int i = 0, j = 0;
        int maxAns = 0, curAns = 0;

        while(i < freeTime.size()) {
            curAns += freeTime[i]; // Add current free time to the window

            // If the window exceeds k+1 intervals, slide it by removing oldes as we can merge only K+1 free time slots
            if((i - j + 1) > k + 1) {
                curAns -= freeTime[j];
                j++;
            }

            // Update the maximum free time sum found
            maxAns = max(maxAns, curAns);
            i++;
        }

        return maxAns; // Return the maximum accumulated free time with up to k events skipped
    }
};

```
