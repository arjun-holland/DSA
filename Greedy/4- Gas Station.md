# PROBLEM
<img width="722" height="715" alt="image" src="https://github.com/user-attachments/assets/2e1a0c8c-e14c-40a3-936d-7fefa3ce4ec4" />
<img width="717" height="330" alt="image" src="https://github.com/user-attachments/assets/1dbf7b34-0de3-488e-b9b1-8d818932b43f" />

# BRUTE FORCE CODE : GENERAL SIMULATION
```
class Solution {
public:
    int startStation(vector<int>& gas, vector<int>& cost) {
        int n = gas.size();

        for (int start = 0; start < n; ++start) {
            if (gas[start] < cost[start]) continue; // Can't even leave station

            int tank = 0;
            int count = 0;
            int i = start;

            while (count < n) { 
                tank += gas[i];
                if (tank < cost[i]) {
                    break; // Not enough gas to go to next station
                }
                tank -= cost[i];
                i = (i + 1) % n;
                ++count;
            }

            if (count == n) return start; // Completed full circle
        }

        return -1; // No valid starting point
    }
};
```

# OPTIMAL : GREEDY
<img width="925" height="238" alt="image" src="https://github.com/user-attachments/assets/85ed3782-e9a0-4469-808d-9042cc3c00f0" />
```
              for (int i = 0; i < gas.size(); ++i) {
                  currGas += gas[i] - cost[i];
              
                  if (currGas < 0) {
                      start = i + 1;
                      currGas = 0;
                  }
              }
```

```
class Solution {
public:
    int startStation(vector<int>& gas, vector<int>& cost) {
        int totalGas = 0, totalCost = 0;
        int currGas = 0, start = 0;

        for (int i = 0; i < gas.size(); ++i) {
            totalGas += gas[i];
            totalCost += cost[i];
            currGas += gas[i] - cost[i];

            // If we can't reach station i+1, reset start
            if (currGas < 0) {
                start = i + 1;
                currGas = 0;
            }
        }

        return (totalGas >= totalCost) ? start : -1;
    }
};
```
