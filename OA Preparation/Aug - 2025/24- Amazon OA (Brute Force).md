# PROBLEM
<img width="604" height="504" alt="image" src="https://github.com/user-attachments/assets/9e12336a-b520-4327-be42-4104595ba038" />
<img width="543" height="542" alt="image" src="https://github.com/user-attachments/assets/761d3ed6-7492-41e5-9462-8ae528572c8e" />


# CODE
```
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n;
	cin >> n;
	string data;
	cin >> data;
	
	int k;
	cin>>k;
	vector<vector<int>>queries(k);
	for(int i=0;i<k;i++){
	    int qi, q1v, q2v;  // query index ,  query value 1, query value 2
	    cin >> qi >> q1v >> q2v;
	    vector<int> q = {qi,q1v,q2v};
	    queries[i] = q;
	}
	
	for(int i=0;i<k;i++){
	    int qi = queries[i][0];
	    if(qi == 1){
	        int ci = queries[i][1];
	        char ch = 'a' + queries[i][2] - 1;
	        data[ci-1] = ch;  // we need to follow 0 -based index
	        cout << data << endl;
	    }else{
	        set<char> st;
	        int si = queries[i][1];
	        int ei = queries[i][2];
	        for(int j=si-1; j <= ei-1; j++){
	            st.insert(data[j]);
	        }
	        cout << st.size() << endl;
	    }
	}
}

```
# Time Complexity : O(n * k)
# Space Complexity : O(1)
