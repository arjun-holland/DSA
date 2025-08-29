# PROBLEM
<img width="982" height="852" alt="image" src="https://github.com/user-attachments/assets/5064bc14-d1c5-43b9-b7eb-3533a963144d" />
<img width="891" height="162" alt="image" src="https://github.com/user-attachments/assets/7de1aeda-8227-4559-9677-121b764078ca" />


# CODE
```
class Solution {
  public:
    string smallestWindow(string &s, string &p) {
        int ans = INT_MAX, si=0, ei=s.length()-1;
        bool valid = false;

        vector<int> pt(26,0);   //know all characters in p
        for(char c : p){
            pt[c-'a']++;
        }
        vector<int> st(26,0);
        int pl = p.length();
        
       //perform sliding window Technique

        int i=0,j=0,n=s.length();
        while(j < n){
            char c = s[j];
            st[c-'a']++;
            if(pt[c-'a'] != 0){      //if the character present in the pt vector
                int pcf = pt[c-'a'];
                int scf = st[c-'a'];
                if(pcf == scf){
                    pl -= pcf;   //reduce the length when frequencies are same
                }
            }
            
            while(pl == 0 && i <= j){  //when pl = 0 means we are having the subarray which contains all the characters of p 
                valid = true;    //as we find the valid subarray
                if(ans > (j-i+1)){  //update the length
                    ans = min(ans,j-i+1);
                    si = i;
                    ei = j;
                }
                char c = s[i];   //try to reduce the shrink of the subarray
                if(pt[c-'a'] != 0){  
                    int pcf = pt[c-'a'];
                    int scf = st[c-'a']; 
                    if(pcf == scf){
                        pl += pcf;      //increase the length as we  going to  remove the necessary character
                    }
                }
                st[c-'a']--;    // remove the necessary character
                i++;
            }
            j++;
        }
        if(!valid) return "";
        int le = ei-si+1;  //to know the length
        return s.substr(si,le);  //s.substr(start_index, length)
    }
};
```
