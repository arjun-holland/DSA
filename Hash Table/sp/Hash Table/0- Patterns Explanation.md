```
Pattern 1 : Using General Hash
            Using hash to know the frequency of particular element

Pattern 2 : Hashing + Observation:
            Using hash to know that is the current element exist before in the array or not or
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
            Take map, map[0] = -1 : Here we need the subarray length when (Total Count - Need Count) = 0 that means that subarray is valid
                       simply when we length of the subarray then map[0] = -1
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
            -Analyze the Equaction and use your analytics to reduce the time complexity
                   Ex : If We want to maximize: (nums[i]−nums[j])×nums[k] and with the condition: i < j < k
                                    For each index 𝑗 : (1,n-2) , to make the val max,
                                    we want:
                                       The maximum nums[i] where i<j
                                       The maximum nums[k] where j<k
                                    compute 
                                      (max_prefix_i − nums[j])×max_suffix_k
                        This can be done in O(n) using prefix max and suffix max arrays.
```

