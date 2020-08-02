Median of Two Sorted Arrays

Hard

There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume **nums1** and **nums2** cannot be both empty.

**Example 1:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

**Example 2:**

```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

**解法1**

空间换时间，先将两个数组归并，然后直接查询

```c++
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    vector<int>ans;
    int i = 0, j  = 0;
    while(i < nums1.size() && j < nums2.size()){
        if(nums1[i] <= nums2[j]){
            ans.push_back(nums1[i++]);
        }else if(nums2[j] <= nums1[i]){
            ans.push_back(nums2[j++]);
        }else{
            ans.push_back(nums1[i++]);
            ans.push_back(nums2[j++]);
        }
    }
    while(i < nums1.size()){
        ans.push_back(nums1[i++]);
    }
    while(j < nums2.size()){
        ans.push_back(nums2[j++]);
    }
    int n = ans.size();
    if(n % 2 == 1)return ans[n / 2];
    else return (ans[n / 2] + ans[n / 2 - 1]) * 0.5;
}
```

**解法2**

递归