# problem 
<img width="1131" height="232" alt="image" src="https://github.com/user-attachments/assets/cb14da7f-5f26-4e6c-b191-fec87240a0e2" />
<img width="1069" height="464" alt="image" src="https://github.com/user-attachments/assets/df545c2f-04ae-4405-ba48-e3251978e638" />
<img width="844" height="227" alt="image" src="https://github.com/user-attachments/assets/bbebc144-4563-4ad9-9642-ee2a5595897b" />


# Intuition
<img width="1151" height="257" alt="image" src="https://github.com/user-attachments/assets/8fba6146-aaa2-4ff4-b3f5-e5e44de9ddc2" />
<img width="1123" height="261" alt="image" src="https://github.com/user-attachments/assets/8dfa12b9-a950-46b9-a755-34f178cefbb2" />
<img width="673" height="169" alt="image" src="https://github.com/user-attachments/assets/e5958643-8657-4304-a9d2-72d57939f7c8" />

## UNDERSTAND THE DRY RUN
![WhatsApp Image 2025-09-05 at 09 03 18_ee017024](https://github.com/user-attachments/assets/d2d331ad-bd76-4775-ad94-68ff06d34b82)

# Code
```
int numberOfSubarrays(vector<int>& nums, int k) {
    unordered_map<int, int> freq;
    freq[0] = 1;   //0 making extra exist in map
    int count = 0, oddCount = 0;

    for (int num : nums) {
        if (num % 2 != 0) oddCount++;

        if (freq.find(oddCount - k) != freq.end()) {  //if the extra part present in map
            count += freq[oddCount - k];  //update the answer
        }

        freq[oddCount]++;  //update the map
    }

    return count;
}
```
