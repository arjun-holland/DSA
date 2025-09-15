# PROBLEM
<img width="728" height="522" alt="image" src="https://github.com/user-attachments/assets/d6dde99b-4aaf-409d-941e-3d13ebe3e2cf" />
<img width="732" height="395" alt="image" src="https://github.com/user-attachments/assets/8cf686e9-3477-4ad7-adaa-f4dbae5eb7bc" />
<img width="748" height="679" alt="image" src="https://github.com/user-attachments/assets/99c1b4fd-cd5c-4196-bcde-58155eccd30b" />
<img width="715" height="194" alt="image" src="https://github.com/user-attachments/assets/6cd338c0-2d4a-4553-8849-aec836c973f6" />
<img width="716" height="267" alt="image" src="https://github.com/user-attachments/assets/4fa40b85-9098-4703-84a1-b17428ed5f92" />

<img width="618" height="170" alt="image" src="https://github.com/user-attachments/assets/710ab0c6-a060-4ebc-a87f-b63fced4e821" />

# CODE
```
#include <iostream>
double power(double N, int P) {
    if (P == 0) {
        return 1;
    } else {
        return N * power(N, P - 1);
    }
}

int main() {
    double N = 2;
    int P = 3;
    double result = power(N, P);
    std::cout << N << "^" << P << " = " << result << std::endl;
    return 0;
}

```
