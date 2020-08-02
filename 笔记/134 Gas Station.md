134. Gas Station

There are *N* gas stations along a circular route, where the amount of gas at station *i* is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from station *i* to its next station (*i*+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1.

**Note:**

- If there exists a solution, it is guaranteed to be unique.
- Both input arrays are non-empty and have the same length.
- Each element in the input arrays is a non-negative integer.

**Example 1:**

```
Input: 
gas  = [1,2,3,4,5]
cost = [3,4,5,1,2]

Output: 3

Explanation:
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.
```

**Example 2:**

```
Input: 
gas  = [2,3,4]
cost = [3,4,3]

Output: -1

Explanation:
You can't start at station 0 or 1, as there is not enough gas to travel to the next station.
Let's start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 0. Your tank = 4 - 3 + 2 = 3
Travel to station 1. Your tank = 3 - 3 + 3 = 3
You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3.
Therefore, you can't travel around the circuit once no matter where you start.
```

**解法1**	暴力求解。验证$\sum_{i=N_s}^k (gas[i]-cost[i]) \geq 0, \forall k \in{N_{s}+1, ..., N-1, 0, 1, ...,N_{s}-1}$是否成立

```c++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int n = gas.size();
        for(int i = 0; i < n; ++i){
            int j = i, cnt = 0;
            int cur_tank = 0;
            bool flag = true;
            while(cnt <= n){
                cur_tank = cur_tank + gas[j] - cost[j];
                j = (j + 1) % n;
                if(cur_tank < 0){
                    flag = false;
                    break;
                }
                cnt++;
            }
            if(flag)return i;
        }
        return -1;
    }
};
```

**解法2**	令$\alpha[i] = gas[i]-cost[i]$。当$total\_tank=\sum_{i=0}^{N-1} \alpha_i \geq 0$时，
$$
\left(\sum_{i=0}^{k-1}+\sum_{i=k}^{N_s -1} + \sum_{i=N_s}^{N-1}\right)\alpha_i \geq 0 
\quad\forall k
$$
第二项肯定小于0，否则起始点会在$N_s$之前。因此$cur\_tank = \left(\sum_{i=N_s}^{N-1}+\sum_{i=0}^{k-1}\right)\alpha_i \geq0$

```c++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int n = gas.size();
        int total_tank = 0, cur_tank = 0;
        int Ns = 0;
        for(int i = 0; i < n; ++i){
            if(cur_tank == 0)Ns = i;
            int d = gas[i] - cost[i];
            cur_tank += d;
            total_tank += d;
            if(cur_tank < 0){
                cur_tank = 0;
            }
        }
        return total_tank < 0 ? -1 : Ns;
    }
};
```



