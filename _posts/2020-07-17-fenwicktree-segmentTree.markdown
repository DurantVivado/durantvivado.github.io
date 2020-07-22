---
layout:     post
title:      "线段树和树状数组"
subtitle:   " \"Fenwick Tree & SegmentTree\""
date:       2020-03-26 15:56:27
author:     "Durant"
latex: true
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 高级数据结构
---

> “树状数组和线段树都是用于维护数列信息的数据结构，支持单点/区间修改，单点/区间询问信息。以增加权值与询问区间权值和为例，其余的信息需要维护也都类似。时间复杂度均为***O(logn)***。 ”

# I. 树状数组

## Fenwick Tree

~~[跳过废话，直接看技术实现,对应LC315 ](#build)~~ 

地中海的程序猿们研究数组，时候遇到这样一个问题: 有一个数组$$S$$从$$0 - n-1$$，现在要在$$O(logn)$$ 的时间复杂度内，搜索一个确定的值（或修改）$$w$$并且对区间 $$[a,b]$$ 求和。空间复杂度必须严格限制在$$O(n)$$.

他们想到了二叉搜索树(BST)，对于平衡二叉树其插入和删除的时间复杂度都是$$O(logn)$$，因为树是类似于嵌套列表的思想，进而可以想到二叉堆，这是一种非嵌套列表，也可以实现$$O(logn)$$。于是有了下面这张图：

![FenwickTree](https://images.cnblogs.com/cnblogs_com/AKMer/1228599/o_TreeArray.jpg)

> 解释一下，编号为$$x$$的节点上统计着$$[x-lowbit(x)+1,x]$$这一段区间的信息，$$x$$的父亲就是$$x+lowbit(x)$$,我们要维护数组$$C$$上的信息，存储在数组$$A$$中。

按照Peter M. Fenwick的说法，正如所有的整数都可以表示成2的幂和，我们也可以把一串序列表示成一系列子序列的和。采用这个想法，我们可将一个前缀和划分成多个子序列的和，而划分的方法与数的2的幂和具有极其相似的方式。一方面，子序列的个数是其二进制表示中1的个数，另一方面，子序列代表的$$f[i]$$的个数也是2的幂。

## 1. Lowbit函数

> 返回参数转换为二进制后，最后一个1的位置所代表的数值。

比如34转换为二进制就是0010 0010, Lowbit(34)返回2. 程序上 我们可以用`((Not I)+1) AND I`, 比如NOT(0010 0010) = 1101 1101, 加1之后为 1101 1110，再与上I,为0000 0010(2)。

``` C++
int lowbit(int x)
{
    return x&(-x);
}
```
## 2. 新建数组

我们定义一个数组BIT，用以维护A的前缀和，

$$
BIT_i = \sum\limits_{j=i-lowbit(i)+1}^{i} A_{j}
$$

```C++
void build()
{ 
    for (int i = 1; i <= MAX_N; i++)
    {
        BIT[i] = A[i - 1];
        for (int j = i - 2; j >= i - lowbit(i); j--)
            BIT[i] += A[j];
    }
}
```

## 3. 修改

假设现在要在$$A[i]$$的值增加$$\delta$$, 那么需要将$$BIT$$在所有含$$A[i]$$的区间都加上一个数，
```C++
void add(int k, int w)
    {// 在下标k、加上w
        for(int j = k; j< tr.size();j+=low_bit(j)) tr[j]+=w;
    }

```

## 4. 区间求和

假设我们需要计算$$\sum\limits_{i=1}^kA_i$$的值。
1. 首先，将$$ans$$初始化为$$k$$
2. 将$$ans$$的值加上$$BIT[i]$$
3. 将$$i$$的值减去$$Lowbit(i)$$
4. 重复2 . 3 步骤直到$$i$$的值变为0.

```C++
int sum (int k)
{
    int ans = 0;
    for (int i = k; i > 0; i -= lowbit(i))
        ans += BIT[i];
    return ans;
}
```
应用：求[逆序数](https://blog.csdn.net/cattycat/article/details/5640838)
> 练习 [LC315. 计算右侧小于当前元素的个数](https://leetcode-cn.com/problems/count-of-smaller-numbers-after-self/)


# II. 线段树
## Segment Tree

> 使用线段树可以快速查找某一个节点在若干线段中出现的次数，时间复杂度为$$O(logN)$$，而未优化的空间复杂度为$$2N$$，一般要开$$4N$$的数组防止越界。

![线段树](https://bkimg.cdn.bcebos.com/pic/bd3eb13533fa828bcb5fe85ffe1f4134970a5a09?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2U5Mg==,g_7,xp_5,yp_5)

除了叶子节点外，对于$$[a,b]$$线段节点，其有两个子节点, 左子节点$$[a,(a+b)/2]$$和右子节点$$[(a+b)/2+1,b]$$。由于线段树在程序竞赛中被广泛应用，这种结构被$$ACMer$$和$$OIer$$戏谑为必须掌握的数据结构。一般地，我们先定义一个线段树节点结构体:

```C++
struct SegmentNode
{
    int start;//线段左节点
    int end;//线段右节点
    int sum;//线段对应的和
    int lazytag;//懒标记
    SegmentNode *left;
    SegmentNode *right;
    SegmentNode():start(0),end(0),sum(0){}
};
```
请务必熟悉理解`上述`结构！

## 1. 建立树

我们对区间$$[l,r]$$建立线段树，是一个自上而下过程。

```C++
inline void build(SegmentNode *self, int l, int r)
    {
        if(l>r) return;
        self->start = l;self->end = r;
        if(l==r)
        {
            return;
        }
        int mid = (l+r)>>1;
        self->left = new SegmentNode();
        build(self->left,l,mid);
        self->right = new SegmentNode();
        build(self->right,mid+1,r);
    }
```

## 2. 单点修改

从根节点开始,以递归的方式不断更新sum值，直到叶子节点即`区间长度为1`，每个区间的sum值等于左子区间的sum值，加上右子区间的sum值。

```C++
    inline void add(SegmentNode *self, int pos, int k)
    {
        if(pos<self->start||pos>self->end) return;
        if(self->start == self->end)
        {
            self->sum += k;
            return; 
        }
        if(self->right->start>pos) add(self->left,pos,k);
        else add(self->right,pos,k);
        self->sum = self->left->sum + self->right->sum;
    }
```

## 3. 区间查询

* 第一种情况是当前的区间范围完全在$$[l,r]$$内，这个时候把当前区间的$$sum$$值返回即可，
* 第二张情况是当前节点的`左子节点`的`右端点`和$$[l,r]$$有交集。这个时候就搜索左子节点。
* 第三张情况是当前节点的`右子节点`的`左端点`和$$[l,r]$$有交集。这个时候就搜索右子节点。
```C++
    inline int search(SegmentNode *self, int i,int j)
    {//这里的i,j分别代表要搜索的区间
        if(i>j) return 0;
        if(i<=self->start && self->end<=j)
        {
            return self->sum; 
        }
        int s = 0;
        if(self->left->end>=i) s+=search(self->left,i,j);
        if(self->right->start<=j) s+=search(self->right,i,j);
        return s;
    }
```
## 4. 延迟标记

对于区间修改，这里会遇到一个问题：为了使所有sum值都保持正确，每一次插入操作可能要更新$$O(N)$$个sum值，从而使时间复杂度退化为$$O(N)$$。所以就有了Lazytag，如果一个节点有延迟标记，那么表明这个节点已经被修改过了。

```C++
void add_tag(SegmentNode *self,int l,int r,int v) {
    self->sum += (r-l+1)*v;self->lazytag+=v;//标记只对儿子有影响，自己在打标记的同时一起把统计信息更改了。
}

void push_down(SegmentNode *self,int l,int r) {
    int mid=(l+r)>>1;
    add_tag(self->left,l,mid,self->lazytag);
    add_tag(self->right,mid+1,r,self->lazytag);
    self->lazytag = 0;//把当前标记分别传给两个儿子然后清空
}

inline int search(SegmentNode *self, int l, int r,int v) {//[l,r]为当前区间,[L,R]为要修改的区间
    if(l<=self->start && self->end<=r) {
        add_tag(self,l,r,v);//打标记
        return;
	}
    int s = 0;
    push_down(self,l,r);//下传标记
    if(self->left->end>=i) s+=search(self->left,i,j,v);
    if(self->right->start<=j) s+=search(self->right,i,j,v);
    return s;
}
```

# III. 树状数组和线段树比较
|数据结构|时间复杂度|空间复杂度|适用特点|
|:---:|:---:|:---:|:---:|
|线段树|$$O(logN)$$|O(N)|-|
|树状数组|$$O(logN)$$|O(N)|空间复杂度略低，容易扩展到多维，适用范围较线段树小


<p id = "build"></p>

# C++代码实现(对应LC315)

```C++
#include <iostream>
#include <vector>
#include <algorithm>
#include <unordered_map>
using namespace std;
struct SegmentNode
{
    int start;
    int end;
    int sum;
    SegmentNode *left;
    SegmentNode *right;
    SegmentNode():start(0),end(0),sum(0){}
};
class Solution{
    public:
//---------------------------Segment tree solution----------------------------
    inline void build(SegmentNode *self, int l, int r)
    {
        if(l>r) return;
        self->start = l;self->end = r;
        if(l==r)
        {
            // self->sum = l;
            return;
        }
        int mid = (l+r)>>1;
        self->left = new SegmentNode();
        build(self->left,l,mid);
        self->right = new SegmentNode();
        build(self->right,mid+1,r);
        // self->sum = self->left->sum + self->right->sum;
    }
    inline void add(SegmentNode *self, int pos, int k)
    {
        if(pos<self->start||pos>self->end) return;
        if(self->start == self->end)
        {
            self->sum += k;
            return; 
        }
        if(self->right->start>pos) add(self->left,pos,k);
        else add(self->right,pos,k);
        self->sum = self->left->sum + self->right->sum;
    }
    inline int search(SegmentNode *self, int i,int j)
    {
        if(i>j) return 0;
        if(i<=self->start && self->end<=j)
        {
            return self->sum; 
        }
        int s = 0;
        if(self->left->end>=i) s+=search(self->left,i,j);
        if(self->right->start<=j) s+=search(self->right,i,j);
        return s;
    }
    vector<int> countSmaller_SegmentTree(vector<int>&nums)
    {
        if(!nums.size()) return nums;
        SegmentNode *root = new SegmentNode();
        //find the min and max val in nums
        int min_val = INT_MAX, max_val = INT_MIN;
        for(auto &c:nums){min_val=min(min_val,c);max_val = max(max_val,c);}
        build(root,min_val,max_val);
        vector<int> res(nums.size());
        // for(auto &c:nums) 
        //     add(root,c,1);//All sub interval adds 1
        for(int i = nums.size()-1; i>=0;i--)
        {
            add(root,nums[i],1);
            res[i] = search(root,min_val,nums[i]-1);
        }
        return res;
    }
//------------------------------Fenwick Tree Solution----------------------------------
//Due to the uncertainty of scale of data, we discretize the array
    int n;
    vector<int> tr;
    int low_bit(int x)
    {//pow(2,x)
        return (x&(-x));
    }
    int sum(int k)
    {
        int res = 0;
        for(int j = k; j>0; j-=low_bit(j)) res+=tr[j];
        return res;
    }
   
    void add(int k, int w)
    {// add k to node w
        for(int j = k; j< tr.size();j+=low_bit(j)) tr[j]+=w;
    }
    vector<int> countSmaller_Fenwick(vector<int>&nums)
    {
        if(!nums.size()) return {};
        int n = nums.size();
        vector<int> res(n);
        //First, we discretize the vector and delete the repeated nums
        vector<int> tmp = nums;
        sort(tmp.begin(),tmp.end());
        auto c = unique(tmp.begin(),tmp.end());
        tmp.erase(c,tmp.end());
        int new_len = c - tmp.begin();
        // we define a unordered-map to count the number of tmp
        unordered_map<int,int> ump;
        tr = vector<int>(new_len + 1);//redefine the tr to (new_len+1) default value
        int count = 1;
        for(int i = 0;i<new_len;i++)
            ump[tmp[i]] = count++;//redefine the discretized values into serialized values using hashmap
        //we build the Fenwick tree and do summation and addition
        for(int k = nums.size()-1;k>=0;k--)
        {
            count = ump[nums[k]];// count of number
            res[k] = sum(count-1);
            add(count,1);
        }
        return res;

    }
};
```

> 感谢！有任何问题请在评论区提出，笔者看到会及时回答！