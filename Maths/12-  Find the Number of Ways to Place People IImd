# PROBLEM
<img width="985" height="321" alt="image" src="https://github.com/user-attachments/assets/f6058a5c-3e4f-4a5f-8f01-7ed668201150" />
<img width="787" height="611" alt="image" src="https://github.com/user-attachments/assets/89746cee-799b-47fb-ab7a-ff637720bd00" />
<img width="975" height="611" alt="image" src="https://github.com/user-attachments/assets/808d3f05-1a2e-48a7-bf1a-46760aa0eff7" />
<img width="987" height="582" alt="image" src="https://github.com/user-attachments/assets/d578f261-6e48-46f0-afaa-426a67f24efc" />
<img width="618" height="189" alt="image" src="https://github.com/user-attachments/assets/5d907af0-6304-427e-8fa3-3c652b0d04a2" />

# INTUITION
<img width="1000" height="251" alt="image" src="https://github.com/user-attachments/assets/9b1a0dc6-b901-4ef9-9f2f-df64cd8e72e3" />

<img width="1259" height="696" alt="image" src="https://github.com/user-attachments/assets/cb4b308f-5222-445e-be6d-2d2ba5317ff9" />
<img width="1169" height="711" alt="image" src="https://github.com/user-attachments/assets/7c133a82-04f4-46b8-b407-3fca4f5641f5" />

<img width="1294" height="780" alt="image" src="https://github.com/user-attachments/assets/cc172d2e-9a98-4c91-adb7-eaa2940817de" />

<img width="1248" height="635" alt="image" src="https://github.com/user-attachments/assets/d88f71f4-dcb6-4889-a7be-f7d713432f29" />
<img width="902" height="480" alt="image" src="https://github.com/user-attachments/assets/54a3e537-81a4-4d47-8ebc-8ebf5bbaec44" />
<img width="1286" height="835" alt="image" src="https://github.com/user-attachments/assets/bfd9b35d-7db8-43ca-96e9-fbdd2c12510c" />


# Optimla CODE : as Previous Brute NOt accepted
```
class Solution {
public:
    int numberOfPairs(vector<vector<int>>& points) {
        int n = points.size();

        // ✅ Sort points:
        // Primary: increasing x (left to right)
        // Secondary: decreasing y (top to bottom)
        // This way, if two points share the same x, we pick the one with higher y first.
        sort(points.begin(), points.end(), [](const vector<int>& p1, const vector<int>& p2){
            return p1[0] == p2[0] ? p1[1] > p2[1] : p1[0] < p2[0];
        });

        int count = 0;

        // Outer loop: pick point A (potential top-left corner)
        for(int A = 0; A < n - 1; ++A){
            int bottom_right_y = INT_MIN;     // To track the highest y seen so far in valid B candidates

            // Inner loop: pick point B (potential bottom-right corner)
            for(int B = A + 1; B < n; ++B){

                // ✅ Check if B is "below" A (same x or to the right, and lower y)
                if(points[B][1] <= points[A][1] && points[B][1] > bottom_right_y){
                    // ➕ Valid pair (A, B):
                    //   - xB >= xA because of sorting
                    //   - yB <= yA from condition
                    //   - yB > bottom_right_y ensures:
                    //        - No point between A and B (in x and y) was already counted
                    //        - Avoids overcounting or overlapping rectangles

                    count++;

                    // ⬇️ Update the y-boundary to avoid counting overlapping rectangles
                    bottom_right_y = points[B][1];
                }
            }
        }

        return count;
    }
};
```

# TIME COMPLEXITY
```
as => 2 <= n <= 10^3
we are using 3 for loops => n^3 which makes
    (10^3)^3  => 10^9
          => (10^9) > (10^8) => O(n^3) not accepted
we have to use O(n^2), O(n) or O(n logn)
```
