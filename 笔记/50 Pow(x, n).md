50. Pow(x, n)

Implement [pow(*x*, *n*)](http://www.cplusplus.com/reference/valarray/pow/), which calculates *x* raised to the power *n* (xn).

**Example 1:**

```
Input: 2.00000, 10
Output: 1024.00000
```

**Example 2:**

```
Input: 2.10000, 3
Output: 9.26100
```

**Example 3:**

```
Input: 2.00000, -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
```

**解**

折半计算

```c++
class Solution {
public:
    double myPow(double x, int n) {
        double ans = 1;
        if(x == 0)return 0;
        if(n == 0)return 1;
        int t = n;
        while(n){
            if(n & 1)ans *= x;
            x *= x;
            n /= 2;
        }
        
        return t < 0 ? 1 / ans : ans;
    }
};
```

