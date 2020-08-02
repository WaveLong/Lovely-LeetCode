31. Next Permutation

Medium

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be **in-place** and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

```
1,2,3` → `1,3,2`
`3,2,1` → `1,2,3`
`1,1,5` → `1,5,1
```

**解**

对于数组$a[0, ... , n - 1]$，将$i$从后往前枚举，在$a[i + 1, ..., n - 1]$中找出最小的并且大于$a[i]$的数$a[index]$，交换$a[index], a[i]$，然后将$a[i+1, ..., n - 1]$排序

```c++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        for(int i = nums.size() - 1; i >= 0; --i){
            int minNum = INT_MAX, index;
            for(int j = i + 1; j < nums.size(); ++j){
                if(nums[j] > nums[i] && nums[j] < minNum){
                    minNum = nums[j];
                    index = j;
                }
            }
            if(minNum != INT_MAX){
                swap(nums[index], nums[i]);
                sort(nums.begin() + i + 1, nums.end());
                return;
            }
        }
        sort(nums.begin(), nums.end());
        return;
    }
};
```

