# PROBLEM
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/8a51e265-bf93-4713-893a-acf6d8ec4c8c" />
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/6b87a554-57b7-48a9-adb8-822db205e764" />
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/17df836c-d43a-4269-b826-c19201ec47cc" />
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/889ed79c-2c11-4c0d-a309-c6d15260b0c6" />
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/817dbd67-f38d-4752-b6d6-ded42c24d621" />
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/90e94b36-e929-4009-a4a4-90bcbf68deb3" />
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/1ecabb3d-9f1a-41d7-86b6-b6170cdda8ac" />
<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/ea7c8b26-a57e-4d01-9d53-1aa404a93c20" />


# INTUITION

` READ THE QUSTSION CAREFULLY you can came up with brute force easily `

## BRUTE FORCE : O(n^2)
```
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n,q;
	cin >> n >> q;
	vector<int> a(n);
	int tot = 0;
	
	for(int &i : a){
	    cin >> i;
	    tot += i;
	}
	
	vector<pair<int,int>> qu;
	
	for(int i=0; i<q; i++){
	    int x,y;
	    cin >> x >> y;
	    qu.push_back({x,y});
	}
	
	int ans = INT_MAX;
	
	for(int i=0; i<q; i++){
	    int x = qu[i].first;
	    int y = qu[i].second;
	    for(int j=0; j<n; j++){
	        int c1 = 0, c2 = 0;
	        if(a[j] < x){
	            c1 += (x - a[j]);
	        }
	        int rem_sum = tot - a[j];
	        if(rem_sum < y){
	            c2 += (y - rem_sum);
	        }
	        //cout << (c1 + c2) << " ";
	        ans = min(ans, (c1+c2));
	    }
	}
	cout << endl << ans;
}
```

## RUN BRUTE FORCE HERE
https://ideone.com/LsMEIN


## OPTIMAL
<img width="1090" height="330" alt="image" src="https://github.com/user-attachments/assets/772cd600-5777-49f7-ae51-ea5bf4293149" />
<img width="795" height="264" alt="image" src="https://github.com/user-attachments/assets/da84f3b6-bc37-435e-80c9-63ffafa620d3" />
<img width="856" height="498" alt="image" src="https://github.com/user-attachments/assets/1b78d993-e314-4ebe-b849-67ff46a2cdac" />
<img width="733" height="194" alt="image" src="https://github.com/user-attachments/assets/0f52dbfc-d750-4f53-806c-0f8d75df6080" />


```
#include <bits/stdc++.h>
using namespace std;
#define ll long long

int main() {
    int n, q;
    cin >> n >> q;
    vector<ll> a(n);
    ll total = 0;

    for (auto &x : a) {
        cin >> x;
        total += x;
    }

    sort(a.begin(), a.end());

    while (q--) {
        ll x, y;
        cin >> x >> y;

        ll ans = LLONG_MAX;

        // Case 1: Try element >= x
        int idx = lower_bound(a.begin(), a.end(), x) - a.begin();
        if (idx < n) {
            ll curr = a[idx];
            ll c1 = 0; // already >= x
            ll c2 = max(0LL, y - (total - curr));
            ans = min(ans, c1 + c2);
        }

        // Case 2: Try element < x
        if (idx > 0) {
            ll curr = a[idx - 1];   
            ll c1 = x - curr;   
            ll c2 = max(0LL, y - (total - curr));
            ans = min(ans, c1 + c2);
        }

        cout << ans << "\n";
    }

    return 0;
}

//test case 1
// 4 1
// 2 5 1 3
// 5 7

//test case 2
// 3 1
// 1 2 9
// 6 15 
 
// DRY RUN test case 2
// tot = 1 + 2 + 9 => 12
//case 1
// x = 6 we find greater than 6 as
// 9 > 6 so c1 = 0
// y = 15 
// c2 = 15 - (12 - 9) => 15 - 3 => 12
//ans = 12

//case 2
// x = 6 lets take below greater than 6
// 2 < 6 so c1 = 6 - 2 => 4
// y = 15
// c2 = 15 - (12- 2) => 15 - 10 => 5
// ans = 5 + 4 => 9
//take 9 as its min
```

## RUN CODE HERE
https://ideone.com/xmx1XZ
