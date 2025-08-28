# PROBLEM
<img width="836" height="182" alt="image" src="https://github.com/user-attachments/assets/48e8d37d-0e62-4071-9569-34b2317afc07" />
<img width="876" height="739" alt="image" src="https://github.com/user-attachments/assets/8c35a327-cf5b-4217-82d3-e48e77cabec6" />
<img width="886" height="489" alt="image" src="https://github.com/user-attachments/assets/8e124d00-0032-4cb7-aef7-85f2b0fe7b1d" />
<img width="817" height="225" alt="image" src="https://github.com/user-attachments/assets/da800509-2ac5-4148-a457-a3948c9e0625" />


# INTUITION
![WhatsApp Image 2025-08-28 at 16 27 24_67961c37](https://github.com/user-attachments/assets/89d1e398-41f0-4351-9dc3-fe09a87e78ed)


# CODE 1
```
class Solution {
public:
    vector<vector<int>> sortMatrix(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        int td = m + n -1;     //total diagonals
        int ed = td/2;         //total even diagonals
        int od = td - ed;      //total odd diagonals

        int i=n-2,j=0;
        for(int d=2;d <= od;d++){    //for all odd diagonals
            vector<int> h;
            int i_ = i,j_ = j;
            int id = i,jd = j;
            while(id < n && jd < m){       //collect all elements in that diagonal
                h.push_back(grid[id][jd]);
                id++;
                jd++;
            }
            sort(h.rbegin(),h.rend());  //sort in descending order
            int k = 0;
            while(i_ < n && j_ < m){   //put back them in grid
                grid[i_][j_] = h[k];
                i_++;
                j_++;
                k++;
            }
            i--;
        }

        i = 0,j = 1;
        for(int d = 1;d<=ed;d++){
            vector<int> h;
            int i_ = i,j_ = j;
            int id = i,jd = j;
            while(id < n && jd < m){
                h.push_back(grid[id][jd]);
                id++;
                jd++;
            }
            sort(h.begin(),h.end());
            int k = 0;
            while(i_ < n && j_ < m){
                grid[i_][j_] = h[k];
                i_++;
                j_++;
                k++;
            }
            j++;
        }

        return grid;
    }
};
```

# INTUITION
![WhatsApp Image 2025-08-28 at 16 17 04_158c56c5](https://github.com/user-attachments/assets/f844b27b-e918-445e-89f3-597167a35b15)

# CODE 2
```
class Solution {
public:
    vector<vector<int>> sortMatrix(vector<vector<int>>& grid) {
        int n=grid.size(),m=grid[0].size();
        unordered_map<int, vector<int>> diag;

        for (int i = 0; i < n; i++) {         //collect all the elements in their respective diagonals
            for (int j = 0; j < n; j++) {
                diag[i - j].push_back(grid[i][j]);
            }
        }
        for (auto &it : diag) {                //sort the elements in diagonals according to given condition
            if (it.first >= 0) {
                sort(it.second.begin(), it.second.end(), greater<int>());
            } 
            else {
                sort(it.second.begin(), it.second.end());
            }
        }
        unordered_map<int,int>mp; 
        for (int i = 0; i < n; i++) {            //put back the elements in diagonal in the grid based on the diagonal
            for (int j = 0; j < n; j++) {
                int a = i-j;     //tells which diagonal 
                grid[i][j] = diag[a][mp[a]++];  //at first mp[a]++ has 0 then it increments to 1 ...so on for the a th diagonal
            }
        }
        return grid;
    }
};
```
