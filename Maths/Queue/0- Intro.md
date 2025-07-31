<img width="1044" height="116" alt="image" src="https://github.com/user-attachments/assets/dec602a5-cb95-4e52-8c3a-75b1a2677380" />
<img width="883" height="184" alt="image" src="https://github.com/user-attachments/assets/d1cdc59c-e3d7-4a2f-a66f-43d5070a90c9" />
<img width="845" height="197" alt="image" src="https://github.com/user-attachments/assets/b4fc0377-0bc5-4422-915e-6b1936243de8" />
✅ Common Functions of queue with Examples

| Function       | Description                                            | Example Code     |
| -------------- | ------------------------------------------------------ | ---------------- |
| `push(val)`    | Adds `val` to the **back** of the queue                | `q.push(10);`    |
| `pop()`        | Removes the element at the **front**                   | `q.pop();`       |
| `front()`      | Returns a reference to the **front** element           | `q.front();`     |
| `back()`       | Returns a reference to the **last** element            | `q.back();`      |
| `empty()`      | Returns `true` if queue is empty                       | `q.empty()`      |
| `size()`       | Returns the number of elements in the queue            | `q.size();`      |
| `swap(q2)`     | Swaps content with another queue `q2`                  | `q.swap(q2);`    |
| `emplace(val)` | Constructs and inserts element at the back (efficient) | `q.emplace(20);` |

🧪 Example with Output
```
#include <iostream>
#include <queue>
using namespace std;

int main() {
    queue<int> q;

    q.push(10);
    q.push(20);
    q.push(30);

    cout << "Front: " << q.front() << endl; // 10
    cout << "Back: " << q.back() << endl;   // 30
    cout << "Size: " << q.size() << endl;   // 3

    q.pop(); // removes 10
    cout << "After pop, Front: " << q.front() << endl; // 20

    if (q.empty()) cout << "Queue is empty\n";
    else cout << "Queue is not empty\n";

    return 0;
}
```

<img width="911" height="628" alt="image" src="https://github.com/user-attachments/assets/1e7f2b5f-a2ea-4d6a-90dc-aff65f1786de" />
<img width="975" height="497" alt="image" src="https://github.com/user-attachments/assets/545d5659-7d4e-4e6b-a886-79bf51fe6134" />
<img width="789" height="388" alt="image" src="https://github.com/user-attachments/assets/eb66b995-7287-4534-a1c8-a3fa7171af79" />

---
<img width="809" height="280" alt="image" src="https://github.com/user-attachments/assets/5547ede3-c1c5-43b0-8f17-ae2dab88809b" />



