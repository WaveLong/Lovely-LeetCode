179. Largest Number

Given a list of non negative integers, arrange them such that they form the largest number.

**Example 1:**

```
Input: [10,2]
Output: "210"
```

**Example 2:**

```
Input: [3,30,34,5,9]
Output: "9534330"
```

**Note:** The result may be very large, so you need to return a string instead of an integer.

**解**	使用排序，自定义比较函数：对于数字a, b

+ 如果ab > ba，则a > b
+ 如果ab < ba，则a < b

然后调用sort函数

```c++
class Solution {
public:
    string largestNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end(), cmp);
        string ans;
        for(int x : nums)ans += to_string(x);
        while(ans.size() > 1 && ans[0] == '0')ans.erase(0, 1);
        return ans;
    }
    static bool cmp(int n1, int n2){
        int len1 = 0, len2 = 0;
        int tmp1 = n1, tmp2 = n2;
        do{
            len1++;
            n1 /= 10;
        }while(n1 != 0);
        do{
            len2++;
            n2 /= 10;
        }while(n2 != 0);
        return tmp1 * pow(10, len2) + tmp2 > tmp1 + tmp2 * pow(10, len1);
    }
};
```

