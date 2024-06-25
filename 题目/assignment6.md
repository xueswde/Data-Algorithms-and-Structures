# Assignment #6: "树"算：Huffman,BinHeap,BST,AVL,DisjointSet

Updated 2214 GMT+8 March 24, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院



**说明：**

1）这次作业内容不简单，耗时长的话直接参考题解。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)

## 1. 题目

### 22275: 二叉搜索树的遍历

http://cs101.openjudge.cn/practice/22275/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
class Node():
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None


def buildTree(preorder):
    if len(preorder) == 0:
        return None

    node = Node(preorder[0])

    idx = len(preorder)
    for i in range(1, len(preorder)):
        if preorder[i] > preorder[0]:
            idx = i
            break
    node.left = buildTree(preorder[1:idx])
    node.right = buildTree(preorder[idx:])

    return node


def postorder(node):
    if node is None:
        return []
    output = []
    output.extend(postorder(node.left))
    output.extend(postorder(node.right))
    output.append(str(node.val))

    return output


n = int(input())
preorder = list(map(int, input().split()))
print(' '.join(postorder(buildTree(preorder))))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240402192740667](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404021927067.png)



### 05455: 二叉搜索树的层次遍历

http://cs101.openjudge.cn/practice/05455/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
from collections import deque

class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

def insert_node(root, key):
    if not root:
        return Node(key)
    if key < root.val:
        root.left = insert_node(root.left, key)
    else:
        root.right = insert_node(root.right, key)
    return root

def build_tree(sq):
    root = Node(sq[0])
    for i in range(1, len(sq)):
        insert_node(root, sq[i])
    return root

def level(root):
    q = deque()
    q.append(root)
    ret = []
    while q:
        node = q.popleft()
        ret.append(str(node.val))
        if node.left:
            q.append(node.left)
        if node.right:
            q.append(node.right)

    return ret

sq = list({int(x): 1 for x in input().split()}.keys())
root = build_tree(sq)
print(' '.join(level(root)))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240402194735916](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404021947981.png)



### 04078: 实现堆结构

http://cs101.openjudge.cn/practice/04078/

