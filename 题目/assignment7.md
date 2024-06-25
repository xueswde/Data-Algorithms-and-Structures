# Assignment #7: April 月考

Updated 1557 GMT+8 Apr 3, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)



## 1. 题目

### 27706: 逐词倒放

http://cs101.openjudge.cn/practice/27706/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
sentence = input().split()
reversed_sentence = ' '.join(sentence[::-1])
print(reversed_sentence)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240409172348672](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404091723891.png)



### 27951: 机器翻译

http://cs101.openjudge.cn/practice/27951/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
from collections import deque

M, N = map(int, input().split())
words = list(map(int, input().split()))

memory = deque()
lookups = 0

for word in words:
    if word not in memory:
        if len(memory) == M:
            memory.popleft()
        memory.append(word)
        lookups += 1

print(lookups)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240409172439817](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404091724978.png)



### 27932: Less or Equal

http://cs101.openjudge.cn/practice/27932/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
n, k = map(int, input().split())

a = list(map(int, input().split()))
a.sort()

if k == 0:
    x = 1 if a[0] > 1 else -1
elif k == n:
    x = a[-1]
else:
    x = a[k-1] if a[k-1] < a[k] else -1

print(x)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240409172546078](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404091725228.png)



### 27948: FBI树

http://cs101.openjudge.cn/practice/27948/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def construct_FBI_tree(s):
    if '0' in s and '1' in s:
        node_type = 'F'
    elif '1' in s:
        node_type = 'I'
    else:
        node_type = 'B'

    if len(s) > 1:  
        mid = len(s) // 2
        left_tree = construct_FBI_tree(s[:mid])
        right_tree = construct_FBI_tree(s[mid:])
        return left_tree + right_tree + node_type
    else:
        return node_type


N = int(input())
s = input()
print(construct_FBI_tree(s))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240409172719197](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404091727390.png)



### 27925: 小组队列

http://cs101.openjudge.cn/practice/27925/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
from collections import deque					

t = int(input())
groups = {}
member_to_group = {}



for _ in range(t):
    members = list(map(int, input().split()))
    group_id = members[0] 
    groups[group_id] = deque()
    for member in members:
        member_to_group[member] = group_id

queue = deque()
queue_set = set()


while True:
    command = input().split()
    if command[0] == 'STOP':
        break
    elif command[0] == 'ENQUEUE':
        x = int(command[1])
        group = member_to_group.get(x, None)
        if group is None:
            group = x
            groups[group] = deque([x])
            member_to_group[x] = group
        else:
            groups[group].append(x)
        if group not in queue_set:
            queue.append(group)
            queue_set.add(group)
    elif command[0] == 'DEQUEUE':
        if queue:
            group = queue[0]
            x = groups[group].popleft()
            print(x)
            if not groups[group]:  
                queue.popleft()
                queue_set.remove(group)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240409172838092](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404091728339.png)



### 27928: 遍历树

http://cs101.openjudge.cn/practice/27928/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.children = []


def traverse_print(root, nodes):
    if root.children == []:
        print(root.value)
        return
    pac = {root.value: root}
    for child in root.children:
        pac[child] = nodes[child]
    for value in sorted(pac.keys()):
        if value in root.children:
            traverse_print(pac[value], nodes)
        else:
            print(root.value)


n = int(input())
nodes = {}
children_list = []
for i in range(n):
    info = list(map(int, input().split()))
    nodes[info[0]] = TreeNode(info[0])
    for child_value in info[1:]:
        nodes[info[0]].children.append(child_value)
        children_list.append(child_value)
root = nodes[[value for value in nodes.keys() if value not in children_list][0]]
traverse_print(root, nodes)


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240409172948263](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404091729511.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

​	这次作业较之前相对简单，也熟悉了之前掌握的语法。



