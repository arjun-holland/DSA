# PROBLEM
<img width="916" height="619" alt="image" src="https://github.com/user-attachments/assets/4ffa1b5c-b06d-41eb-917c-0e95cced37ae" />
<img width="936" height="877" alt="image" src="https://github.com/user-attachments/assets/154d3be5-fa6b-44e7-a9c5-60e78b7843e0" />
<img width="902" height="229" alt="image" src="https://github.com/user-attachments/assets/b09e997f-9890-4ad8-926b-166410548c8a" />
<img width="968" height="262" alt="image" src="https://github.com/user-attachments/assets/f26d0c85-f091-46ac-9bd1-68d59bf71b27" />


# INTUITION
<img width="876" height="236" alt="image" src="https://github.com/user-attachments/assets/dc6d1887-0e1f-4da1-bb46-bfcdec0fa58a" />
<img width="987" height="409" alt="image" src="https://github.com/user-attachments/assets/4b832ea7-e412-4a21-a52c-d67a49a4156c" />
<img width="950" height="566" alt="image" src="https://github.com/user-attachments/assets/46eb2fc1-38b7-4627-9c75-2a86af087f6f" />
<img width="932" height="529" alt="image" src="https://github.com/user-attachments/assets/bc59af5b-fdfd-4dc4-976b-920085a2199d" />

## BRUTE FORCE CODE
```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

// Recursive function
// idx = current operation index
// val = current value after applying some ops
// ops = list of operations
// nums = numbers with those operations

ll solve(int idx, ll val, vector<char> &ops, vector<ll> &nums, int b) {
    if (idx > b) return val;  // base case: all operations processed

    ll best = val; // option: skip the operation

    char g = ops[idx];
    if (g == '+') {
        best = max(best, solve(idx+1, val + nums[idx], ops, nums, b));
    }
    else if (g == '-') {
        best = max(best, solve(idx+1, val - nums[idx], ops, nums, b));
    }
    else if (g == '*') {
        best = max(best, solve(idx+1, val * nums[idx], ops, nums, b));
    }
    else if (g == '/') {
        if (nums[idx] != 0)  // avoid division by zero
            best = max(best, solve(idx+1, val / nums[idx], ops, nums, b));
    }
    else if (g == 'N') {
        best = max(best, solve(idx+1, -val, ops, nums, b));
    }

    return best;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int t; cin >> t;
    while (t--) {
        int b; cin >> b;
        vector<char> ops(b+1);
        vector<ll> nums(b+1, 0);  //0->N

        for (int i=1; i<=b; i++) {
            char g; cin >> g;
            ops[i] = g;
            if (g=='+' || g=='-' || g=='*' || g=='/')
                cin >> nums[i];
        }

        // start recursion with value = 1
        cout << solve(1, 1, ops, nums, b) << "\n";
    }
    return 0;
}

```



