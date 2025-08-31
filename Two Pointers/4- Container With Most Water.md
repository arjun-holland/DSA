# PROBLEM
<img width="877" height="673" alt="image" src="https://github.com/user-attachments/assets/3b5051ed-dda6-4ec9-a008-5cdb5377c98b" />
<img width="875" height="369" alt="image" src="https://github.com/user-attachments/assets/740c5924-8fef-45ee-b82e-deca9e62b742" />

# INTUITION
```
Even the given array is not in sorted order We are using the two pointers technique here'cause
when we're finding the (how much water can hold)value for the I and J and if we got
that the I th value is lesser than the J th value that means I th building height is less than the JTH building height
So the I th building height affects the answer(ans is min cus I is min)
the I th building affects the answer 'cause water can hold up to that I th building height so we have to move that I th building
As we initialized I = 0, we have to increment that I to I++
```

# CODE
```
class Solution {
  public:
    int maxWater(vector<int> &arr) {
        int i=0,j=arr.size()-1;
        int ans = 0;
        while(i < j){
            int curAns = min(arr[i],arr[j])*(j-i);
            ans = max(ans, curAns);
            if(arr[i] < arr[j])i++;
            else j--;
        }
        return ans;
    }
};
```
