# Assignment #F: All-Killed 满分

Updated 1844 GMT+8 May 20, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)



## 1. 题目

### 22485: 升空的焰火，从侧面看

http://cs101.openjudge.cn/practice/22485/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
from collections import deque

def right_view(n, tree):
    queue = deque([(1, tree[1])])  # start with root node
    right_view = []

    while queue:
        level_size = len(queue)
        for i in range(level_size):
            node, children = queue.popleft()
            if children[0] != -1:
                queue.append((children[0], tree[children[0]]))
            if children[1] != -1:
                queue.append((children[1], tree[children[1]]))
        right_view.append(node)

    return right_view

n = int(input())
tree = {1: [-1, -1] for _ in range(n+1)}  # initialize tree with -1s
for i in range(1, n+1):
    left, right = map(int, input().split())
    tree[i] = [left, right]

result = right_view(n, tree)
print(' '.join(map(str, result)))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240528192527168](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405281925265.png)



### 28203:【模板】单调栈

http://cs101.openjudge.cn/practice/28203/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
n = int(input())
a = list(map(int, input().split()))
stack = []

#f = [0]*n
for i in range(n):
    while stack and a[stack[-1]] < a[i]:
        #f[stack.pop()] = i + 1
        a[stack.pop()] = i + 1


    stack.append(i)

while stack:
    a[stack[-1]] = 0
    stack.pop()

print(*a)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240528192729502](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405281927552.png)



### 09202: 舰队、海域出击！

http://cs101.openjudge.cn/practice/09202/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
from collections import defaultdict

def dfs(node, color):
    color[node] = 1
    for neighbour in graph[node]:
        if color[neighbour] == 1:
            return True
        if color[neighbour] == 0 and dfs(neighbour, color):
            return True
    color[node] = 2
    return False

T = int(input())
for _ in range(T):
    N, M = map(int, input().split())
    graph = defaultdict(list)
    for _ in range(M):
        x, y = map(int, input().split())
        graph[x].append(y)
    color = [0] * (N + 1)
    is_cyclic = False
    for node in range(1, N + 1):
        if color[node] == 0:
            if dfs(node, color):
                is_cyclic = True
                break
    print("Yes" if is_cyclic else "No")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240528192815493](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405281928706.png)



### 04135: 月度开销

http://cs101.openjudge.cn/practice/04135/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
n, m = map(int, input().split())
expenditure = [int(input()) for _ in range(n)]

left, right = max(expenditure), sum(expenditure)


def check(x):
    num, s = 1, 0
    for i in range(n):
        if s + expenditure[i] > x:
            s = expenditure[i]
            num += 1
        else:
            s += expenditure[i]

    return [False, True][num > m]


res = 0


def binary_search(lo, hi):
    if lo >= hi:
        global res
        res = lo
        return

    mid = (lo + hi) // 2
    # print(mid)
    if check(mid):
        lo = mid + 1
        binary_search(lo, hi)
    else:
        hi = mid
        binary_search(lo, hi)


binary_search(left, right)
print(res)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240528192922204](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405281929280.png)



### 07735: 道路

http://cs101.openjudge.cn/practice/07735/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
import heapq

def dijkstra(g):
    while pq:
        dist,node,fee = heapq.heappop(pq)
        if node == n-1 :
            return dist
        for nei,w,f in g[node]:
            n_dist = dist + w
            n_fee = fee + f
            if n_fee <= k:
                dists[nei] = n_dist
                heapq.heappush(pq,(n_dist,nei,n_fee))
    return -1

k,n,r = int(input()),int(input()),int(input())
g = [[] for _ in range(n)]
for i in range(r):
    s,d,l,t = map(int,input().split())
    g[s-1].append((d-1,l,t)) #node,dist,fee

pq = [(0,0,0)] #dist,node,fee
dists = [float('inf')] * n
dists[0] = 0
spend = 0

result = dijkstra(g)
print(result)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240528193008473](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405281930688.png)



### 01182: 食物链

http://cs101.openjudge.cn/practice/01182/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def find(x):  
    if p[x] == x:
        return x
    else:
        p[x] = find(p[x])  
        return p[x]

n, k = map(int, input().split())

p = [0] * (3 * n + 1)
for i in range(3 * n + 1):  
    p[i] = i

ans = 0
for _ in range(k):
    a, x, y = map(int, input().split())
    if x > n or y > n:
        ans += 1;
        continue

    if a == 1:
        if find(x + n) == find(y) or find(y + n) == find(x):
            ans += 1;
            continue

        p[find(x)] = find(y)
        p[find(x + n)] = find(y + n)
        p[find(x + 2 * n)] = find(y + 2 * n)
    else:
        if find(x) == find(y) or find(y + n) == find(x):
            ans += 1;
            continue
        p[find(x + n)] = find(y)
        p[find(y + 2 * n)] = find(x)
        p[find(x + 2 * n)] = find(y + n)

print(ans)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240528193140811](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202405281931078.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

​	前几题较简单，复习了之前的内容，后几题参考了题解。



