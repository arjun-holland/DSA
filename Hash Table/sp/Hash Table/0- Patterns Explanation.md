```
Pattern 1 : Using General Hash
            Using hash to know the frequency of particular element
            * Unordered Map 
                Key Features : Fast average-case lookup, insertion, and deletion: O(1) , No guaranteed order of elements
                Use Cases :  Frequency counting, Hash-based lookups, Caching / Memoization, Key-value storage where order doesn't matter
            * Ordered Map
                Key Features : Maintains sorted order of keys (by default in C++), Lookup, insertion, and deletion: O(log n)        
                Use Cases : Comparing two maps, Storing sorted data, Range queries, Ordered traversal

Pattern 2 : Hashing + Observation:
            Using hash to know that is the current element exist before in the array or not or
                                    is to know the frquency of current element which exist before before in the array or not
                                    is the relationship with current element exist before in the array or not
                                    
Pattern 3 : Using Hash (unordered_map) To maintain the Global assign Values 
            Maintain in the sence reduce or increase the frequency of the element
            We use this pattern when we need to control/Know that char is exist in all the elements of a container....etc
```

```
Pattern 4 : Prefix Sum + Hashing 
            Given : Need Count , Array
            Problemm : (find count of subarray with Need Count of even or odd ..etc)
            Take map, map[0] = 1 : map initially contains 0 as when (Total Count - Need Count) = 0 that means that subarray is valid
                      simply when we count the valid subarrays then map[0] = 1
            Iterate the Array
                   Update the `Total count` according to the constraints
                   (Total count - (Need Count)) = [Extra Size]
                    if [Extra Size] present in the map then
                        update the ans with freq of [Extra Size]
                    otherwise update the map with current `Total count`

Pattern 5 : Prefix Sum + Hashing
            Given : Array
            Problemm : (find shortet/longest subarray sum ..etc)
            Take map, map[0] = -1 : when (Total Count - Need Count) = 0 that means that subarray is valid
                       simply when we length of the subarray then map[0] = -1, (when 0th index = k, then len = 0-(-1)=1)
            Iterate the Array(i : 0...n-1)
                   Update the `Total count` (total count += a[i])
                   (Total count - (Need Count)) = [Extra Size]
                    if [Extra Size] present in the map then
                        update the length with the index-value of [Extra Size]
                                   //longest sum : len = 0, len = max(len,j-i) for max len
                                   //shortest sum : len = INT_MAX, len = min(len,j-i) for max len
                    if map does not contain the Total Count then
                        update the map with current `Total count` and the index i

```

```
Pattern 6 : Analyzing The Equations (Prefix Sum, Hasing)
            Given : Equation, Array
            Problem : Find the `max value or Min value, array Size` which satisfy the Equation
            -Reduce the Given Equation Mathematiclly and use that Reduced Equation for further process or
                    Ex : If We want to maximize: (nums[i]−nums[j])×nums[k] and with the condition: i < j < k
                                    when we make (nums[i]−nums[j]) maximum it will generate ans max
                                    ans = 0,maxDiff[1] = nums[0]-nums[1], maVal = max(nums[0],nums[1])
                                    iterate k = 2...n:
                                         maxDiff[k] = max(maxDiff[k-1], maxVal - arr[k]) //update the maxDiff                   
                                         ans = max(ans,maxDiff[k-1]*arr[k])
                                         maxVal = max(maxVal, arr[k])  //curr ele max max                           
                        This can be done in O(n) using prefix max and suffix max arrays.                       
            -Analyze the Equaction and use your analytics to reduce the time complexity
                   Ex : If We want to maximize: (nums[i]−nums[j])×nums[k] and with the condition: i < j < k
                                    For each index 𝑗 : (1,n-2) , to make the val max,
                                    we want:
                                       The maximum nums[i] where i<j
                                       The maximum nums[k] where j<k
                                    compute 
                                      (max_prefix_i − nums[j])×max_suffix_k
                        This can be done in O(n) using prefix max and suffix max arrays.

Pattern 6.2 : Analyzing The Problem (Prefix Sum, Suffix Sum)
              Tip: When we got a equation in three or more then three variable use the prefix , suffix arrays
                  to track the max or min elements present before and after at the i'th index and use them.
                                                            or
                   When we need to take the elments from the starting and ending of array use prefix and sufix resfectively
                        Take elements from starting -> prefix
                        Take elements from ending -> suffix
```

```
Pattern 7 : Prefix DIfference Hashing Technique
            Problem : Count Subarrays with Valid condition : freq(a)=freq(b), freq(c)=freq(d), freq(e)=freq(f) .. etc

            Lets us take the problem is find count of subarrays such that freq(a) = freq(b) where array contains only a,b
            Take the subarray i--j is valid,
                       that means the freq(a) = freq(b)
            M1athimatically the freq(a)[i--j] =  freq(b)[i--j]
                        freqA(j) - freqA(i-1) = freqB(j) - freqB(i-1)

                          we have , freq(a) = freq(b)
                      freqA(j) - freqA(i-1) = freqB(j) - freqB(i-1)
                      freqA(j) - freqB(j) = freqA(i-1) - freqB(i-1)  [place the commen terms on one side]
                      the above equation says that
           freqA() - freqB() at j'th index = freqA() - freqB() at (i-1)'th index
           ----------------------------------------------------------------------------------------------------------------------------------------------- 
           when we want subarrays with freq(A) = freq(B) = freq(C)
           then  {freqA()-freqB()} && {freqC()-freqB()} at j'th index = {freqA()-freqB()} && {freqC()-freqB()} at (i-1)'th index 
           -----------------------------------------------------------------------------------------------------------------------------------------------
           when we want subarrays with freq(A) = freq(B) = freq(C) = freq(D) then 
            {freqA()-freqB()} && {freqC()-freqB() && {freqD()-freqC()} at j'th index =
            {freqA()-freqB()} && {freqC()-freqB()  && {freqD()-freqC()} at (i-1)'th index 
           -----------------------------------------------------------------------------------------------------------------------------------------------
           when we want subarrays with freq(a) = freq(b) and freq(c) = freq(d) then 
            {freqA()-freqB()} && {freqD()-freqC()} at j'th index =
            {freqA()-freqB()} && {freqD()-freqC()} at (i-1)'th index 
           ------------------------------------------------------------------------------------------------------------------------------------------------- 
```
