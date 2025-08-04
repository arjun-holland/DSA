# General QUestion
<img width="794" height="198" alt="image" src="https://github.com/user-attachments/assets/9deb0f1e-c587-4a9b-8c57-46b95eb52ba4" />

# Brute Force
```
int main() {
    int n, x, y;
    cin >> n >> x >> y;
    vector<int> b(n + 1, 0);  // Initialize the array with size n + 1

    // Input array
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }

    int c = 0;  // Count of valid subarrays

    // Brute-force approach
    for (int i = 1; i <= n; i++) {
        int cx = 0, cy = 0;  // Counters for x and y
        
        for (int j = i; j <= n; j++) {  // Iterate over subarrays
            if (b[j] == x) {
                cx++;
            }
            if (b[j] == y) {
                cy++;
            }
            if (cx == cy) {
                c++;  // Found a valid subarray
            }
        }
    }
    cout << c << endl;  // Print the result
    return 0;
}
```

# Optimal Code

https://www.jdoodle.com/ga/NPlN7eyS7oX8qKN4oXMQ%2Fg%3D%3D
