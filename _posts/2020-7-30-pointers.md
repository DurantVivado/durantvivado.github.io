---
layout:     post
title:      "多指针问题"
subtitle:   " \"Multiple Pointers\""
date:       2020-07-19 15:56:27
author:     "Durant"
latex: true
header-img: "img/post-bg-geek.jpg"
catalog: true
tags:
    - 多指针
    - 算法
---





# 多指针问题

很多时候多指针（双指针，三指针）能极大的帮助我们降低时间复杂度。

比如求链表到数第N个节点，以及判断链表中是否有环。

今天我们看LeetCode 75.[颜色分类](https://leetcode-cn.com/problems/sort-colors/)，原型是荷兰国旗问题。

---

给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

注意:
不能使用代码库中的排序函数来解决这道题。

示例:

```
输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]
```

---

我们用三个指针（p0, p2 和curr）来分别追踪0的最右边界，2的最左边界和当前考虑的元素。

![image.png](https://pic.leetcode-cn.com/5b3d372e0bfb293ca3aac12e90421d7612c9e75b78b579f954c42ebfe74705d4-image.png)

此题思路很直观，本解法的思路是沿着数组移动 curr 指针，若nums[curr] = 0，则将其与 nums[p0]互换；若 nums[curr] = 2 ，则与 nums[p2]互换。

但是细节很需要注意，细节往往能致人于死地。

1. 中间指针curr起始位置为0，不是1，为什么？
2. 若nums[curr]==0，则与nums[p0]互换时curr++，而nums[curr]==1，curr不需要--，为什么？

这两个问题实质是相同的，我们需要让curr在p0前面，去接近p1，相当于给你一个方向，你去前进。这样理解会不会好些。





```C++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        if(!nums.size()) return;
        int begin = 0, mid =0, end = nums.size()-1;
        while(begin<=mid && mid<=end)
        {
            // mid = begin;
            if(nums[mid]==0)
            {
                swap(nums[mid],nums[begin]);
                begin++;
                mid ++;
            }
            else if(nums[mid]==2)
            {
                swap(nums[mid],nums[end]);
                end--;
            }
            else mid ++;
            
        }
    }
};
```

