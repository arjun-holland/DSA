# Problem
```
William Macfarlane wants to look at an array.
You are given a list of N numbers and Q queries. Each query is specified by two numbers i and j;
the answer to each query is the sum of every number between the range [i, j] (inclusive).
Note: the query ranges are specified using 0-based indexing.
```
# Input
The first line contains N, the number of integers in our list (N ≤ 100,000). The next line holds N numbers that are guaranteed to fit inside an integer. Following the list is a number Q (Q ≤ 10,000). The next Q lines each contain two numbers i and j which specify a query you must answer (0 ≤ i, j ≤ N-1).

# Output
For each query, output the answer to that query on its own line in the order the queries were made.

# Example
```
Input:
3
1 4 1
3
1 1
1 2
0 2
Output:
4
5
6
```
# Code
```
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n;
	cin>>n;
	vector<int> a(n);
	for(int i=0;i<n;i++)cin>>a[i];
	
	vector<int> pr(n);
	pr[0] = a[0];
	for(int i=1;i<n;i++)pr[i] = pr[i-1]+a[i];
	
	int q;
	cin>>q;
	while(q--){
		int l,r;
		cin>>l>>r;
		cout << pr[r] - pr[l-1]<< endl;
	}
	return 0;
}
```
