# Problem
Given a positive integer n, you need to count the numbers less than or equal to n having exactly 9 divisors.

# Examples :
```
Input: n = 100
Output: 2
Explanation: Numbers which have exactly 9 divisors are 36 and 100.

Input: n = 200
Output: 3
Explanation: Numbers which have exactly 9 divisors are 36, 100, 196. 
```
# Constraints:
1 ≤ n ≤ 10^9
*/

# Intuition
<img width="778" height="391" alt="image" src="https://github.com/user-attachments/assets/5502777a-bb23-4b08-9c71-87233b4627b6" />

<img width="880" height="369" alt="image" src="https://github.com/user-attachments/assets/8f034b02-7a9a-4e9f-9f02-713826dc2bc2" />


# Code
```
class Solution {
  public:
    int countNumbers(int n) {
    
        vector<bool> isPrime(ceil(sqrt(n)) + 1, true);
        vector<int> primes;
        
        // Sieve of Eratosthenes
        isPrime[0] = isPrime[1] = false;
        for (int i = 2; i * i <= sqrt(n); i++) {
            if (isPrime[i]) {
                for (int j = i * i; j <= sqrt(n); j += i) {
                    isPrime[j] = false;
                }
            }
        }

        // Collect all primes up to sqrt(n)
        for (int i = 2; i <= sqrt(n); i++) {
            if (isPrime[i]) primes.push_back(i);
        }

        int count = 0;

        // Case 1: p^8 as (8+1) => 9
        for (int i = 0; i < primes.size(); i++) {
            long long num = pow(primes[i], 8);
            if (num <= n) count++;
            else break;
        }

        // Case 2: p^2 * q^2 (p ≠ q) as (2+1)(2+1)=>(3)(3)=> 9
        int sz = primes.size();
        for (int i = 0; i < sz; i++) {
            for (int j = i + 1; j < sz; j++) {
                long long num = 1LL * primes[i] * primes[i] * primes[j] * primes[j];
                if (num <= n) count++;
                else break; // early break
            }
        }
        return count;
    }
};
```
