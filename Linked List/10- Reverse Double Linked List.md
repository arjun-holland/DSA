# PROBLEM
<img width="921" height="737" alt="image" src="https://github.com/user-attachments/assets/dcf9eb41-cd5f-4154-bb63-9c872fecfc9b" />
<img width="906" height="674" alt="image" src="https://github.com/user-attachments/assets/f967bb10-9d65-4c9b-979d-079f00f9daae" />

# INTUITION
<img width="750" height="355" alt="image" src="https://github.com/user-attachments/assets/cee31a0c-0a75-4376-80aa-342605950b48" />

![WhatsApp Image 2025-09-03 at 16 45 01_a0692f1f](https://github.com/user-attachments/assets/2c321b83-7781-40fa-9011-ecad2ad1a5da)



# CODE
```
/*
class Node {
  public:
    int data;
    Node *next;
    Node *prev;
    Node(int val) {
        data = val;
        next = NULL;
        prev = NULL;
    }
};
*/

class Solution {
  public:
    Node *reverse(Node *head) {
        Node* cur = head;              // Start from head
        while(cur != NULL){           // Loop through the list
            Node* temp = cur->next;   // Save next node
            cur->next = cur->prev;    // Swap next with prev
            cur->prev = temp;         // Swap prev with saved next (original next)
        
            if(cur->prev == NULL)     // If prev becomes NULL after swap, it's new head
                head = cur;
        
            cur = cur->prev;          // Move to next node (which is now in prev)
        }
        return head;
    }
};
```
