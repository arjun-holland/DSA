# Problam
<img width="949" height="291" alt="image" src="https://github.com/user-attachments/assets/cf903689-f4b5-4f49-b996-c1fc9b8c9798" />


# Code
```
#include <bits/stdc++.h> 
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n);
    vector<int> b(n);
    
    unordered_map<int,int> mpA;
    unordered_map<int,int> mpB;
    
    for(int &i : a){
        cin >> i;
        mpA[i]++;
    }
    
    for(int &i : b){
        cin >> i;
        mpB[i]++;
    }
    
    int ans = 0;
    
    for(auto it = mpA.begin(); it != mpA.end(); it++){
        int e = it->first;
        int c = it->second;        //freq of A
        int ct = 0;
        for(int se = e; se <= 1000005; se += e){ 
            ct += mpB[se];
        }
        ct = ct * c;
        ans += ct;
    }
    cout << ans;
}
    
```
<img width="793" height="616" alt="image" src="https://github.com/user-attachments/assets/48beb5c2-d842-4966-9ad5-90a444459724" />

<img width="768" height="206" alt="image" src="https://github.com/user-attachments/assets/154bbb54-7cea-4dd0-aa06-7581794e1ad9" />



## 🧠 JDoodle Interactive Demo

You can test and run the solution online using the following JDoodle link:

👉 [Try the Blackbox Method Code on JDoodle](https://www.jdoodle.com/ga/1zaYQPBc0ILhcylvKZdM%2BQ%3D%3D)

This demonstrates the optimized `O(N log N)` solution for counting valid pairs \((A[i], B[j])\) such that \(B[j] \mod A[i] = 0\).  
The method leverages frequency mapping and harmonic progression to efficiently compute results for large inputs.

