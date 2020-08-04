```
layout:     post
title:      "如何让Unordered_map支持pair作为键值"
subtitle:   " \"Pair as key of unordered_map\""
date:       2020-07-16 16:56:27
author:     "Durant"
latex: true
header-img: "img/post-bg-o.jpg"
catalog: true
tags:
   - C++
   - 实用用技巧
```



 # 如何让Unordered_map支持pair作为键值

```cpp
template<class T1, class T2> 
struct pair_hash//没这个pair 就不能在unorder——map快乐的玩耍了
{
    size_t operator() (const pair<T1, T2>& p) const
    {
        return hash<T1>()(p.first) ^ hash<T2>()( p.second);//异或思想
    }
    //如果遇到了<3,5>和<5,3>怎么办，皮神有想法，再把两个hash判断一遍
    
    bool operator()(const pair<T1,T2> &lhs, const pair<T1,T2> &rhs) const
    {
        return equal_to<T1>()(lhs.first,rhs.first) && equal_to<T2>()(lhs.second,rhs.second);
    }
};
//使用
unordered_map<pair<int,int>,double,pair_hash<int,int>,pair_hash<int,int>> minDis;
   minDis.insert({{1,2}, 1.5});
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

像python那样将任何对象变为dict的键值，C++把原有的hash函数删去了（处于性能考虑 )，所以要自己写。

然后用的话就根据需要，正常操作了。

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

嗯 Python中defaultdict有一点好处，就是可以直接用tuple作为键值，这样的话间接解决了list不能作为键值的问题，mark一下