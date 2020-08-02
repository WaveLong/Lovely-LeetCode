16. 3Sum Closest

Medium

Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**Example:**

```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

思路同15，稍作修改，不用考虑去重的问题

```c++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int ans, d = INT_MAX;
        sort(nums.begin(), nums.end());
        int n = nums.size();
        for(int i = 0; i < n - 2; ++i){
            int m = target -nums[i];
            int j = i + 1, k = n - 1;
            while(j < k){
                int temp = nums[j] + nums[k];
                if(abs(temp - m) < d){
                    ans = nums[i] + nums[j] + nums[k];
                    d = abs(temp - m);
                }
                if(temp == m){
                    break;
                }else if(temp < m){
                    j++;
                }else{
                    k--;
                }
            }
        }
        return ans;
    }
};
```