# CODE:: TC - O(n) SC - O(n)  
```
#include<bits/stdc++.h>
using namespace std;
typedef long long int ll;
#define rep(i, l, r) for ((i) = (l); (i) <=(r); (i)++)
#define rep1(i, r, l) for ((i) = (r); (i) >=(l); (i)--)

ll max(ll a,ll b,ll c)
{
    return max(a,max(b,c)) ; 
}
ll min(ll a,ll b,ll c)
{
    return min(a,min(b,c)) ;
}

int main()
{
  	ios_base::sync_with_stdio(false) ; 
  	cin.tie(NULL);
    cout.tie(NULL);

    ll t ; 
    cin>>t;
    while(t--)
    {
      ll b; 
      cin>>b ; 
      ll i ; 
      ll dp1[b+1];  //dp1[i] has the max value paddy can make till i index
      ll dp2[b+1];  //dp2[i] has the min value paddy can make till i index
      dp1[0]=1;
      dp2[0]=dp1[0];
      rep(i,1,b)
      {
          char g ; 
          cin>>g ; 
          if(g=='+')
          { ll e ; cin>>e;
              dp1[i] = max(dp1[i-1]+e,dp2[i-1]+e,dp1[i-1]) ; 
              dp2[i] = min(dp1[i-1]+e,dp2[i-1]+e,dp2[i-1]) ;   
          }
          else if(g=='-')
          { ll e ; cin>>e;
              dp1[i] = max(dp1[i-1]-e,dp2[i-1]-e,dp1[i-1]) ; 
              dp2[i] = min(dp1[i-1]-e,dp2[i-1]-e,dp2[i-1]) ; 
          }
          else if(g=='*')
          { ll e ; cin>>e;
              dp1[i] = max(dp1[i-1]*e,dp2[i-1]*e,dp1[i-1]) ; 
              dp2[i] = min(dp1[i-1]*e,dp2[i-1]*e,dp2[i-1]) ; 
          }
          else if(g=='/')
          { ll e ; cin>>e;
              dp1[i] = max(dp1[i-1]/e,dp2[i-1]/e,dp1[i-1]) ; 
              dp2[i] = min(dp1[i-1]/e,dp2[i-1]/e,dp2[i-1]) ; 
          }
          else{
              dp1[i] = max(-1*dp1[i-1],-1*dp2[i-1], dp1[i-1]) ; 
              dp2[i] = min(-1*dp1[i-1],-1*dp2[i-1], dp2[i-1]) ;
          }
     }
     cout<<dp1[b]; 
     cout<<"\n";    
  }   							
	return 0;
}

```
# CODE: TC - O(n) SC - O(n)
```
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

/*
dpMax[i] = maximum energy achievable after considering first i balloons
dpMin[i] = minimum energy achievable after considering first i balloons

For each balloon:
  - We can skip it → keep dpMax[i-1], dpMin[i-1]
  - Or we can take it → apply the operation to both dpMax[i-1] and dpMin[i-1]
Then take max/min accordingly.

Operations:
 + x : add x
 - x : subtract x
 * x : multiply x (x >= 0, monotone)
 / x : divide by x (x > 0, monotone with truncation)
 N   : negate (flip signs, max becomes -min, min becomes -max)
*/

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int T;
    cin >> T;
    while (T--) {
        int B; 
        cin >> B;

        // DP arrays, 0-based index (dp[0] = initial state)
        vector<ll> dpMax(B+1), dpMin(B+1);

        // Base case: start energy = 1
        dpMax[0] = dpMin[0] = 1;

        for (int i = 1; i <= B; i++) {
            char op;
            cin >> op;

            ll takeMax, takeMin; // values if we take this balloon

            if (op == 'N') {  // Negation flips the interval
                takeMax = -dpMin[i-1];
                takeMin = -dpMax[i-1];
//dpMin[i-1] = -10
//dpMax[i-1] = +5
//Old set:   [-10 ... 5]
//New set:   [-5 ... 10]   (because -(-10) = +10, and -(+5) = -5)
//takeMax = -dpMin[i-1]   // negating the smallest gives the largest
//takeMin = -dpMax[i-1]   // negating the largest gives the smallest
            } else {
                ll x;
                cin >> x;

                if (op == '+') {
                    takeMax = dpMax[i-1] + x;
                    takeMin = dpMin[i-1] + x;
                } 
                else if (op == '-') {
                    takeMax = dpMax[i-1] - x;
                    takeMin = dpMin[i-1] - x;
                } 
                else if (op == '*') {
                    takeMax = dpMax[i-1] * x;
                    takeMin = dpMin[i-1] * x;
                } 
                else if (op == '/') {
                    takeMax = dpMax[i-1] / x;
                    takeMin = dpMin[i-1] / x;
                } 
                else {
                    // invalid op, just skip
                    takeMax = dpMax[i-1];
                    takeMin = dpMin[i-1];
                }
            }

            // Now decide: either skip or take
            dpMax[i] = max(dpMax[i-1], takeMax);
            dpMin[i] = min(dpMin[i-1], takeMin);
        }

        cout << dpMax[B] << "\n";
    }
    return 0;
}

```

# CODE: TC - O(n), SC - O(1)
```
#include <bits/stdc++.h>
using namespace std;
using int64 = long long;

/*
 We process B balloons in order. For each balloon we may either:
   - skip it (keep our current energy), or
   - take it (apply the operation to our current energy).

 Invariant:
   mx = maximum energy reachable after processing the balloons seen so far
   mn = minimum energy reachable after processing the balloons seen so far

 Because +x, -x, *x (x>=0), and /x (x>0) are monotone, and N is a sign flip,
 it suffices to update using only (mx, mn). That collapses the exponential
 state space to O(1) per step.
*/

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int T;
    if (!(cin >> T)) return 0;
    while (T--) {
        int B;
        cin >> B;

        // Start energy is exactly 1, so both min and max are 1 initially.
        int64 mx = 1;
        int64 mn = 1;

        for (int i = 0; i < B; ++i) {
            char op;
            cin >> op;

            int64 takeMax, takeMin;

            if (op == 'N') {
                // Negation flips the interval [mn, mx] to [-mx, -mn]
                takeMax = -mn;
                takeMin = -mx;
            } else {
                int64 x; 
                cin >> x;

                if (op == '+') {
                    // Adding a positive shifts the whole set by +x
                    takeMax = mx + x;
                    takeMin = mn + x;
                } else if (op == '-') {
                    // Subtracting a positive shifts the whole set by -x
                    takeMax = mx - x;
                    takeMin = mn - x;
                } else if (op == '*') {
                    // Multiplying by non-negative keeps order: extremes map to extremes
                    // (If x could be negative, we'd need to swap, but problem uses x >= 0.)
                    takeMax = mx * x;
                    takeMin = mn * x;
                } else if (op == '/') {
                    // Division by positive (integer, truncates toward zero in C++) is monotone
                    // so extremes map to extremes as well.
                    // Assumes x > 0 as per problem statement.
                    takeMax = mx / x;
                    takeMin = mn / x;
                } else {
                    // Unknown op: treat as skip (defensive)
                    takeMax = mx;
                    takeMin = mn;
                }
            }

            // Option to skip vs. take:
            mx = max(mx, takeMax);
            mn = min(mn, takeMin);
        }

        cout << mx << '\n';
    }
    return 0;
}

```
