# problem
You are given an integer power and two integer arrays damage and health, both having length n.
Bob has n enemies, where enemy i will deal Bob damage[i] points of damage per second while they are alive (i.e. health[i] > 0).
Every second, after the enemies deal damage to Bob, he chooses one of the enemies that is still alive and deals power points of damage to them.
Determine the minimum total amount of damage points that will be dealt to Bob before all n enemies are dead.

# Example :
Input: power = 4, damage = [1,2,3,4], health = [4,5,6,8]
Output: 39
Explanation:
Attack enemy 3 in the first two seconds, after which enemy 3 will go down, the number of damage points dealt to Bob is 10 + 10 = 20 points.
Attack enemy 2 in the next two seconds, after which enemy 2 will go down, the number of damage points dealt to Bob is 6 + 6 = 12 points.
Attack enemy 0 in the next second, after which enemy 0 will go down, the number of damage points dealt to Bob is 3 points.
Attack enemy 1 in the next two seconds, after which enemy 1 will go down, the number of damage points dealt to Bob is 2 + 2 = 4 points.


# Constraints:
- 1 <= power <= 10^4
- 1 <= n == damage.length == health.length <= 10^5
- 1 <= damage[i], health[i] <= 10^4

# Explanation



# code
```
#include <bits/stdc++.h>
typedef long long int ll;
using namespace std;

class Solution {
public:
    long long minDamage(int power, vector<int>& damage, vector<int>& health) {
        int n = damage.size();
        vector<pair<double, int>> threat(n);
        
        // Calculate threat level for each enemy: (time_to_kill / damage[i])
        for (int i = 0; i < n; i++) {
            double time_to_kill = ceil((double)health[i] / power);
            threat[i] = {time_to_kill / damage[i], i};
        }
        
        // Sort enemies by threat level in ascending order
        sort(threat.begin(), threat.end());
        
        ll totalDamage = 0;
        ll cumulativeDamage = accumulate(damage.begin(), damage.end(), 0LL);
        
        for (int i = 0; i < n; i++) {
            int idx = threat[i].second;
            int time_to_kill = ceil((double)health[idx] / power);
            
            // Add the damage dealt by all enemies during the time it takes to kill the current one
            totalDamage += cumulativeDamage * time_to_kill;
            
            // After this enemy is killed, subtract its damage from the cumulative damage
            cumulativeDamage -= damage[idx];
        }
        
        return totalDamage;
    }
};
```
