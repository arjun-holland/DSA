# PRoblem
<img width="675" height="617" alt="image" src="https://github.com/user-attachments/assets/933b1ba6-5404-4680-8a32-98832b8db99f" />
 
# Intuition
```
-> You are given string a and string b ; you have to output Yes ; if both of the strings can be made equal by doing some specific operations. 

    What are those operations?
  -> You can swap any even index element with any other even index element of same string 
  -> You Can SWAP any odd index element with any other odd index element of same string
```

```
-> Let’s try to solve an easy problem. ->
    You are given string a and b ; you can swap any character in any string with any other character of the same string ; tell me the answer if both can become equal 
                    A = “bghy”
                    B = “ybgh”
As you can swap any character with any other character of the same string it means the order doesn't matter ;
only the quantity matters ;

if “a” is coming for same numbers of times in A and B ; similarly if frequency of “b” is same in both A and B; 
Similarly if frequency of “c” is same in both +  “d” -> is having the same frequency in both the strings.
.
.
.
“Z” -> if all of them are having the same frequency in both the strings this means they can be made equal by doing some swaps.

-> Both the strings will be equal if all the characters from “a” to “z” are having the same frequency in both the strings. 

Algorithm :- > For string A ; create a map1 ; for string B ; create a map2;

                  if(map1 == map2){
                      print(yes)
                  }
                  Else{
                      print(no)
                  }
-> Use a proper function to check equality of two unordered-map for safety purposes. 

TC : - O(N + M); N is the size of first string ; M is the size of second string ; 
SC: - O(constant) -> O(1) 



-> Code : 
          bool equal(map1,map2){
              char g = 'a'
              while(g <= 'z'){
                  if(map1[g]==map2[g]){
                  }
                  else{
                      return false; 
                  }
                  g++;
              }
              return true;
          }
          
          
          -> string x
          -> string y
          
          -> map1{char; int} //character->frequency 
          -> map2{char; int}
          
          i = 0 
          while(i<x.size()){
              char g = x[i] 
              map1[g] = map1[g] + 1 //update the char freq of map1
              i = i + 1 
          }
          
          i = 0 
          while(i < y.size()){
              char g = y[i] 
              map2[g] = map2[g] + 1  //update the char freq of map2
              i = i + 1 
          }
          
          if(equal(map1,map2) == true){
              print(yes)
          }
          else{
              print(no)
          }

Efficient Real Q Sol :->
Create map1 for even indices of string A ; similarly map2 for odd indices of string A ;
Create map3 for even indices of string B ; similarly map4 for odd indices of string B ;

 check the quality 
-> TC : -> O(Sum of length of all the strings)
   SC : -> O(Constant) -> O(1)

```

# Run Code:
https://ideone.com/ctvTdJ
