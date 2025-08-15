# Problem
<img width="1040" height="723" alt="image" src="https://github.com/user-attachments/assets/3e50a46c-2119-4f7b-8361-82e5463f91d6" />

# Code
## Brute Force : O(n^2)
```
#include <bits/stdc++.h>
using namespace std;

int LongestMountain(vector<int> &a)
{

    int ans = 0;  
    int n = a.size(); 
    

    // iterate over the array
    for (int i = 0; i < n; i++)
    {
        int j = i + 1;
        int inc = 0, dec = 0;
       // check weather it make it is increase first or not
        while (j < n && a[j] > a[j - 1])
        {
            inc = 1;
            j++;
        }
        // check weather it is decreasing after checking the increaseing part
        while (j < n && a[j] < a[j - 1])
        {
            dec = 1;
            j++;
        }
        // if mountain
        if (inc && dec)
        {
            ans = max(j - i, ans);
            inc = 0, dec = 0;
        }
    }
    // return maximum length 
    return ans;
}

int main()
{
    vector<int> d = {1, 3, 1, 4,
                     5, 6, 7, 8,
                     9, 8, 7, 6, 5};

    cout << LongestMountain(d)
         << endl;

    return 0;
}
```

## Optimal 1
```
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// longest mountain subarray
int LongestMountain(vector<int> &arr)
{
    int n = arr.size();
    if (n < 3) 
        return 0;
        
    int ans = 0;
    for (int i = 1; i <= n - 2;)
    {
        if (arr[i] > arr[i - 1] and arr[i] > arr[i + 1])
        {
            int count = 0;
            int j = i; 

            while (arr[j] > arr[j - 1] and j > 0)  //left length
                count++, j--;
            while (arr[i] > arr[i + 1] and i <= n - 2)   //right length
                count++, i++;
            ans = max(ans, count);
        }
        else
            i++;
    }
    if (ans > 0)
        return ans + 1;
    return ans;
}

int main()
{
    vector<int> d = {1, 3, 1, 4, 5, 6, 7, 8, 9, 8, 7, 6, 5};
    cout << LongestMountain(d) << endl;
    return 0;
}
```
