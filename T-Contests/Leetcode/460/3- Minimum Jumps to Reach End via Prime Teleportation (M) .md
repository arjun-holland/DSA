//Submission : https://leetcode.com/problems/minimum-jumps-to-reach-end-via-prime-teleportation/submissions/1716463290/

# Problem
<img width="1206" height="469" alt="image" src="https://github.com/user-attachments/assets/9578e9df-a582-4ff0-8274-0d53b5730818" />
<img width="1168" height="454" alt="image" src="https://github.com/user-attachments/assets/a1b7fb1b-2dae-4577-aef3-e31cb46ab611" />
<img width="1126" height="453" alt="image" src="https://github.com/user-attachments/assets/d9fa940f-f808-48f2-a2e2-52282a0dc5e9" />
<img width="1017" height="263" alt="image" src="https://github.com/user-attachments/assets/f2178373-1594-493b-82e2-0977b602155a" />
<img width="751" height="159" alt="image" src="https://github.com/user-attachments/assets/e2287dcb-b2b6-4809-a80a-1341365a4228" />

# Intution
<img width="1072" height="258" alt="image" src="https://github.com/user-attachments/assets/221b403a-d39b-4d11-ba19-d0cc7bcca147" />
<img width="1105" height="583" alt="image" src="https://github.com/user-attachments/assets/7682229d-e8be-464a-a8e8-f2e0e5de323a" />



# Code
```
vector<bool> isPrime (1e6 + 1, true);

class Solution {
public:
    void fill () {      //seive()
        isPrime [0] = isPrime [1] = false;
        for (int i = 2; i * i <= 1e6; ++i) {
            if (isPrime [i]) {
                for (int j = i * i; j <= 1e6; j += i)
                    isPrime [j] = false;
            }
        }
    }

    int minJumps(vector<int>& nums) {
        if (isPrime[0]) fill();

        int n = nums.size();
        unordered_map <int,vector <int>> mp;
        for (int i = 0; i < n; i++) mp[nums[i]].push_back(i);  //mp : value -> index
        
        vector<int> dist (n, -1);
        queue<int> qu;   //hold the inidices

        qu.push(0); dist[0] = 0;
        unordered_set<int> used;

        while (!qu.empty()) {  
            int node = qu.front();qu.pop();

            if (node - 1 >= 0 && dist[node-1] == -1) {
                qu.push(node-1);
                dist[node-1] = dist[node] + 1;
            }
            if (node + 1 < n && dist[node+1] == -1) {
                qu.push(node+1);
                dist[node+1] = dist[node] + 1;
            }

            if (isPrime[nums[node]] == false || used.contains(nums[node])) continue;

            //when the node is prime 
            for (int i = 1; i*nums[node] <= 1e6 ; i++) {
                if (mp.contains(i*nums[node]) == false) continue;
                for (auto it : mp[i*nums[node]]) {
                    if (dist[it] != -1) continue;
                    qu.push(it);
                    dist[it] = dist[node] + 1;
                }
            }
            used.insert(nums[node]);
        }
        return dist.back();
    }
};
```

<img width="1163" height="374" alt="image" src="https://github.com/user-attachments/assets/c242cbf4-7294-47fa-bddc-47280f9d1a6c" />
<img width="1170" height="476" alt="image" src="https://github.com/user-attachments/assets/c068746a-0f27-4099-8519-800b22da3730" />

