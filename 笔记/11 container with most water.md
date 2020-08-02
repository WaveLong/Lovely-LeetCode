 Container With Most Water

Medium

Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i*is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

 

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

 

**Example:**

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

**分析：注意到水的容量取决于矮的板，当底缩小的时候，若改变移动长的板，水容量必然减少，因此要移动短的板**

```c++
//two pointer，暴力法超时
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n = height.size();
        int maxW = -1, i = 0, j = n - 1;
        while(i < j){
            maxW = max(maxW, min(height[i], height[j]) * (j - i));
            if(height[i] < height[j])i++;
            else j--;
        }
        return maxW;
    }
};
```

