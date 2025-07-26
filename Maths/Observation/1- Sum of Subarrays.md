# Problem
<img width="897" height="675" alt="image" src="https://github.com/user-attachments/assets/a33025cc-a9ee-4373-9db2-67fa641c57b3" />
<img width="834" height="382" alt="image" src="https://github.com/user-attachments/assets/6e70dc76-ae5d-4651-97eb-176ba1816a08" />

---
# Observation
```
a =  [1,2,3] , n = 3 (length of array)
the sub arrays : [1],[2],[3],[1,2],[2,3],[1,2,3] {3*(3+1)/2 => 3*4/2 => 3*2 => 6 subarrays}
here 1 is at index '0' and it is repeated 3 times
            => left length of array -> 0 (there are no previous index then 0)
            => right length of array -> n-0 -> 3-0 -> 3
            => so total freq of 1 is 3 so the sum of 1 which is repeated 3 times is 1 * 3 => 3
     2 is at index '1' and it is repeated 4 times
            => left length of array -> 2 [ at index i the length from index 0 to i is (i+1) ]
                      => the subarrays which has 2 and present in left part are [1,2],[1,2,3]
            => right length of array -> n-1 -> 3-1 -> 2
                      => the subarrays which has 2 and present in right part are [2],[2,3]
            => so total freq of 2 is 4(left part of 2 can combine with any part of right => 2*2 => 4) so the sum of 2  which is repeated 4 times is 2 * 4 => 8
     3 is at index '2' and it is repeated 4 times
            => left length of array -> 3 [ at index i the length from index 0 to i is (i+1) ]
                      => the subarrays which has 3 and present in left part are [3],[2,3],[1,2,3]
            => right length of array -> n-2 -> 3-2 -> 1
                      => the subarrays which has 2 and present in right part are [3]
            => so total freq of 3 is 3(3*1 => 3) so the sum of 3  which is repeated 3 times is 3 * 3 => 9
    Total sum => 3 + 8 + 9
              => 20
```
## The formula for the total number of non-empty subarrays in an array of length n is given by `n * (n + 1) / 2`.
//element * (i + 1) * (n - i)
//i + 1 gives the left length of the array (from index 0 to i)
//n - i gives the right length of the array (from index i to n-1)
<img width="1021" height="459" alt="image" src="https://github.com/user-attachments/assets/650257af-b379-4f17-a960-69471079c10f" />
<img width="1131" height="450" alt="image" src="https://github.com/user-attachments/assets/82a5ec50-a6a2-4df8-a9cd-4900dcdcddbc" />

---

# Code
```
class Solution {
  public:
    int subarraySum(vector<int>& arr) {
        int n = arr.size();
        long long totalSum = 0;
        for(int i = 0; i < n; ++i){
            totalSum += (long long)arr[i] * (i + 1) * (n - i);
        }
        return totalSum;
    }
};

```
