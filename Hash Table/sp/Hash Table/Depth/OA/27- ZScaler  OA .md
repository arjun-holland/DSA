# Problem
<img width="664" height="527" alt="image" src="https://github.com/user-attachments/assets/ab5a0347-3351-4889-af2d-1cddd32e49e8" />
<img width="899" height="1599" alt="image" src="https://github.com/user-attachments/assets/d2b522a5-ba44-4bb3-ab7e-1e71d3dc637b" />
<img width="899" height="1599" alt="image" src="https://github.com/user-attachments/assets/4e964790-a437-4774-88dc-e3fa973efef5" />


# Intuition
## Brutre Force : O(n ^ 2) 
```
-> n
-> b[n+1]

count = 0 
for(int i=1;i<=n;i++){
    sum = 0 
    for(j=i;j<=n;j++){
        sum = sum + a[j]   //[i....j]
        focus_sum = sum - (a[i] + a[j])
        
        if(a[i]==a[j] && focus_sum==a[i]){
            count=count+1
        }
    }
}
print(count)
```

```
int main() {
    int n;
    cin >> n;

    vector<int> capacity(n);
    for (int i = 0; i < n; i++) {
        cin >> capacity[i];
    }
    int count = 0;

    //step 1: Try all subsegments of length >= 3
    for (int l = 0; l < n; l++) {
        for (int r = l + 2; r < n; r++) {
            int left = capacity[l];
            int right = capacity[r];

            //step 2: Sum from l+1 to r-1
            int sum = 0;
            for (int k = l + 1; k < r; k++) {
                sum += capacity[k];
            }

            //step 3 : increment count
            if (left == right && left == sum) {
                count++;
            }
        }
    }
    cout << count << endl;
    return 0;
}
```

## Optimal 
<img width="735" height="424" alt="image" src="https://github.com/user-attachments/assets/449e7bd3-cb99-4581-a0ae-da793d421434" />
<img width="725" height="395" alt="image" src="https://github.com/user-attachments/assets/02deb32d-4ea8-4ae3-b4e3-5473972b7a7f" />
<img width="717" height="415" alt="image" src="https://github.com/user-attachments/assets/4c4b3ebd-42b4-48ae-889c-dce3b94b1700" />
<img width="656" height="424" alt="image" src="https://github.com/user-attachments/assets/667dd935-0fab-4264-950a-6e46d2fde211" />

    
<img width="744" height="401" alt="image" src="https://github.com/user-attachments/assets/922c2333-6fd3-4de8-8c40-7103c2ba0acd" />

`As we need to know whether a[j] == a[i] (first and last elemety should be same) then only the subarray is valid for checking that we have to add 
              map<pair<int,int>,int> mp ===> <<number, sum>, frequency of sum >`

<img width="721" height="111" alt="image" src="https://github.com/user-attachments/assets/d3fe0687-cde3-44aa-9985-3547ea78314f" />


<img width="1600" height="980" alt="image" src="https://github.com/user-attachments/assets/987a16bf-fd82-488a-8319-fd4f5a7f0baa" />


```
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n);
    for (int &i : a) cin >> i;

    // Prefix sum array
    vector<long long> prefix(n);
    prefix[0] = a[0];
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + a[i];
    }

    long long ans = 0;
    map<pair<long long, long long>, long long> mp;       // (endpoint value, prefix sum)

    for (int j = 0; j < n; j++) {
        long long sum = prefix[j];
        long long number = a[j];
        long long focus_sum = sum - number;   //sole this equ, g = prefix[j] - (2*a[j]);
        long long g = focus_sum - number;

        // Count matches
        ans += mp[{number, g}];

        // Store current endpoint and prefix sum
        mp[{number, sum}]++;
    }

    cout << ans;
}

```

# If the a[i] == a[j] condition is not required then the below code accepted
<img width="958" height="163" alt="image" src="https://github.com/user-attachments/assets/adaa1330-02c4-4ab6-a9d9-ad26aa15a9bc" />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n;
	cin>>n;
	vector<int> a(n);
	for(int &i : a)cin >> i;
	
	vector<int> prefix(n);
	prefix[0] = a[0];
	
	for(int i=1;i<n;i++){
	    prefix[i] = prefix[i-1] + a[i];
	}
	
	int ans = 0;
	map<int,int> mp;
	for(int j=0; j<n; j++){
	    int g = prefix[j] - (2*a[j]);
	    if(!mp.empty() && mp.count(g)){
	        ans += mp[g];
	    }else{
	        mp[prefix[j]]++;
	    }
	}
    cout<<ans;
}

 ```
