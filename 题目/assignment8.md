# Assignment #8: 图论：概念、遍历，及 树算

Updated 1919 GMT+8 Apr 8, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)



## 1. 题目

### 19943: 图的拉普拉斯矩阵

matrices, http://cs101.openjudge.cn/practice/19943/

请定义Vertex类，Graph类，然后实现



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
n, m = map(int, input().split())
ans = [[0 for i in range(n)] for j in range(n)]
for i in range(m):       
    knot1, knot2 = map(int, input().split())       
    ans[knot1][knot1] += 1       
    ans[knot2][knot2] += 1       
    ans[knot1][knot2] -= 1       
    ans[knot2][knot1] -= 1
for j in range(n):       
    print(' '.join(map(str, ans[j])))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240416184957540](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404161850727.png)



### 18160: 最大连通域面积

matrix/dfs similar, http://cs101.openjudge.cn/practice/18160



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
dire = [[-1,-1],[-1,0],[-1,1],[0,-1],[0,1],[1,-1],[1,0],[1,1]]
area = 0
def dfs(x,y):
    global area
    if matrix[x][y] == '.':return
    matrix[x][y] = '.'
    area += 1
    for i in range(len(dire)):
        dfs(x+dire[i][0], y+dire[i][1])
for _ in range(int(input())):
    n,m = map(int,input().split())
    matrix = [['.' for _ in range(m+2)] for _ in range(n+2)]
    for i in range(1,n+1):
        matrix[i][1:-1] = input()
    sur = 0
    for i in range(1, n+1):
        for j in range(1, m+1):
            if matrix[i][j] == 'W':
                area = 0
                dfs(i, j)
                sur = max(sur, area)
    print(sur)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240416185040307](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404161850496.png)



### sy383: 最大权值连通块

https://sunnywhy.com/sfbj/10/3/383



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def max_weight(n, m, weights, edges):
    graph = [[] for _ in range(n)]
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)

    visited = [False] * n
    max_weight = 0

    def dfs(node):
        visited[node] = True
        total_weight = weights[node]
        for neighbor in graph[node]:
            if not visited[neighbor]:
                total_weight += dfs(neighbor)
        return total_weight

    for i in range(n):
        if not visited[i]:
            max_weight = max(max_weight, dfs(i))

    return max_weight

n, m = map(int, input().split())
weights = list(map(int, input().split()))
edges = []
for _ in range(m):
    u, v = map(int, input().split())
    edges.append((u, v))

print(max_weight(n, m, weights, edges))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240416185159127](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404161851282.png)



### 03441: 4 Values whose Sum is 0

data structure/binary search, http://cs101.openjudge.cn/practice/03441



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
n = int(input())
a = [0]*(n+1)
b = [0]*(n+1)
c = [0]*(n+1)
d = [0]*(n+1)

for i in range(n):
    a[i],b[i],c[i],d[i] = map(int, input().split())

dict1 = {}
for i in range(n):
    for j in range(n):
        if not a[i]+b[j] in dict1:
            dict1[a[i] + b[j]] = 0
        dict1[a[i] + b[j]] += 1

ans = 0
for i in range(n):
    for j in range(n):
        if -(c[i]+d[j]) in dict1:
            ans += dict1[-(c[i]+d[j])]

print(ans)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240416185316321](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404161853531.png)



### 04089: 电话号码

trie, http://cs101.openjudge.cn/practice/04089/

Trie 数据结构可能需要自学下。



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
class TrieNode:
    def __init__(self):
        self.child={}


class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, nums):
        curnode = self.root
        for x in nums:
            if x not in curnode.child:
                curnode.child[x] = TrieNode()
            curnode=curnode.child[x]

    def search(self, num):
        curnode = self.root
        for x in num:
            if x not in curnode.child:
                return 0
            curnode = curnode.child[x]
        return 1


t = int(input())
p = []
for _ in range(t):
    n = int(input())
    nums = []
    for _ in range(n):
        nums.append(str(input()))
    nums.sort(reverse=True)
    s = 0
    trie = Trie()
    for num in nums:
        s += trie.search(num)
        trie.insert(num)
    if s > 0:
        print('NO')
    else:
        print('YES')# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240416185540510](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404161855777.png)



### 04082: 树的镜面映射

http://cs101.openjudge.cn/practice/04082/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
from collections import deque

class TreeNode:
    def __init__(self, x):
        self.x = x
        self.children = []

def create_node():
    return TreeNode('')

def build_tree(tempList, index):
    node = create_node()
    node.x = tempList[index][0]
    if tempList[index][1] == '0':
        index += 1
        child, index = build_tree(tempList, index)
        node.children.append(child)
        index += 1
        child, index = build_tree(tempList, index)
        node.children.append(child)
    return node, index

def print_tree(p):
    Q = deque()
    s = deque()

    while p is not None:
        if p.x != '$':
            s.append(p)
        p = p.children[1] if len(p.children) > 1 else None

    while s:
        Q.append(s.pop())

    while Q:
        p = Q.popleft()
        print(p.x, end=' ')

        if p.children:
            p = p.children[0]
            while p is not None:
                if p.x != '$':
                    s.append(p)
                p = p.children[1] if len(p.children) > 1 else None

            while s:
                Q.append(s.pop())


n = int(input())
tempList = input().split()

root, _ = build_tree(tempList, 0)

print_tree(root)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240416185653926](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404161856204.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

​	学习了字典树（Trie）的用法。



