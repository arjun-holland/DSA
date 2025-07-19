# Problem
<img width="1215" height="292" alt="image" src="https://github.com/user-attachments/assets/ec5cc241-a4b4-4221-aaf0-3900a4fceece" />

# Intuition
<img width="1159" height="680" alt="image" src="https://github.com/user-attachments/assets/55336bdb-cb1a-4016-9667-0bb13bc916bf" />
<img width="1048" height="683" alt="image" src="https://github.com/user-attachments/assets/4a895d4b-dbe7-4d07-a6e3-caca4c702c83" />


# Code
```
class Solution {
public:
    vector<string> removeSubfolders(vector<string>& f) {
        // Step 1: Put all folders into an unordered_set for O(1) average lookups
        unordered_set<string> s(f.begin(), f.end());

        vector<string> v;  // This will hold the final folders after removal of subfolders

        // Step 2: Iterate over each folder string in f
        for(string& c : f) {
            bool issubfold = false; // Flag to mark if current folder is a subfolder

            string t = c;  // Save original folder path because 'c' will be modified

            // Step 3: Keep cutting the last directory part to check its parents
            while(!c.empty()) {
                auto p = c.find_last_of('/');   // Find the last '/' character in 'c'

                c = c.substr(0, p);  // Get the substring from start to last '/'

                // Step 4: Check if this substring (parent folder) exists in the set
                if(s.find(c) != s.end()) {
                    issubfold = true;  // If parent folder exists, current folder is a subfolder
                    break;
                }
            }

            // Step 5: If no parent folder was found in the set, add to result
            if(!issubfold) v.push_back(t);
        }

        return v;
    }
};

```

# Code 2
```
class Solution {
public:
    vector<string> removeSubfolders(vector<string>& folders) {
        unordered_set<string> folderSet(folders.begin(), folders.end());  // Store all folders for O(1) lookup
        vector<string> result;

        for (const string& folder : folders) {
            string temp = folder;  // Keep original folder intact
            bool isSubfolder = false;

            // Peel off each parent directory from the end
            while (true) {
                size_t pos = temp.find_last_of('/');  // Find last '/'
                if (pos == string::npos) break;       // No more parent folders

                temp = temp.substr(0, pos);  // Get parent folder path

                if (folderSet.find(temp) != folderSet.end()) {
                    isSubfolder = true;  // Found a parent folder in the set
                    break;
                }
            }

            if (!isSubfolder) {
                result.push_back(folder);  // Add only if not a subfolder
            }
        }

        return result;
    }
};

```
