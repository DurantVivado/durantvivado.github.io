# 排序算法汇总











## x.拓扑排序

LC 课程表问题系列：207 210

> 核心特性，对于图G中任何一条有向边$(u,v)$，$u$在排列中都出现在$v$的前面，这样的排列称为「拓扑排序」。

对一个有向无环图(Directed Acyclic Graph简称DAG)G进行拓扑排序，是将G中所有顶点排成一个线性序列，使得图中任意一对顶点u和v，若边(u,v)∈E(G)，则u在线性序列中出现在v之前。通常，这样的线性序列称为满足拓扑次序(Topological Order)的序列，简称拓扑序列。简单的说，由某个集合上的一个偏序得到该集合上的一个全序，这个操作称之为拓扑排序。

在图论中，由一个有向无环图的顶点组成的序列，当且仅当满足下列条件时，称为该图的一个拓扑排序（英语：Topological sorting）：

- 每个顶点出现且只出现一次；
- 若A在序列中排在B的前面，则在图中不存在从B到A的路径。
- 若图中存在环，则不存在拓扑排序

***重点***：如何判断有无环：如果某个节点的相邻节点处于探索状态（在visited中），但还未加入拓扑序列，则说明有环。

```python
from collections import defaultdict
class graph:
    def __init__(self,num):
        self.graph = defaultdict(list)
        self.visited = {} 
    
    def addEdge(self,u,v):
        self.graph[u].append(v)


class Solution:
        
        
    def canFinish(self, numCourses: int, prerequisites: [[int]]) -> bool:
        g = graph(numCourses+1)   
        topo_sort = []
        for lists in prerequisites:
            g.visited[lists[0]] = False
            for i,it in zip(range(1,len(lists)), lists):
                g.graph[lists[i]].append(lists[0])
                g.visited[lists[i]] = False
                
        isLoop = False
        if not prerequisites or not prerequisites[0]: return True
        #只要存在一种拓扑排序，返回true
        #定义三种状态，未探索，探索中以及已经探索
        #A->B: 表示A是B的先修课
        def dfs(vertex):
            nonlocal isLoop
            if isLoop: return
            if not vertex in g.graph.keys():
                g.visited[vertex] = True #标记为已经访问
                topo_sort.append(vertex)
                return #如果已经访问则跳过
            g.visited[vertex] = True #标记为已经访问
            for neigbor in g.graph[vertex]:#遍历邻接顶点
                if not g.visited[neigbor] :
                    dfs(neigbor)
                elif not neigbor in topo_sort:#如果某个节点的相邻节点处于探索状态（在visited中），但还未加入拓扑序列，则说明有环
                    isLoop = True
                    return 
            topo_sort.append(vertex)
        
        for v in g.graph.keys():
            if not isLoop and not g.visited[v]:
                dfs(v)
                
        return not isLoop
    
```

> 复杂度分析

时间复杂度: $O(n+m)$，其中 $n$ 为课程数，$m$ 为先修课程的要求数。这其实就是对图进行深度优先搜索的时间复杂度。

空间复杂度: $O(n+m)$。题目中是以列表形式给出的先修课程关系，为了对图进行深度优先搜索，我们需要存储成邻接表的形式，空间复杂度为 $O(n+m)$。在深度优先搜索的过程中，我们需要最多 $O(n)$ 的栈空间（递归）进行深度优先搜索，并且还需要若干个 $O(n)$ 的空间存储节点状态、最终答案等。
