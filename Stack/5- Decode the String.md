# PROBLEM
<img width="858" height="399" alt="image" src="https://github.com/user-attachments/assets/a345c196-1516-4d56-aa78-9392edb6f808" />
<img width="855" height="603" alt="image" src="https://github.com/user-attachments/assets/5f54f626-3218-48a7-afb2-99cf81843e45" />

# INTUITION
<img width="608" height="279" alt="image" src="https://github.com/user-attachments/assets/f52cdb4d-77c4-4365-8a47-d92f40825f30" />
<img width="754" height="372" alt="image" src="https://github.com/user-attachments/assets/b8ba6885-ee57-496d-93c8-13787d46a980" />
<img width="700" height="454" alt="image" src="https://github.com/user-attachments/assets/8bb7c40a-eb76-4fac-a74d-6892817207b8" />
<img width="627" height="362" alt="image" src="https://github.com/user-attachments/assets/c7b5229f-a500-4292-9529-8caaf061abb0" />


# CODE
```
class Solution {
  public:
    string decodedString(string &s) {
        stack<int> count;         // Stack to store repeat counts (k)
        stack<string> result;     // Stack to store strings at each level before '['
        
        string current = "";      // Current string being built
        int k = 0;                // Current number being read

        // Loop through each character in the input string
        for(char c : s){
            
            // If the character is a digit, build the number (could be >9)
            if(isdigit(c)){
                k = 10 * k + (c - '0');
            }
            
            // If we see '[', we push current k and current string to stacks
            else if(c == '['){
                count.push(k);            // Save current repeat count
                result.push(current);     // Save the string so far
                k = 0;                    // Reset k for the next number
                current = "";             // Start a new current string
            }
            
            // If we see ']', we pop from both stacks and repeat the current string
            else if(c == ']'){
                string previous = result.top(); result.pop(); // Get last string
                int repeat = count.top(); count.pop();        // Get repeat count
                
                // Repeat the current string and append it to previous
                for(int i = 0; i < repeat; i++){
                    previous += current;
                }
                
                // Update current with the combined string
                current = previous;
            }
            
            // If it's a letter, just add it to the current string
            else{
                current += c;
            }
        }

        // Return the final decoded string
        return current;
    }
};

```
