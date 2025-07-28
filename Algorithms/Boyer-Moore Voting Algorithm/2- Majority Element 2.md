# Problem
<img width="882" height="680" alt="image" src="https://github.com/user-attachments/assets/ff6f41b4-8176-41e7-8fe5-2c8333f5ee40" />


# Intuition
<img width="1038" height="219" alt="image" src="https://github.com/user-attachments/assets/764c8d98-60c0-4998-a313-441d4f995e02" />


# code
```
class Solution {
  public:
    vector<int> findMajority(vector<int>& arr) {
        int tv = arr.size();  // Total number of elements in the array : tv -> total votes
        
        unordered_map<int, int> mp;  // Hash map to count frequency of each element

        // Step 1: Count frequency of each element
        for (int i = 0; i < tv; i++) {
            mp[arr[i]]++;     // Increment count for arr[i]
        }

        vector<int> ans;  // Vector to store elements that appear more than n/3 times

        // Step 2: Check which elements appear more than n/3 times
        for (auto it = mp.begin(); it != mp.end(); it++) {
            int f = it->second;     // Frequency of the element
            int e = it->first;      // The element itself
            if (f > (tv / 3)) {
                ans.push_back(e);    // Add to result if frequency > n/3
            }
        }

        // Step 3: Sort the result in ascending order (as required by many platforms)
        sort(ans.begin(), ans.end());

        return ans;  // Return the final result
    }
};
```


# Optimal Intuition
```
solve the "find all elements that appear more than ⌊n/3⌋ times" problem using the Boyer-Moore Majority Vote algorithm — a very efficient solution with:
✅ Time Complexity: O(n)
✅ Space Complexity: O(1) (constant extra space)

The classic Boyer-Moore algorithm is designed to find a majority element (one that appears more than ⌊n/2⌋ times).
But with a slight modification, we can extend it to find elements that appear more than ⌊n/3⌋ times.
👉 Key idea:
There can be at most 2 elements that appear more than ⌊n/3⌋ times in any array.

📌 Real-World Example:
Let’s say n = 9  Then n/3 = 3
Let’s try:
x appears 4 times
y appears 4 times
z appears 4 times
Then total occurrences = 4 + 4 + 4 = 12 > 9 → ❌ Not possible.

But if only two elements appear > 3 times, say:
x appears 4 times
y appears 4 times
z appears 1 time
Total = 9 → ✅ Possible.

So we just need to track 2 potential candidates and then verify them in a second pass.
```


# Optimal Code
```
class Solution {
  public:
    vector<int> findMajority(vector<int>& arr) {
        int n = arr.size();

        // Step 1: Initialize two potential candidates and their counts
        int candidate1 = -1, candidate2 = -1;
        int count1 = 0, count2 = 0;

        // Step 2: Boyer-Moore Voting Phase
        for (int num : arr) {
            if (num == candidate1) {
                count1++;  // Same as candidate1 → increment count
            }
            else if (num == candidate2) {
                count2++;  // Same as candidate2 → increment count
            }
            else if (count1 == 0) {
                candidate1 = num;  // Replace candidate1
                count1 = 1;
            }
            else if (count2 == 0) {
                candidate2 = num;  // Replace candidate2
                count2 = 1;
            }
            else {
                count1--;  // Decrement both counts
                count2--;
            }
        }

        // Step 3: Verify the counts of the final candidates
        count1 = 0;
        count2 = 0;
        for (int num : arr) {
            if (num == candidate1) count1++;
            else if (num == candidate2) count2++;
        }

        // Step 4: Collect elements that occur more than n/3 times
        vector<int> result;
        if (count1 > n / 3) result.push_back(candidate1);
        if (count2 > n / 3) result.push_back(candidate2);

        // Step 5: Sort the result if needed
        sort(result.begin(), result.end());

        return result;
    }
};

```
