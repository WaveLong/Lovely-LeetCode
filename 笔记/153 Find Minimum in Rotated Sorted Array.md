153. Find Minimum in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  `[0,1,2,4,5,6,7]` might become  `[4,5,6,7,0,1,2]`).

Find the minimum element.

You may assume no duplicate exists in the array.

**Example 1:**

```
Input: [3,4,5,1,2] 
Output: 1
```

**Example 2:**

```
Input: [4,5,6,7,0,1,2]
Output: 0
```

**解**	二分查找

```c++
class Solution {
public:
    int findMin(vector<int>& nums) {
        // 特殊情况
        if(nums.size() == 1)return nums[0];
        int l = 0, r = nums.size()-1, mid;
        if(nums[r] > nums[l])return nums[l];
        //查找
        while(l <= r){
            mid = (l+r)/2;
            //两种情况对应着断点
            if(nums[mid] > nums[mid+1])return nums[mid+1];
            if(nums[mid-1] > nums[mid])return nums[mid];
            //调整两侧的范围
            if(nums[mid] > nums[0]){
                l = mid + 1;
            }else{
                r = mid - 1;
            }
        }
        return -1;
    }
};
```

