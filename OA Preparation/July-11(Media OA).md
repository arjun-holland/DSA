# Problem
<img width="1028" height="554" alt="image" src="https://github.com/user-attachments/assets/99b0e31c-751d-486c-be47-f090bb1db2a3" />

#include<bits/stdc++.h>
using namespace std;

int main(){
    int n;
    cin >> n;
    
    int blockedCells = 0;
    
    vector<vector<int>> mp(n,vector<int>(n,-1));
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            int e;
            cin >> e;
            if(e == -1){
                blockedCells++;
            }else{
                mp[i][j] = e;
            }
        }
    }
    
    
    
    
    return 0;
}
