# PROBLEM
<img width="794" height="302" alt="image" src="https://github.com/user-attachments/assets/eb6b8e7a-a554-43e8-ab28-359a1527b568" />
<img width="724" height="454" alt="image" src="https://github.com/user-attachments/assets/063726f8-030f-40f5-883f-1cd1927165ec" />
<img width="804" height="663" alt="image" src="https://github.com/user-attachments/assets/e4c8e352-663b-4ce9-beb9-6e79ca750fa9" />
<img width="681" height="455" alt="image" src="https://github.com/user-attachments/assets/b5710aa3-3f84-43f5-99bc-e9bb769f2a1e" />
<img width="812" height="518" alt="image" src="https://github.com/user-attachments/assets/45cb6b08-cf6e-4fd2-9b51-c4b11698e5ab" />
<img width="600" height="134" alt="image" src="https://github.com/user-attachments/assets/63717f7a-e9b6-4de9-a468-351baaf7f11e" />

# INTUITION
```
After Observing the question we understand that the question says that it gives the min cost as possible
-> The entire (n*m)size sheet will be consider as one sheet which means : 
-> Initially the Horizontal segemnt (HS) = 1
-> Initially the Vertical segemnt (VS) = 1

-> When we cut the sheet, vertically then we have the (VS) = 2 and (HS) = 1 
-> When we cut the sheet, horizontally then we have the (VS) = 1 and (HS) = 2

-> As we have the cost to cut and
      we observce that (HS) or (VS) are increasing with respect top the cuts [ like for vertical cuts (VS) increasing and for horizontal cuts (HS) increasing ]
      so the (VS), (HS) are small at that strating time so multiply them with high cost as .....

                  high cost * low Value = low
                  high cost * high Value = high

-> so we need the high cost for every iteration : which means we need to use the MAX-HEAP
```

# CODE
```
class Solution {
  public:
    int minCost(int nn, int mm, vector<int>& x, vector<int>& y) {
        int n = x.size(), m = y.size();
        
        priority_queue<pair<int,int>> q;
        
        for(int i=0;i<n;i++){
            q.push({x[i],1});
        }
        for(int i=0;i<m;i++){
            q.push({y[i],2});
        }
        int hs = 1, vs = 1;
        int ans = 0;   
        
        while(!q.empty()){
            int vl = q.top().first;
            int md = q.top().second;
            q.pop();
            
            if(md == 1){
                ans += (vl * hs);
                vs++;
            }
            else if(md == 2){
                ans += (vl * vs);
                hs++;
            }
        }
        return ans;
    }
};
```
