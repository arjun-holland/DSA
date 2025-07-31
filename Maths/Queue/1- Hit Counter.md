# Problem
<img width="935" height="271" alt="image" src="https://github.com/user-attachments/assets/72836bbd-5857-4c86-82a0-c56a05ae6f81" />

# Intuition
<img width="968" height="114" alt="image" src="https://github.com/user-attachments/assets/f97257ca-52ff-4779-bd04-7ec4c1927c81" />


# Code 1
```
class HitCounter {
    queue<int> hits;
public:
    void hit(int timestamp) {
        hits.push(timestamp);
    }

    int get(int timestamp) {
        while (!hits.empty() && hits.front() <= timestamp - 300) {
            hits.pop();
        }
        return hits.size();
    }
};
Every hit(t) is recorded.
get(t) filters out hits older than 5 minutes.
```

# code 2 - Using a Min-Heap (Priority Queue)
```
class HitCounter {
    priority_queue<int, vector<int>, greater<int>> pq;
public:
    void hit(int timestamp) {
        pq.push(timestamp);
    }

    int get(int timestamp) {
        while (!pq.empty() && pq.top() <= timestamp - 300) {
            pq.pop();
        }
        return pq.size();
    }
};
Same logic as queue.
pq.top() gives the earliest timestamp (like queue front).
```
🔁 Summary of Data Structures:
| Structure                   | Allows Duplicates | Maintains Order | Efficient for this Problem | Comment |
| --------------------------- | ----------------- | --------------- | -------------------------- | ------- |
| `set<int>`                  | ❌ No              | ✅ Sorted        | ❌ Incorrect for duplicates |         |
| `queue<int>`                | ✅ Yes             | ✅ FIFO          | ✅ Best choice              |         |
| `priority_queue` (min-heap) | ✅ Yes             | ✅ Sorted        | ✅ Also works               |         |