练习自己写个BinHeap。当然机考时候，如果遇到这样题目，直接import heapq。手搓栈、队列、堆、AVL等，考试前需要搓个遍。



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
class BinHeap:
    def __init__(self):
        self.heapList = [0]
        self.currentSize = 0

    def percUp(self, i):
        while i // 2 > 0:
            if self.heapList[i] < self.heapList[i // 2]:
                tmp = self.heapList[i // 2]
                self.heapList[i // 2] = self.heapList[i]
                self.heapList[i] = tmp
            i = i // 2

    def insert(self, k):
        self.heapList.append(k)
        self.currentSize = self.currentSize + 1
        self.percUp(self.currentSize)

    def percDown(self, i):
        while (i * 2) <= self.currentSize:
            mc = self.minChild(i)
            if self.heapList[i] > self.heapList[mc]:
                tmp = self.heapList[i]
                self.heapList[i] = self.heapList[mc]
                self.heapList[mc] = tmp
            i = mc

    def minChild(self, i):
        if i * 2 + 1 > self.currentSize:
            return i * 2
        else:
            if self.heapList[i * 2] < self.heapList[i * 2 + 1]:
                return i * 2
            else:
                return i * 2 + 1

    def delMin(self):
        retval = self.heapList[1]
        self.heapList[1] = self.heapList[self.currentSize]
        self.currentSize = self.currentSize - 1
        self.heapList.pop()
        self.percDown(1)
        return retval

    def buildHeap(self, alist):
        i = len(alist) // 2
        self.currentSize = len(alist)
        self.heapList = [0] + alist[:]
        while (i > 0):
            #print(f'i = {i}, {self.heapList}')
            self.percDown(i)
            i = i - 1
        #print(f'i = {i}, {self.heapList}')


n = int(input().strip())
bh = BinHeap()
for _ in range(n):
    inp = input().strip()
    if inp[0] == '1':
        bh.insert(int(inp.split()[1]))
    else:
        print(bh.delMin())

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240402193017347](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404021930413.png)



### 22161: 哈夫曼编码树

http://cs101.openjudge.cn/practice/22161/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
import heapq

class Node:
    def __init__(self, weight, char=None):
        self.weight = weight
        self.char = char
        self.left = None
        self.right = None

    def __lt__(self, other):
        if self.weight == other.weight:
            return self.char < other.char
        return self.weight < other.weight

def build_huffman_tree(characters):
    heap = []
    for char, weight in characters.items():
        heapq.heappush(heap, Node(weight, char))

    while len(heap) > 1:
        left = heapq.heappop(heap)
        right = heapq.heappop(heap)
        merged = Node(left.weight + right.weight)
        merged.left = left
        merged.right = right
        heapq.heappush(heap, merged)

    return heap[0]

def encode_huffman_tree(root):
    codes = {}

    def traverse(node, code):
        if node.char:
            codes[node.char] = code
        else:
            traverse(node.left, code + '0')
            traverse(node.right, code + '1')

    traverse(root, '')
    return codes

def huffman_encoding(codes, string):
    encoded = ''
    for char in string:
        encoded += codes[char]
    return encoded

def huffman_decoding(root, encoded_string):
    decoded = ''
    node = root
    for bit in encoded_string:
        if bit == '0':
            node = node.left
        else:
            node = node.right

        if node.char:
            decoded += node.char
            node = root
    return decoded

n = int(input())
characters = {}
for _ in range(n):
    char, weight = input().split()
    characters[char] = int(weight)

#string = input().strip()
#encoded_string = input().strip()

huffman_tree = build_huffman_tree(characters)

codes = encode_huffman_tree(huffman_tree)

strings = []
while True:
    try:
        line = input()
        if line:
            strings.append(line)
        else:
            break
    except EOFError:
        break

results = []
#print(strings)
for string in strings:
    if string[0] in ('0','1'):
        results.append(huffman_decoding(huffman_tree, string))
    else:
        results.append(huffman_encoding(codes, string))

for result in results:
    print(result)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240402193203999](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404021932273.png)



### 晴问9.5: 平衡二叉树的建立

https://sunnywhy.com/sfbj/9/5/359



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
        self.height = 1


class AVL:
    def __init__(self):
        self.root = None

    def insert(self, value):
        if not self.root:
            self.root = Node(value)
        else:
            self.root = self._insert(value, self.root)

    def _insert(self, value, node):
        if not node:
            return Node(value)
        elif value < node.value:
            node.left = self._insert(value, node.left)
        else:
            node.right = self._insert(value, node.right)
        node.height = 1 + max(self._get_height(node.left), self._get_height(node.right))
        balance = self._get_balance(node)
        if balance > 1:
            if value < node.left.value:
                return self._rotate_right(node)
            else:
                node.left = self._rotate_left(node.left)
                return self._rotate_right(node)
        if balance < -1:
            if value > node.right.value:
                return self._rotate_left(node)
            else:
                node.right = self._rotate_right(node.right)
                return self._rotate_left(node)
        return node

    def _get_height(self, node):
        if not node:
            return 0
        return node.height

    def _get_balance(self, node):
        if not node:
            return 0
        return self._get_height(node.left) - self._get_height(node.right)

    def _rotate_left(self, node):
        new_root = node.right
        node.right = new_root.left
        new_root.left = node
        node.height = 1 + max(self._get_height(node.left), self._get_height(node.right))
        new_root.height = 1 + max(self._get_height(new_root.left), self._get_height(new_root.right))

        return new_root

    def _rotate_right(self, node):

        new_root = node.left
        node.left = new_root.right
        new_root.right = node

        node.height = 1 + max(self._get_height(node.left), self._get_height(node.right))
        new_root.height = 1 + max(self._get_height(new_root.left), self._get_height(new_root.right))

        return new_root

    def pre(self):
        return self._pre(self.root)

    def _pre(self, node):
        if not node:
            return []
        sq = [node.value]
        sq.extend(self._pre(node.left))
        sq.extend(self._pre(node.right))

        return sq


n = int(input())
sq = [int(x) for x in input().split()]
avl = AVL()
for x in sq:
    avl.insert(x)
print(*avl.pre())
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240402195110382](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404021951565.png)



### 02524: 宗教信仰

http://cs101.openjudge.cn/practice/02524/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def init_set(n):
    return list(range(n))

def get_father(x, father):
    if father[x] != x:
        father[x] = get_father(father[x], father)
    return father[x]

def join(x, y, father):
    fx = get_father(x, father)
    fy = get_father(y, father)
    if fx == fy:
        return
    father[fx] = fy

def is_same(x, y, father):
    return get_father(x, father) == get_father(y, father)

def main():
    case_num = 0
    while True:
        n, m = map(int, input().split())
        if n == 0 and m == 0:
            break
        count = 0
        father = init_set(n)
        for _ in range(m):
            s1, s2 = map(int, input().split())
            join(s1 - 1, s2 - 1, father)
        for i in range(n):
            if father[i] == i:
                count += 1
        case_num += 1
        print(f"Case {case_num}: {count}")

if __name__ == "__main__":
    main()
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240402193410129](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202404021934359.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

​	学习了关于二叉树的知识。



