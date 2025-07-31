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
