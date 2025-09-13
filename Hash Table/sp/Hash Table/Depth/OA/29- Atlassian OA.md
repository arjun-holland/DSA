# Problem 
<img width="1599" height="899" alt="image" src="https://github.com/user-attachments/assets/2b3cd80a-3951-497b-bcff-5982140bdc5c" />
<img width="1599" height="899" alt="image" src="https://github.com/user-attachments/assets/f6b804fe-16cc-4e7d-898f-5bc89adf4fac" />
<img width="1599" height="899" alt="image" src="https://github.com/user-attachments/assets/7461448f-5395-42be-b97c-e286dfe21753" />
<img width="1599" height="899" alt="image" src="https://github.com/user-attachments/assets/9ca2de42-85e3-4747-a31b-c17bfe73a42c" />
<img width="1599" height="899" alt="image" src="https://github.com/user-attachments/assets/3fe75e9f-0929-441b-a082-b8f6cef3a1ea" />
<img width="1599" height="899" alt="image" src="https://github.com/user-attachments/assets/5841490a-8b19-46c5-93e1-67a55b1bd96f" />
<img width="1599" height="899" alt="image" src="https://github.com/user-attachments/assets/8819c7a8-5fff-45d9-8461-90a1140cb6fc" />


# INTUITION
<img width="681" height="329" alt="image" src="https://github.com/user-attachments/assets/5e8f68f9-480f-4f9e-b9ea-87e376633f5e" />
<img width="671" height="121" alt="image" src="https://github.com/user-attachments/assets/1028ef8e-1a27-440e-a40d-adf5b9850f05" />
<img width="754" height="427" alt="image" src="https://github.com/user-attachments/assets/8fe920c1-e7a7-46c4-bb12-057ee55f738f" />
<img width="717" height="391" alt="image" src="https://github.com/user-attachments/assets/2a68f413-833e-44a3-ad0c-16a181517857" />
<img width="734" height="401" alt="image" src="https://github.com/user-attachments/assets/4a302e91-d92d-49bf-a2ba-7776219f8e4c" />

```
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n; cin >> n;
	vector<int> a(n);
	for(int &i : a)cin >> i;
	
	//core logic
	unordered_map<int,int> mp; // s[i]-i -> elements sum 
	
	for(int i=0; i<n; i++){
	    int e = a[i]-i;
	    if(mp.find(e) != mp.end()){
	        mp[e] += a[i];
	    }
	    else{
    	    mp[e] = a[i];
	    }
	}
	
	int ans = 0;
	for(auto it = mp.begin(); it != mp.end(); it++){
	    ans = max(ans, it->second);
	}
    cout << ans;
}
```

<img width="897" height="256" alt="image" src="https://github.com/user-attachments/assets/67a22f28-6522-415f-be67-ef32ee967c39" />

