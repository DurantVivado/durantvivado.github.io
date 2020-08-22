---
layout:     post
title:      "什么是前缀树"
subtitle:   " \"What is Trie\""
date:       2020-08-14 10:23:45
author:     "Durant"
latex: true
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
   - 前缀树
   - 经典数据结构   
---



# <面试热点>什么是前缀树Trie？如何实现？

> 前缀树又名**Tries树**、字典树、单词查找树等，常用于快速检索，大量字符串的排序和统计等。
>
> LC208.[实现前缀树](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)

**三个基本性质**

1. 根节点不包含字符，除根节点外每个节点只包含一个字符
2. 从根节点到某个节点，路径上所有的字符连在一起，就是这个节点所对应的字符串
3. 每个节点的子节点所包含的字符都不同



![Trie](https://upload-images.jianshu.io/upload_images/1038472-736d2bc3ddd4b1cc.png?imageMogr2/auto-orient/strip)

**应用场景**：

1.自动补全

![自动补全](https://pic.leetcode-cn.com/963cd3fc83e9618aba9cb78365c8a5bf6b7cef8967da0d204dede7844f6738f2-file_1562596867150)

<p align="center" style="font:italic;color:gray"><i>图1. 谷歌的搜索建议</i></p>

2. 拼写检查

![image.png](https://pic.leetcode-cn.com/4d18efbdd4d51ae3935b42cd59b11d66fb62f1586b9638f9499d2a18fa8919d0-image.png)

<p align="center" style="font:italic;color:gray"><i>图2. 拼写检查</i></p>

3.IP路由（最长前缀匹配）

![无效的图片地址](https://pic.leetcode-cn.com/e3f22b3ab2df82e6c0a7880996749b5e62707e9ef925876e583d666343644526-file_1562596867150)

<p align="center"><i>图 3. 使用Trie树的最长前缀匹配算法，Internet 协议（IP）路由中利用转发表选择路径。</i></p>

4. T9打字预测
5. Boggle单词游戏

还有现成的高效结构如哈希表和平衡树，但为什么我们还要用前缀树呢，因为它有如下优势：

- 找到具有同一前缀的全部键值
- 按词典枚举字符串的数据集

Trie相比于哈希表的另一个优势是，随着哈希表长度增加，会出现大量冲突，时间复杂度可能会增加到$O(N)$. trie树子存储多个具有相同前缀的键时所用空间较少。因此前缀树只需要$O(m)$的空间，m为键长度。而在平衡树中需要$O(m\log n)$。

## **设计Trie树**

**初始化**

我们设计一个Trie节点`node`具有如下属性：

- 子树数组：因为字母表长度为26，所以数组长度为26；
- 结束标记，bool型表示，比如"apple"和"app",后者是前者一个前缀，所以需要结束标记。

```C++
class Trie {
private:
    /** Initialize your data structure here. */
    bool isEnd;
    Trie* next[26];
public:
    Trie()
    {
		isEnd = false;
        memset(next,0,sizeof(next));
    }
};
```



**插入键值**

我们从字符串头开始，如果字符`s[i]`存在于当前节点的子树数组中，那么我们直接递归进入该节点，否则我们创造新节点，再进入。

```C++
   void insert(string word)
   {
       Trie *node = this;
       for(char &c:word)
       {
           if(node->next[c-'a']==NULL)
           node->next[c-'a'] = new Trie(c);
           node = node->next[c-'a'];
       }
   }
```

注意这里我们把this作为根节点。所以每次new一个node都会产生一个根节点。  

* 时间复杂度：$O(m)$，其中 $m$ 为键长。在算法的每次迭代中，我们要么检查要么创建一个节点，直到到达键尾。只需要 $m$ 次操作。

- 空间复杂度：$O(m)$。最坏的情况下，新插入的键和 Trie 树中已有的键没有公共前缀。此时需要添加 $m$ 个结点，使用 $O(m)$ 空间。

**查找键值**

每个键在 trie 中表示为从根到内部节点或叶的路径。我们用第一个键字符从根开始。检查当前节点中与键字符对应的链接。有两种情况：

存在链接。我们移动到该链接后面路径中的下一个节点，并继续搜索下一个键字符。
不存在链接。若已无键字符，且当前结点标记为 End，则返回 true。否则有两种可能，均返回 false :
还有键字符剩余，但无法跟随 Trie 树的键路径，找不到键。
没有键字符剩余，但当前结点没有标记为 End。也就是说，待查找键只是Trie树中另一个键的前缀。



```C++
  
    bool search(string word) {
        if(!this) return false;
    	Trie* node = this;
        for(char &c:word)
        {
            node = node->next[c-'a'];
            if(node==NULL) return false;
        }
        return node->isEnd;
    }
```



**复杂度分析**

- 时间复杂度 : $O(m)$。算法的每一步均搜索下一个键字符。最坏的情况下需要 $m$ 次操作。
- 空间复杂度 : $O(1)$。



**查找 Trie 树中的键前缀**
该方法与在 Trie 树中搜索键时使用的方法非常相似。我们从根遍历 Trie 树，直到键前缀中没有字符，或者无法用当前的键字符继续 Trie 中的路径。与上面提到的“搜索键”算法唯一的区别是，到达键前缀的末尾时，总是返回 true。我们不需要考虑当前 Trie 节点是否用 “End” 标记，因为我们搜索的是键的前缀，而不是整个键。



```C++
bool startWith{
   if(!this) return false;
   Trie* node = this;
   for(char &c:word)
   {
   node = node->next[c-'a'];
   if(node==NULL) return false;
   }
   return true;
  }
```



**复杂度分析**

- 时间复杂度 : $O(m)$。算法的每一步均搜索下一个键字符。最坏的情况下需要 $m$ 次操作。
- 空间复杂度 : $O(1)$。





## 练习题目
下面是一些很好的问题，供您练习使用 Trie 数据结构。

- 添加与搜索单词 - 一个 Trie 树的直接应用。
- 单词搜索 II - 类似 Boggle 的游戏。



## 扩展：删除元素

https://mp.weixin.qq.com/s/uDar0F7x9w5F3sHOB5tIDA