# PROBLEM
<img width="985" height="321" alt="image" src="https://github.com/user-attachments/assets/f6058a5c-3e4f-4a5f-8f01-7ed668201150" />
<img width="787" height="611" alt="image" src="https://github.com/user-attachments/assets/89746cee-799b-47fb-ab7a-ff637720bd00" />
<img width="975" height="611" alt="image" src="https://github.com/user-attachments/assets/808d3f05-1a2e-48a7-bf1a-46760aa0eff7" />
<img width="987" height="582" alt="image" src="https://github.com/user-attachments/assets/d578f261-6e48-46f0-afaa-426a67f24efc" />
<img width="618" height="189" alt="image" src="https://github.com/user-attachments/assets/5d907af0-6304-427e-8fa3-3c652b0d04a2" />

# INTUITION
<img width="1043" height="202" alt="image" src="https://github.com/user-attachments/assets/585ed44c-77ff-4662-bc78-2f17f264ef54" />

<img width="1259" height="696" alt="image" src="https://github.com/user-attachments/assets/cb4b308f-5222-445e-be6d-2d2ba5317ff9" />
<img width="1169" height="711" alt="image" src="https://github.com/user-attachments/assets/7c133a82-04f4-46b8-b407-3fca4f5641f5" />


# CODE
```
class Solution {
public:
    int numberOfPairs(vector<vector<int>>& points) {
        int ans = 0;

        // ✅ Sort the points
        // Primary: increasing x
        // Secondary: decreasing y (to handle same x with higher y first)
        sort(points.begin(), points.end(), [](const auto &a, const auto &b){
            return a[0] == b[0] ? a[1] > b[1] : a[0] < b[0];
        });

        // Loop over all pairs (i, j)
        for(int i = 0; i < points.size(); i++) {
            int x1 = points[i][0];
            int y1 = points[i][1];

            for(int j = i + 1; j < points.size(); j++) {
                int x2 = points[j][0];
                int y2 = points[j][1];

                // ✅ A must be top-left of B: x1 ≤ x2 and y1 ≥ y2
                if(x2 >= x1 && y1 >= y2) {
                    bool valid = true;

                    // Check if any third point lies inside the rectangle formed by (i, j)
                    for(int k = 0; k < points.size(); k++) {
                        if(points[k] == points[i] || points[k] == points[j]) continue;

                        int x3 = points[k][0];
                        int y3 = points[k][1];

                        // ✅ Check if point[k] lies within or on the border of the rectangle
                        if(x1 <= x3 && x3 <= x2 && y1 >= y3 && y3 >= y2) {
                            valid = false;
                            break; // Found an interfering point
                        }
                    }
                    if(valid) ans++; // Valid (A, B) pair
                }
            }
        }

        return ans;
    }
};

```

# TIME COMPLEXITY
```
as => 2 <= n <= 50
we are using 3 for loops => n^3 which makes
    50^3  => 5^3 X 10^3
          => (125 X 10^3) < (10^8)
=> O(n^3)
```
