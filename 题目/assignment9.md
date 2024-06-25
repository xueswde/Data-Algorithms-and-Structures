# Assignment #9: 图论：遍历，及 树算

Updated 1739 GMT+8 Apr 14, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)



## 1. 题目

### 04081: 树的转换

http://cs101.openjudge.cn/dsapre/04081/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def tree_heights(s):
    old_height = 0
    max_old = 0
    new_height = 0
    max_new = 0
    stack = []
    for c in s:
        if c == 'd':
            old_height += 1
            max_old = max(max_old, old_height)

            new_height += 1
            stack.append(new_height)
            max_new = max(max_new, new_height)
        else:
            old_height -= 1

            new_height = stack[-1]
            stack.pop()
    return f"{max_old} => {max_new}"

s = input().strip()
print(tree_heights(s))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240423210637992](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404232106261.png)



### 08581: 扩展二叉树

http://cs101.openjudge.cn/dsapre/08581/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def build_tree(preorder):
    if not preorder or preorder[0] == '.':
        return None, preorder[1:]
    root = preorder[0]
    left, preorder = build_tree(preorder[1:])
    right, preorder = build_tree(preorder)
    return (root, left, right), preorder

def inorder(tree):
    if tree is None:
        return ''
    root, left, right = tree
    return inorder(left) + root + inorder(right)

def postorder(tree):
    if tree is None:
        return ''
    root, left, right = tree
    return postorder(left) + postorder(right) + root

preorder = input().strip()

tree, _ = build_tree(preorder)

