---
layout:     post
title:      "初认识-单调栈"
subtitle:   " \"What is MonoStack\""
date:       2020-08-14 10:23:45
author:     "Durant"
latex: true
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
   - 栈
---



# 初认识-单调栈

- 84. [柱状图中最大矩形（Hard）](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)
  85. 求最大矩形(Hard)

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

 ![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram.png)



以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 [2,1,5,6,2,3]。



![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram_area.png)

图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。

 

**示例:**

```
输入: [2,1,5,6,2,3]
输出: 10
```

---

这道题无论是暴力还是枚举均会超时（时间复杂度$O(N^2)$），最初的想法是用一个哈希表存`heights`中每一个高度「最长的横向距离」，最大面积等于`max(maxArea,heights[i]×len)`后来发现过于麻烦。但是直觉告诉我这是可行的，题解采用单调栈也验证了我的想法。

有一个*事实*需要注意：

- 若后一个高度小于前一个高度，那么前一个高度将不会对后续的求最大面积操作产生影响。

我们需要对$i$左右进行扩展，我们需要找到**左右两侧最近且高度小于$h$的柱子，这和接雨水那一题非常相似**。以

$[6,7,5,2,4,5,9,3]$为例，

1. 将6入栈，6左侧为哨兵，位置-1；
2. 将7入栈，由于7>6，故7不会被移除；
3. 将5入栈，由于7>5且6>5，故6，7会被移除。此时栈为空，5左侧为哨兵，位置-1.
4. 将2入栈，由于2<5，5会被移除，2左侧为哨兵-1.
5. 将4入栈
6. 将5入栈
7. 将9入栈
8. 不断出栈直到遇到2<3

$$
\begin{array}\\
1.[6(0)]\\
2.[6(0),7(1)]\\
3.[5(2)]\\
4.[2(3)]\\
5.[2(3),4(4)]\\
6.[2(3),4(4),5(5)]\\
7.[2(3),4(4),5(5),9(6)]\\
8.[2(3),3(7)]
\end{array}
$$



这样以来我们得到左侧柱子的编号为$[-1,0,-1,-1,3,4,5,3]$，同样地，我们可以得到右侧柱子的编号$[2,2,3,8,7,7,7,8]$。  因而根据$(l\_height-r\_height-1)*height[i]$得到最大面积。

代码如下：

​	 

```C++
class Solution {
public:
    
    int largestRectangleArea(vector<int>& heights) {
     if(!heights.size()) return 0;
     int n = heights.size();
     int maxArea = INT32_MIN;
    //采用单调栈的思想，分别找到i左右两侧最近且高度小于h的柱子
    vector<int> lbound(n,0),rbound(n,0);
    vector<pair<int,int>> lstack,rstack;//存放高度位置和下标
    for(int i = 0; i < n;i++)
    {
        if(lstack.empty()) lbound[i] = -1;//哨兵 
        else if(heights[i] > lstack.back().first) 
        {
            lbound[i] = lstack.back().second;
        }else
        {
            while(!lstack.empty()&&heights[i]<=lstack.back().first)lstack.pop_back();
            if(lstack.empty()) lbound[i] = -1;
            else lbound[i] = lstack.back().second;
        }
        lstack.push_back({heights[i],i});
        
    }
    for(int j = n-1; j >= 0;j--)
    {
        if(rstack.empty()) rbound[j] = n;//哨兵 
        else if(heights[j] > rstack.back().first) 
        {
            rbound[j] = rstack.back().second;
        }else
        {
            while(!rstack.empty()&&heights[j]<=rstack.back().first) rstack.pop_back();
            if(rstack.empty()) rbound[j] = n;
            else rbound[j] = rstack.back().second;
        }
        rstack.push_back({heights[j],j});
        
    }
    // for(auto &c:lbound)
    // printf("%d,",c);
    // printf("\n");
    // for(auto &c:rbound)
    // printf("%d,",c);
    // printf("\n");
    for(int c = 0; c < n;c++)
    {
        if(lbound[c]==-1) maxArea = max(maxArea,rbound[c]*heights[c]);
        else maxArea = max(maxArea,(rbound[c]-lbound[c]-1)*heights[c]);
    }
    return maxArea<0?0:maxArea;
    }
};

```

时间复杂度：$O(2N)$

空间复杂度: $O(4N)$，左右边界以及栈

但是此代码可以简化，把寻找左边界和寻找右边界放在一次迭代中完成。

```C++
 int largestRectangleArea(vector<int>& heights) {
            //84求柱状图的最大矩形，O(N)
            int n = heights.size();
            vector<int> left(n), right(n, n);
            //左右边界数组，维护每个矩形的最大左右宽度
            stack<int> mono_stack;//单调栈
            for (int i = 0; i < n; ++i) {

                while (!mono_stack.empty() && heights[mono_stack.top()] >= heights[i]) {
                    right[mono_stack.top()] = i;
                    mono_stack.pop();
                }
                left[i] = (mono_stack.empty() ? -1 : mono_stack.top());
                mono_stack.push(i);
            }
            
            int ans = 0;
            for (int i = 0; i < n; ++i) {
                ans = max(ans, (right[i] - left[i] - 1) * heights[i]);//计算最大面积
            }
            return ans;
        }
```

可能看代码有些复杂，我们制作一个动画方便理解：





- 85. 求最大矩形
- 