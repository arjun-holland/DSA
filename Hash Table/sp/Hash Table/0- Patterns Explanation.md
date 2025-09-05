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
            Problemm : (find array with Need Count of even or odd or array sum ..etc)
            Take map, map[0] = 1 : as map initially contains 0
            Iterate the Array
                   Update the `Total count` according to the constraints
                   (Total count - (Need Count)) = [Extra Size]
                    if [Extra Size] present in the map then
                        update the ans with freq of [Extra Size]
                    otherwise update the map with current `Total count`
```

