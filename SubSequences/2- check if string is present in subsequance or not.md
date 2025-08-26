# PROBLEM
<img width="775" height="759" alt="image" src="https://github.com/user-attachments/assets/d4d7483e-3f95-4052-8bfa-60c683bb82d4" />
<img width="776" height="108" alt="image" src="https://github.com/user-attachments/assets/cd5906e4-d7f7-4339-9b60-1043eabcafec" />


# CODE
```
class Solution {
public:
    bool isSubSeq(string &s1, string &s2) {
        int i = 0, j = 0;
        int l1 = s1.length(), l2 = s2.length();

        while (i < l1 && j < l2) {
            if (s1[i] == s2[j]) {
                i++;    // move in s1
            }
            j++;     // always move in s2
        }

        return (i == l1); // matched all characters of s1
    }
};
```

<img width="947" height="479" alt="image" src="https://github.com/user-attachments/assets/b2e57f6e-5a99-4845-a512-1001d1d73c39" />
<img width="802" height="290" alt="image" src="https://github.com/user-attachments/assets/bb2e180d-a4e0-4366-a8a9-4352719ceec2" />
