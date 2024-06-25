# Assignment #D: May月考

Updated 1654 GMT+8 May 8, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)



## 1. 题目

### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
L, m = map(int, input().split())

dp = [1]*(L+1)

for i in range(m):
    s, e = map(int, input().split())
    for j in range(s, e+1):
        dp[j] = 0

print(dp.count(1))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240521204948196](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405212049418.png)



### 20449: 是否被5整除

http://cs101.openjudge.cn/practice/20449/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def divisible_by_5(A):
    current_value = 0
    answer = []

    for digit in A:
        current_value = (current_value * 2 + int(digit)) % 5

        if current_value == 0:
            answer.append('1')
        else:
            answer.append('0')

    return ''.join(answer)

input_str = input()
result = divisible_by_5(input_str)
print(result) 

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240521205632681](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405212056831.png)



### 01258: Agri-Net

http://cs101.openjudge.cn/practice/01258/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
class DisjointSetUnion:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        xr = self.find(x)
        yr = self.find(y)
        if xr == yr:
            return False
        elif self.rank[xr] < self.rank[yr]:
            self.parent[xr] = yr
        elif self.rank[xr] > self.rank[yr]:
            self.parent[yr] = xr
        else:
            self.parent[yr] = xr
            self.rank[xr] += 1
        return True

def kruskal(n, edges):
    dsu = DisjointSetUnion(n)
    mst_weight = 0
    for weight, u, v in sorted(edges):
        if dsu.union(u, v):
            mst_weight += weight
    return mst_weight

def main():
    while True:
        try:
            n = int(input().strip())
            edges = []
            for i in range(n):
                # Since the input lines may continue onto others, we read them all at once
                row = list(map(int, input().split()))
                for j in range(i + 1, n):
                    if row[j] != 0:  # No need to add edges with 0 weight
                        edges.append((row[j], i, j))
            print(kruskal(n, edges))
        except EOFError:  # Exit the loop when all test cases are processed
            break

if __name__ == "__main__":
    main()

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240521205847393](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405212058712.png)



### 27635: 判断无向图是否连通有无回路(同23163)

http://cs101.openjudge.cn/practice/27635/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def is_connected(graph, n):
    visited = [False] * n  
    stack = [0]
    visited[0] = True

    while stack:
        node = stack.pop()
        for neighbor in graph[node]:
            if not visited[neighbor]:
                stack.append(neighbor)
                visited[neighbor] = True

    return all(visited)

def has_cycle(graph, n):
    def dfs(node, visited, parent):
        visited[node] = True
        for neighbor in graph[node]:
            if not visited[neighbor]:
                if dfs(neighbor, visited, node):
                    return True
            elif parent != neighbor:
                return True
        return False

    visited = [False] * n
    for node in range(n):
        if not visited[node]:
            if dfs(node, visited, -1):
                return True
    return False

n, m = map(int, input().split())
graph = [[] for _ in range(n)]
for _ in range(m):
    u, v = map(int, input().split())
    graph[u].append(v)
    graph[v].append(u)

connected = is_connected(graph, n)
has_loop = has_cycle(graph, n)
print("connected:yes" if connected else "connected:no")
print("loop:yes" if has_loop else "loop:no")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240521210029428](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405212100505.png)





### 27947: 动态中位数

http://cs101.openjudge.cn/practice/27947/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
import heapq

def dynamic_median(nums):
    min_heap = []  
    max_heap = []  

    median = []
    for i, num in enumerate(nums):
        if not max_heap or num <= -max_heap[0]:
            heapq.heappush(max_heap, -num)
        else:
            heapq.heappush(min_heap, num)

        if len(max_heap) - len(min_heap) > 1:
            heapq.heappush(min_heap, -heapq.heappop(max_heap))
        elif len(min_heap) > len(max_heap):
            heapq.heappush(max_heap, -heapq.heappop(min_heap))

        if i % 2 == 0:
            median.append(-max_heap[0])

    return median

T = int(input())
for _ in range(T):
    nums = list(map(int, input().split()))
    median = dynamic_median(nums)
    print(len(median))
    print(*median)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240521210258655](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405212102839.png)



### 28190: 奶牛排队

http://cs101.openjudge.cn/practice/28190/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
N = int(input())
heights = [int(input()) for _ in range(N)]

left_bound = [-1] * N
right_bound = [N] * N

stack = []  

for i in range(N):
    while stack and heights[stack[-1]] < heights[i]:
        stack.pop()

    if stack:
        left_bound[i] = stack[-1]

    stack.append(i)

stack = []  

for i in range(N-1, -1, -1):
    while stack and heights[stack[-1]] > heights[i]:
        stack.pop()

    if stack:
        right_bound[i] = stack[-1]

    stack.append(i)

ans = 0

for i in range(N):  
    for j in range(left_bound[i] + 1, i):
        if right_bound[j] > i:
            ans = max(ans, i - j + 1)
            break
print(ans)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240521210414375](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405212104443.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

​	后几题参考了题解，借鉴了同学的思路，对前面所学的有了更好的理解。