print(inorder(tree))
print(postorder(tree))
```



代码运行截图 ==（至少包含有"Accepted"）==

![ ](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404232107076.png)



### 22067: 快速堆猪

http://cs101.openjudge.cn/practice/22067/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
a = []
m = []

while True:
    try:
        s = input().split()

        if s[0] == "pop":
            if a:
                a.pop()
                if m:
                    m.pop()
        elif s[0] == "min":
            if m:
                print(m[-1])
        else:
            h = int(s[1])
            a.append(h)
            if not m:
                m.append(h)
            else:
                k = m[-1]
                m.append(min(k, h))
    except EOFError:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240423210832945](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404232108149.png)



### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
maxn = 10;
sx = [-2, -1, 1, 2, 2, 1, -1, -2]
sy = [1, 2, 2, 1, -1, -2, -2, -1]

ans = 0;


def Dfs(dep: int, x: int, y: int):
    if n * m == dep:
        global ans
        ans += 1
        return

    for r in range(8):
        s = x + sx[r]
        t = y + sy[r]
        if chess[s][t] == False and 0 <= s < n and 0 <= t < m:
            chess[s][t] = True
            Dfs(dep + 1, s, t)
            chess[s][t] = False;

for _ in range(int(input())):
    n, m, x, y = map(int, input().split())
    chess = [[False] * maxn for _ in range(maxn)]  
    ans = 0
    chess[x][y] = True
    Dfs(1, x, y)
    print(ans)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240423210953973](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404232109195.png)



### 28046: 词梯

bfs, http://cs101.openjudge.cn/practice/28046/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
from collections import defaultdict
dic=defaultdict(list)
n,lis=int(input()),[]
for i in range(n):
    lis.append(input())
for word in lis:
    for i in range(len(word)):
        bucket=word[:i]+'_'+word[i+1:]
        dic[bucket].append(word)
def bfs(start,end,dic):
    queue=[(start,[start])]
    visited=[start]
    while queue:
        currentword,currentpath=queue.pop(0)
        if currentword==end:
            return ' '.join(currentpath)
        for i in range(len(currentword)):
            bucket=currentword[:i]+'_'+currentword[i+1:]
            for nbr in dic[bucket]:
                if nbr not in visited:
                    visited.append(nbr)
                    newpath=currentpath+[nbr]
                    queue.append((nbr,newpath))
    return 'NO'
start,end=map(str,input().split())    
print(bfs(start,end,dic))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240423211237077](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404232112137.png)



### 28050: 骑士周游

dfs, http://cs101.openjudge.cn/practice/28050/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
import sys

class Graph:
    def __init__(self):
        self.vertices = {}
        self.num_vertices = 0

    def add_vertex(self, key):
        self.num_vertices = self.num_vertices + 1
        new_ertex = Vertex(key)
        self.vertices[key] = new_ertex
        return new_ertex

    def get_vertex(self, n):
        if n in self.vertices:
            return self.vertices[n]
        else:
            return None

    def __len__(self):
        return self.num_vertices

    def __contains__(self, n):
        return n in self.vertices

    def add_edge(self, f, t, cost=0):
        if f not in self.vertices:
            nv = self.add_vertex(f)
        if t not in self.vertices:
            nv = self.add_vertex(t)
        self.vertices[f].add_neighbor(self.vertices[t], cost)
        #self.vertices[t].add_neighbor(self.vertices[f], cost)

    def getVertices(self):
        return list(self.vertices.keys())

    def __iter__(self):
        return iter(self.vertices.values())


class Vertex:
    def __init__(self, num):
        self.key = num
        self.connectedTo = {}
        self.color = 'white'
        self.distance = sys.maxsize
        self.previous = None
        self.disc = 0
        self.fin = 0

    def __lt__(self,o):
        return self.key < o.key

    def add_neighbor(self, nbr, weight=0):
        self.connectedTo[nbr] = weight


    # def setDiscovery(self, dtime):
    #     self.disc = dtime
    #
    # def setFinish(self, ftime):
    #     self.fin = ftime
    #
    # def getFinish(self):
    #     return self.fin
    #
    # def getDiscovery(self):
    #     return self.disc

    def get_neighbors(self):
        return self.connectedTo.keys()

    # def getWeight(self, nbr):
    #     return self.connectedTo[nbr]

    def __str__(self):
        return str(self.key) + ":color " + self.color + ":disc " + str(self.disc) + ":fin " + str(
            self.fin) + ":dist " + str(self.distance) + ":pred \n\t[" + str(self.previous) + "]\n"



def knight_graph(board_size):
    kt_graph = Graph()
    for row in range(board_size):           #遍历每一行
        for col in range(board_size):       #遍历行上的每一个格子
            node_id = pos_to_node_id(row, col, board_size) #把行、列号转为格子ID
            new_positions = gen_legal_moves(row, col, board_size) #按照 马走日，返回下一步可能位置
            for row2, col2 in new_positions:
                other_node_id = pos_to_node_id(row2, col2, board_size) #下一步的格子ID
                kt_graph.add_edge(node_id, other_node_id) #在骑士周游图中为两个格子加一条边
    return kt_graph

def pos_to_node_id(x, y, bdSize):
    return x * bdSize + y

def gen_legal_moves(row, col, board_size):
    new_moves = []
    move_offsets = [                        # 马走日的8种走法
        (-1, -2),  # left-down-down
        (-1, 2),  # left-up-up
        (-2, -1),  # left-left-down
        (-2, 1),  # left-left-up
        (1, -2),  # right-down-down
        (1, 2),  # right-up-up
        (2, -1),  # right-right-down
        (2, 1),  # right-right-up
    ]
    for r_off, c_off in move_offsets:
        if (                                # #检查，不能走出棋盘
            0 <= row + r_off < board_size
            and 0 <= col + c_off < board_size
        ):
            new_moves.append((row + r_off, col + c_off))
    return new_moves

# def legal_coord(row, col, board_size):
#     return 0 <= row < board_size and 0 <= col < board_size


def knight_tour(n, path, u, limit):
    u.color = "gray"
    path.append(u)              #当前顶点涂色并加入路径
    if n < limit:
        neighbors = ordered_by_avail(u) #对所有的合法移动依次深入
        #neighbors = sorted(list(u.get_neighbors()))
        i = 0

        for nbr in neighbors:
            if nbr.color == "white" and \
                knight_tour(n + 1, path, nbr, limit):   #选择“白色”未经深入的点，层次加一，递归深入
                return True
        else:                       #所有的“下一步”都试了走不通
            path.pop()              #回溯，从路径中删除当前顶点
            u.color = "white"       #当前顶点改回白色
            return False
    else:
        return True

def ordered_by_avail(n):
    res_list = []
    for v in n.get_neighbors():
        if v.color == "white":
            c = 0
            for w in v.get_neighbors():
                if w.color == "white":
                    c += 1
            res_list.append((c,v))
    res_list.sort(key = lambda x: x[0])
    return [y[1] for y in res_list]


def main():
    def NodeToPos(id):
       return ((id//8, id%8))

    bdSize = int(input())  # 棋盘大小
    *start_pos, = map(int, input().split())  # 起始位置
    g = knight_graph(bdSize)
    start_vertex = g.get_vertex(pos_to_node_id(start_pos[0], start_pos[1], bdSize))
    if start_vertex is None:
        print("fail")
        exit(0)

    tour_path = []
    done = knight_tour(0, tour_path, start_vertex, bdSize * bdSize-1)
    if done:
        print("success")
    else:
        print("fail")

    exit(0)

    # 打印路径
    cnt = 0
    for vertex in tour_path:
        cnt += 1
        if cnt % bdSize == 0:
            print()
        else:
            print(vertex.key, end=" ")
            #print(NodeToPos(vertex.key), end=" ")   # 打印坐标

if __name__ == '__main__':
    main()

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240423211427186](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404232114446.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

​	大部分参考了题解，借鉴了同学的思路，联习了dfs



