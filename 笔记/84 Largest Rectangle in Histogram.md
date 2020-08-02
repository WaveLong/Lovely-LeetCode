84. Largest Rectangle in Histogram

Hard

Given *n* non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

 

![img](https://assets.leetcode.com/uploads/2018/10/12/histogram.png)
Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.

 

![img](https://assets.leetcode.com/uploads/2018/10/12/histogram_area.png)
The largest rectangle is shown in the shaded area, which has area = `10` unit.

 

**Example:**

```
Input: [2,1,5,6,2,3]
Output: 10
```

**解**

解法1	暴力。对于每个条柱，计算最左延申的范围和最右延申的范围，时间复杂度为$O(N^2)$

超时。。。。

解法2	使用栈。对于每个条柱，试图计算它能形成的面积

case1

<div>
    <figure>
        <img src="..\pic\84_case1.png" width=300>
        <figureCaption>case1</figureCaption>
        <img src="..\pic\84_case2.png" width = 300>
    	<figureCaption>case2</figureCaption>
    </figure>
</div>


条柱i的右边界一定是i，不会继续扩展

case2

条柱i的左边界一定是i，不会继续扩展

因此对于case1，计算最大面积；对于case2，将i入栈即可





