# Problem
<img width="819" height="471" alt="image" src="https://github.com/user-attachments/assets/17040acb-4552-4519-92bb-2ec9d1eb2500" />


# Intuition
<img width="1120" height="542" alt="image" src="https://github.com/user-attachments/assets/fa25d853-046a-4e2d-9521-ec87828716a1" />
<img width="927" height="440" alt="image" src="https://github.com/user-attachments/assets/2302ea62-4457-41b0-bc34-c5587084b17a" />

<img width="1143" height="481" alt="image" src="https://github.com/user-attachments/assets/5c4d4b66-6f33-49b2-abfd-fd848b9512c5" />
<img width="1139" height="473" alt="image" src="https://github.com/user-attachments/assets/1d9d8118-08fa-4a75-8e2b-0830d54f0bc1" />
<img width="833" height="234" alt="image" src="https://github.com/user-attachments/assets/5048d5bb-935e-43b9-b026-403a45ec8cf0" />
<img width="1132" height="251" alt="image" src="https://github.com/user-attachments/assets/23d9229a-526a-4aa0-90a0-50ca5584aaa2" />



# Code
```
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum of digits of a number
int digSum(int e){
    int sum = 0;
    while(e != 0){
        sum += e % 10;     // Add the last digit
        e /= 10;           // Remove the last digit
    }
    return sum;
}

int main(){
    int n;
    cin >> n;       // Input the size of the array
    vector<int> a(n);

    for(int i = 0; i < n; i++) cin >> a[i];    // Input the elements of the array
    
    unordered_map<int, int> mp;       // Map from digit sum to the largest number with that digit sum
    int ans = -1;                     // To store the maximum sum of any two elements with the same digit sum

    for(int e : a){
        int ds = digSum(e);         // Calculate the digit sum of the current number

        if(mp.find(ds) != mp.end()){        // If we've already seen a number with the same digit sum
            ans = max(ans, mp[ds] + e);    // Update the maximum sum of such a pair
            mp[ds] = max(mp[ds], e);       // Keep the maximum of the two numbers for future comparisons
        } else {
            mp[ds] = e;        // First time seeing this digit sum, store the number
        }
    }

    cout << ans;     // Output the result
    return 0;
}
```

## 🔗 Live Demo

👉 **[Run Code on JDoodle 🚀](https://www.jdoodle.com/ga/A5NzwKPI4nOasu2HOwG6Mw%3D%3D)**
