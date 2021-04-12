# course_schedule

## 题目截图
 ![](course_schedule.jpg)

## 思路一 图， BFS

 

    class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        # 构建入度表与邻接表
        indegree = [0 for _ in range(numCourses)]
        adjacency = [[] for _ in range(numCourses)]
        queue = []
        for cur, pre in prerequisites:
            adjacency[pre].append(cur)
            indegree[cur] += 1
        
        # 判断是否为有向无环图
        for i, x in enumerate(indegree):
            if not x:
                queue.append(i)
        while queue:
            i = queue.pop()
            for j in adjacency[i]:
                indegree[j] -= 1
                if not indegree[j]:
                    queue.append(j)
        
        for i in indegree:
            if i:
                return False
        
        return True


## 思路二 dfs

关键点在于，若该点在环中，则无论从哪条路径到这了，都会进入环中，故若该点之前判断过，那么可直接返回`True`

使用 flags 记录节点的状态:
- `-1` 代表此前已遍历过,遇到直接返回 `True`
- `1` 代表当前循环遍历过,遇到直接返回 `False`
- `0` 代表未遍历过，对该点 `dfs`


    class Solution:
        def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
            # dfs
            def dfs(i, adjacency, flags):
                if flags[i] == -1: return True
                if flags[i] == 1: return False
                flags[i] = 1
                for j in adjacency[i]:
                    if not dfs(j, adjacency, flags):
                        return False
                flags[i] = -1
                return True
            # 构建入度表与邻接表
            flags = [0 for _ in range(numCourses)]
            adjacency = [[] for _ in range(numCourses)]
            for cur, pre in prerequisites:
                adjacency[pre].append(cur)
    
            # 判断是否为有向无环图
            for i in range(numCourses):
                if not dfs(i, adjacency, flags):
                    return False
            
            return True
