# Problem
<img width="700" height="472" alt="image" src="https://github.com/user-attachments/assets/4b487844-8607-4395-b2ca-ae0434359c7e" />
<img width="749" height="139" alt="image" src="https://github.com/user-attachments/assets/78f555de-003a-4745-8797-63f6826f5c69" />

# Brute Intuition
```
->n->size of the array 
->a[n+1]->1 based indexing 
 
count = 0 
for(i=1;i<=n;i++){
    for(j=i+1;j<=n;j++){
        //-->(i,j)
        if(a[a[a[i]]]==a[a[a[j]]]){
            count = count + 1 
        }
        else{
          //do nothing
        }
    }
}
print(count)
TC :-> O(N*N)
SC :-> O(1) 
```

# Optimal Code

![WhatsApp Image 2025-08-04 at 10 36 21_8fb51aa9](https://github.com/user-attachments/assets/ddbe400c-81ed-46ae-bee3-ee643952e593)

<img width="973" height="352" alt="image" src="https://github.com/user-attachments/assets/c39d4dd4-cf7c-45cb-b632-08bb06f6d599" />

<img width="856" height="355" alt="image" src="https://github.com/user-attachments/assets/7af4ae77-18c2-4566-96db-cf0ad184fda7" />

```
->n->size of the array 
->a[n+1]->1 based indexing

hashmap <int,int> kk; 
count = 0

for(i=1;i<=n;i++){
     //assuming now you are at index j
     RHS = a[a[a[i]]] 
     g = kk[RHS]     //---> it tells how many times RHS has come from 1 to i-1
     count = count + g

     LHS = a[a[a[i]]] 
 
     kk[LHS] = kk[LHS] + 1      //storing the elment in the map maintaining its frequency
}

print(count)

TC :-> O(N)
SC :-> O(N) 
```

<img width="868" height="373" alt="image" src="https://github.com/user-attachments/assets/8fe860d1-41a2-4623-892c-3c6141991661" />
<img width="1051" height="260" alt="image" src="https://github.com/user-attachments/assets/610b48f9-f911-48b0-8e2f-4fe3a738bed3" />

| i | a\[i] | a\[a\[i]] | a\[a\[a\[i]]] | RHS = a\[a\[a\[i]]] |
| - | ----- | --------- | ------------- | ------------------- |
| 1 | 4     | a\[4]=2   | a\[2]=2       | 2                   |
| 2 | 2     | a\[2]=2   | a\[2]=2       | 2                   |
| 3 | 1     | a\[1]=4   | a\[4]=2       | 2                   |
| 4 | 2     | a\[2]=2   | a\[2]=2       | 2                   |

So RHS is 2 for every index.

```
🧠 Hash Map kk Explanation
We count how many times we've seen RHS = 2 so far:
```

| i | RHS = 2 | kk\[2] before | count added | New kk\[2] |
| - | ------- | ------------- | ----------- | ---------- |
| 1 | 2       | 0             | 0           | 1          |
| 2 | 2       | 1             | 1           | 2          |
| 3 | 2       | 2             | 2           | 3          |
| 4 | 2       | 3             | 3           | 4          |

🧮 Final count = 0 + 1 + 2 + 3 = 6

<img width="587" height="252" alt="image" src="https://github.com/user-attachments/assets/5364c73d-d269-4f59-a350-a27a09a8ce81" />

# Code
Run Here : https://ideone.com/d6yEgf
