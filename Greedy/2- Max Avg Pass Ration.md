# PROBLEM
<img width="647" height="721" alt="image" src="https://github.com/user-attachments/assets/72e157ab-fcd4-4ea6-a6ee-5620becbcd81" />
<img width="650" height="671" alt="image" src="https://github.com/user-attachments/assets/a6b18b7e-da07-4683-899e-2561f1d0c56b" />

# INTUITION
`After reading that question we get thye idea of recurssion as we need to try out every possibility`  
## CODE OF RECURSSION
```
class Solution {
public:
    int tl;
    double ans = 0;
    
    double helper(vector<vector<int>>& c){
        double ca = 0;
        for(int i = 0; i < c.size(); i++){
            ca += (double)c[i][0] / c[i][1];
        }
        return ca / tl;
    }

    void solve(int i, vector<vector<int>>& c, int et, int e){
        if(i >= c.size() || et > e) return;

        if(et == e){
            double v = helper(c);
            ans = max(ans, v);
            return;
        }

        // Assign extra student to current class
        c[i][0] += 1;
        c[i][1] += 1;
        solve(i, c, et + 1, e);

        c[i][0] -= 1;
        c[i][1] -= 1;
        // Move to next class without assigning here
        solve(i + 1, c, et, e);
    }

    double maxAverageRatio(vector<vector<int>>& classes, int extraStudents) {
        tl = classes.size();
        solve(0, classes, 0, extraStudents);
        return ans;
    }
};
```

## CODE OF MEMOIZATION THE VOID RETURN TYPE
```
class Solution {
public:
    unordered_map<string, double> memo;
    int n;

    string encode(const vector<vector<int>>& classes) {
        string key;
        for (const auto& c : classes) {
            key += to_string(c[0]) + "/" + to_string(c[1]) + ",";
        }
        return key;
    }

    double helper(vector<vector<int>>& classes, int extraStudents) {
        if (extraStudents == 0) {
            double sum = 0.0;
            for (auto& c : classes) {
                sum += (double)c[0] / c[1];
            }
            return sum / classes.size();
        }

        string key = encode(classes) + "_" + to_string(extraStudents);
        if (memo.count(key)) return memo[key];

        double maxAvg = 0.0;

        for (int i = 0; i < classes.size(); ++i) {
            classes[i][0]++;
            classes[i][1]++;
            maxAvg = max(maxAvg, helper(classes, extraStudents - 1));
            classes[i][0]--;
            classes[i][1]--;
        }

        return memo[key] = maxAvg;
    }

    double maxAverageRatio(vector<vector<int>>& classes, int extraStudents) {
        n = classes.size();
        return helper(classes, extraStudents);
    }
};
```
# OPTYIMLA CODE INTUITION
<img width="844" height="392" alt="image" src="https://github.com/user-attachments/assets/672ed9d8-3ac5-4d26-8d3b-7700aec78bd5" />
<img width="952" height="416" alt="image" src="https://github.com/user-attachments/assets/b2396a81-a7fb-4474-b0d1-d3589f7915b9" />
<img width="961" height="676" alt="image" src="https://github.com/user-attachments/assets/ddce63b6-fad9-4e17-ac9a-63e1ad87898a" />
<img width="951" height="289" alt="image" src="https://github.com/user-attachments/assets/a0af9d2b-e99e-4e4b-afa7-fe26f8b63b08" />


# CODE
```
class Solution {
public:
    double maxAverageRatio(vector<vector<int>>& classes, int extraStudents) {

        // Lambda to compute the gain in pass ratio if one extra student is added to a class
        auto calculateGain = [](int pass, int total) {
            return (double)(pass + 1) / (total + 1) - (double)(pass) / total;
        };

        // Max heap to always pick the class with maximum gain if a student is added
        priority_queue<pair<double, pair<int, int>>> maxHeap;

        // Push all classes into heap based on initial gain
        for (auto& c : classes) {
            int pass = c[0], total = c[1];
            maxHeap.push({calculateGain(pass, total), {pass, total}});
        }

        // Assign each extra student to the class with the highest gain
        while (extraStudents--) {
            auto [gain, classInfo] = maxHeap.top();
            maxHeap.pop();

            int pass = classInfo.first;
            int total = classInfo.second;

            // Add one passing student to the chosen class
            pass++;
            total++;

            // Recalculate gain and push updated class back into heap
            maxHeap.push({calculateGain(pass, total), {pass, total}});
        }

        // Calculate the final average pass ratio
        double totalPassRatio = 0;
        while (!maxHeap.empty()) {
            auto [_, classInfo] = maxHeap.top();
            maxHeap.pop();
            totalPassRatio += (double)classInfo.first / classInfo.second;
        }

        return totalPassRatio / classes.size();
    }
};

```
