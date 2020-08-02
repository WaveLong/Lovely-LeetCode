53. Maximum Subarray

Easy

5395222Share

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**

If you have figured out the O(*n*) solution, try coding another solution using the divide and conquer approach, which is more subtle.

**解**

动态规划

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int>dp(nums.size() + 1);
        dp[0] = 0;
        dp[1] = nums[0];
        int ans = dp[1];
        for(int i = 2; i < dp.size(); ++i){
            dp[i] = max(dp[i - 1] + nums[i - 1], nums[i - 1]);
            ans = max(ans, dp[i]);
        }
        return ans;
    }
};
```

