# PROBLEM
<img width="732" height="679" alt="image" src="https://github.com/user-attachments/assets/96128b36-5f32-446f-9033-ff1f6c366bf2" />
<img width="773" height="576" alt="image" src="https://github.com/user-attachments/assets/10cae6bd-d4ef-43ec-91df-8169a3948544" />

# INTUITION
```
Steps To Solve Tower of Hanoi Problem
Let N = No. of Disks 
  Shift ‘N-1’ top disks from ‘A’ to ‘B’, using C.
  Shift last disk from ‘A’ to ‘C’.
  Shift ‘N-1’ disks from ‘B’ to ‘C’, using A
where A = Source Rod, B = Helper Rod, C = Destination Rod


towerOfHanoi(3, A, B, C)
│
├── towerOfHanoi(2, A, C, B)              // Step 1: Move top 2 disks from A → B
│   │
│   ├── towerOfHanoi(1, A, B, C)          // Step 1: Move disk 1 from A → C
│   │   │
│   │   ├── towerOfHanoi(0, A, C, B)      // Base case
│   │   ├── Move Disk 1: A → C
│   │   └── towerOfHanoi(0, B, A, C)      // Base case
│   │
│   ├── Move Disk 2: A → B
│   │
│   └── towerOfHanoi(1, C, A, B)          // Step 3: Move disk 1 from C → B
│       │
│       ├── towerOfHanoi(0, C, B, A)      // Base case
│       ├── Move Disk 1: C → B
│       └── towerOfHanoi(0, A, C, B)      // Base case
│
├── Move Disk 3: A → C                     // Step 2: Move largest disk
│
└── towerOfHanoi(2, B, A, C)              // Step 3: Move 2 disks from B → C
    │
    ├── towerOfHanoi(1, B, C, A)          // Step 1: Move disk 1 from B → A
    │   │
    │   ├── towerOfHanoi(0, B, A, C)      // Base case
    │   ├── Move Disk 1: B → A
    │   └── towerOfHanoi(0, C, B, A)      // Base case
    │
    ├── Move Disk 2: B → C
    │
    └── towerOfHanoi(1, A, B, C)          // Step 3: Move disk 1 from A → C
        │
        ├── towerOfHanoi(0, A, C, B)      // Base case
        ├── Move Disk 1: A → C
        └── towerOfHanoi(0, B, A, C)      // Base case

```
# CODE
```
#include <iostream>
using namespace std;

void towerOfHanoi(int N, char Source_Rod, char Helper_Rod, char Destination_Rod) {
    if (N == 0) {
        return; // Base case: No disks to move
    }

    towerOfHanoi(N - 1, Source_Rod, Destination_Rod, Helper_Rod); // STEP - 1
    cout << "Moving Disk " << N << " From ROD " << Source_Rod << " To ROD " << Destination_Rod << endl; // STEP - 2
    towerOfHanoi(N - 1, Helper_Rod, Source_Rod, Destination_Rod); // STEP - 3
}

int main() {
    int N = 3; // Change the number of disks as needed
    towerOfHanoi(N, 'A', 'B', 'C');
    return 0;
}

```

# RUN HERE
https://ideone.com/Kr9C7z
