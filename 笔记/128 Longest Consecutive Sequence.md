128. Longest Consecutive Sequence

Hard

3265175Add to ListShare

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(*n*) complexity.

**Example:**

```
Input: [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

**解法1**	排序

**解法2**	hashset

```c++
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int res = 0;
        unordered_map<int, bool>mp;
        for(int x : nums)mp[x] = true;
        for(int x : nums){
            if(!mp[x-1]){
                int cur_num = x, tmp_len = 1;
                while(mp[cur_num + 1]){
                    cur_num += 1;
                    tmp_len += 1;
                }
                res = max(res, tmp_len);
            }
        }
        return res;
    }
};
```

