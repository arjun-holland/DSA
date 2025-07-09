![image](https://github.com/user-attachments/assets/c5769d37-4365-4815-9a9c-51fbda416f7b)
![image](https://github.com/user-attachments/assets/968831cf-0e91-4f98-ac85-ddec4c171578)
![image](https://github.com/user-attachments/assets/1235f636-ac60-4232-8037-1be782b984df)
![image](https://github.com/user-attachments/assets/4959031c-9f75-452c-b337-cfef67197a1a)
![image](https://github.com/user-attachments/assets/8cdd8e70-24c8-42a4-a95d-e9b9b84ffc5c)
![image](https://github.com/user-attachments/assets/8d42c68d-6256-4e52-9179-3dddbcd0389f)

---
# code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a,b,k;
    cin>>a>>b>>k;
    cout<<(a%k + b%k)%k;
    cout<<'\n';
    cout<<((a%k)*(b%k))%k;
    cout<<'\n';
    cout<<(a%k -b%k + k)%k;
    return 0;
}
```
