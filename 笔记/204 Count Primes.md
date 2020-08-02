204. Count Primes

Count the number of prime numbers less than a non-negative number, ***n\***.

**Example:**

```
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

**解法1** 埃氏筛法

```c++
class Solution {
public:
    int countPrimes(int n) {
        if(n < 2)return 0;
        vector<bool>isPrime(n, true);
        isPrime[0] = false;
        isPrime[1] = false;
        int ans = 0;
        for(int i = 2; i < n; ++i){
            if(isPrime[i]){
                ans++;
                int k = 2;
                while(k * i < n){
                    isPrime[k*i] = false;
                    k++;
                }
            }
        }
        return ans;
    }
};
```

**解法2**	欧拉筛法（线性筛）

```c++
class Solution {
public:
    int countPrimes(int n) {
        if(n < 3)return 0;
        vector<bool>isPrime(n, true);
        vector<int>Prime(n);
        isPrime[0] = false;
        isPrime[1] = false;
        int cnt = 0;
        for(int i = 2; i <= n -1 ; ++i){
            if(isPrime[i]){
                Prime[cnt++] = i;
            }
            for(int j = 0; j < cnt && i * Prime[j] < n; ++j){
                isPrime[Prime[j]*i] = false;
            }
        }
        return cnt;
    }
};
```

