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
            //even we get the time to kill (how long that enimy alive), we kill  based on the damage point to , like enimy with more damage point in will die in less time that that enimy has to die first
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

# 🧠 Why Use Greedy with time_to_kill / damage[i]?
```
The code does this:
`double time_to_kill = ceil(health[i] / (double)power);`
double threat_score = time_to_kill / damage[i];
This gives us a "damage efficiency score" — how long it takes to stop 1 unit of damage from an enemy.
Lower score = high damage, low health (fast kill, high threat) → kill earlier
Higher score = low damage, high health (slow to kill, less threat) → kill later

By sorting enemies by this score and killing lowest score first, Bob:

Eliminates the most dangerous per second enemies quickly, and

Reduces cumulative damage as fast as possible.
```

# 🔁 Intuition With Time Flow:
Each second:
- All alive enemies deal damage
- Bob can only reduce health of one enemy
- So the longer you leave high-damage enemies alive, the more damage they stack.
Killing:
- Enemy A (5 seconds to kill, 10 dps) = 50 total damage
- Enemy B (2 seconds to kill, 2 dps) = 4 total damage
Clearly, Bob should kill A before B.
- But if A had very high health and low damage, and B had low health and high damage, you might flip the choice.
- That’s what the time_to_kill / damage[i] ratio quantifies — it helps Bob choose enemies that are:
- "Easiest to kill per damage they deal"

# ✅ Why This Greedy Works:
This greedy approach works because:
- The problem has optimal substructure — the remaining problem after killing one enemy is the same type of problem.
- And it satisfies the greedy choice property — making the locally optimal choice (kill the most threatening enemy now) leads to the globally optimal solution.
