# PROBLEM
<img width="916" height="931" alt="image" src="https://github.com/user-attachments/assets/8914d1b6-26ed-440a-a1e6-7f7ae76ad63a" />

# INTUITION
<img width="1039" height="681" alt="image" src="https://github.com/user-attachments/assets/0a82fd52-02cc-496e-938e-e99eacfb6ae2" />
<img width="1012" height="731" alt="image" src="https://github.com/user-attachments/assets/d67001fa-9780-470a-a2ae-0b65e992560a" />
<img width="946" height="204" alt="image" src="https://github.com/user-attachments/assets/b0a936a2-1435-4c88-b5ac-5934e34fa225" />


# CODE
```
class Solution {
  public:
    int median(vector<vector<int>> &mat) {
        int n = mat.size(), m = mat[0].size();
        
        // min = smallest of first elements, max = largest of last elements
        int low = INT_MAX, high = INT_MIN;
        for(int i = 0; i < n; i++) {
            low = min(low, mat[i][0]);
            high = max(high, mat[i][m-1]);
        }
        
        int desired = (n*m + 1) / 2; // median position
        
        while(low < high) {
            int mid = low + (high - low)/2;
            int cnt = 0;
            
            // count elements <= mid
            for(int i = 0; i < n; i++) {
                cnt += upper_bound(mat[i].begin(), mat[i].end(), mid) - mat[i].begin();
            }
            
            if(cnt < desired) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }
        
        return low; // or high, both converge
    }
};
```
