# 数算整理

2024 spring Compiled by 刘乐天 23生科

说明：

1. 大部分代码来源于老师和同学。
1. 为基础内容的整理，可能会有遗漏。

# I. 基础算法

## 一、排序

### (一)冒泡排序：

```python
def BubbleSort(arr):
    for i in range(1,len(arr)):
        for j in range(0,len(arr)-i):
            if arr[j]>arr[j+1]:
                arr[j],arr[j+1]=arr[j+1],arr[j]
    return arr

```

### **(**二)选择排序:

```python
def SelectionSort(arr):
    for i in range(len(arr)-1):
        minIndex=i
        for j in range(i+1,len(arr)):
            if arr[j]<arr[minIndex]:
                minIndex=j
        if i!=minIndex:
            arr[i],arr[minIndex]=arr[minIndex],arr[i]
    return arr

```

### **(**三)插入排序：

```python
def InsertionSort(arr):
    for i in range(len(arr)):
        preIndex=i-1
        current=arr[i]
        while preIndex>=0 and arr[preIndex]>current:
            arr[preIndex+1]=arr[preIndex]
            preIndex-=1
        arr[preIndex+1]=current
    return arr

```

### **(**四)希尔排序：

```python
def ShellSort(arr):
    gap=int(len(arr)/3)
    while gap>0:
        for i in range(gap,len(arr)):
            temp=arr[i]
            j=i-gap
            while j>=0 and arr[j]>temp:
                arr[j+gap]=arr[j]
                j-=gap
            arr[j+gap]=temp
        gap=int(gap/3)
return arr

```

### **(五)归并排序&求逆序数/交换次数：**

```python
def MergeSort(arr):
	n=len(arr)
	if n<=1:
	    return arr,0
	middle=n//2
	left,left_swap=MergeSort(arr[:middle])
	right,right_swap=MergeSort(arr[middle:])
	swaps=left_swap+right_swap
	result=[]
	i=j=0
	while i<len(left) and j<len(right): 
        if left[i]<right[j]:
            result.append(left[i])
            i+=1
        else:
            result.append(right[j])
            j+=1
            swaps+=(middle-i)
if i==len(left):
    result.extend(right[j:])
else:
    result.extend(left[i:])
return result,swaps 

```

### (六)快速排序:

```python
def QuickSort(arr,start,end):
    if start>=end:
       return
	middle,left,right=arr[start],start,end
	while left<right:
	    while arr[right]>=middle and left<right:
	        right-=1
	    arr[left]=arr[right] 
	    while arr[left]<middle and left<right:
	        left+=1
	    arr[right]=arr[left]
	arr[left]=middle
	QuickSort(arr,start,left-1)
	QuickSort(arr,left+1,end)
QuickSort(arr,0,len(arr)-1)

```

### **(**七)堆排序&堆的构建:

```python
def Big_Heap(arr,start,end): #构建大根堆
	root=start
	child=root*2+1
	while child<=end:
	    if child+1<=end and arr[child]<arr[child+1]:
	        child+=1
	    if arr[root]<arr[child]:
	        arr[root],arr[child]=arr[child],arr[root]
	        root=child
    	    child=root*2+1
		else:
        	break
def HeapSort(arr): #堆排序
	first=len(arr)//2-1
	for start in range(first,-1,-1):
	    Big_Heap(arr,start,len(arr)-1)
	for end in range(len(arr)-1,0,-1):
    	arr[0],arr[end]=arr[end],arr[0]
    	Big_Heap(arr,0,end-1)
	return arr

```

### **(**八)计数排序:

```python
def CountSort(arr):
	max_num=max(arr)
	count_arr=[0]*(max_num+1)
	for value in arr:
	    count_arr[value]+=1
	new_arr=[]
	for i in range(len(count_arr)):
	    while count_arr[i]!=0:
			new_arr.append(i)
			count_arr[i]-=1
	return new_arr 

```

### **(**九)桶排序:

```python
def BucketSort(arr,bucket_size):
	arr_min,arr_max=min(arr),max(arr)
	bucket_count=(arr_max-arr_min)//bucket_size+1
	buckets=[[] for _ in range(bucket_count)]
	for num in arr:
	    buckets[(num-arr_min)//bucket_size].append(num)
	new_arr=[]
	for bucket in buckets:
	    bucket.sort()
	    （也可换成其他排序算法）
	    new_arr.extend(bucket)
	return new_arr

```

### **(十)基数排序:**

```python
def RadixSort(arr):
	max_num=max(arr)
	place=1
	while max_num>=10**place:
	    place+=1
	for i in range(place):
	    buckets=[[] for _ in range(10)]
	    for num in arr:
	        radix=int(num/(10**i)%10)
	        buckets[radix].append(num)
		j=0
		for k in range(10):
        	for num in buckets[k]:
            	arr[j]=num
            	j+=1
	return arr

```

## 二、栈、队列

```python
#自己建立Stack对象
Stack() #创建空栈
push(item) #添加元素到顶端
pop() #移出顶端
peek() #返回顶端元素但不移除
isEmpty() #检查栈是否为空
size() #返回栈中元素数目
```

### 单调栈  

```python
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

#### 中序表达式转后序表达式

```python
pre={'+':1,'-':1,'*':2,'/':2}
for _ in range(int(input())):
    expr=input()
    ans=[]; ops=[]
    for char in expr:
        if char.isdigit() or char=='.':
            ans.append(char)
        elif char=='(':
            ops.append(char)
        elif char==')':
            while ops and ops[-1]!='(':
                ans.append(ops.pop())
            ops.pop()
        else:
            while ops and ops[-1]!='(' and pre[ops[-1]]>=pre[char]:
                ans.append(ops.pop())
            ops.append(char)
    while ops:
        ans.append(ops.pop())
    print(''.join(ans))
```

#### 逆波兰表达式求值

```python
stack=[]
for t in s:
    if t in '+-*/':
        b,a=stack.pop(),stack.pop()
        stack.append(str(eval(a+t+b)))
    else:
        stack.append(t)
print(f'{float(stack[0]):.6f}')
```

#### 最大全0子矩阵

```python
for row in ma:
    stack=[]
    for i in range(n):
        h[i]=h[i]+1 if row[i]==0 else 0
        while stack and h[stack[-1]]>h[i]:
            y=h[stack.pop()]
            w=i if not stack else i-stack[-1]-1
            ans=max(ans,y*w)
        stack.append(i)
    while stack:
        y=h[stack.pop()]
        w=n if not stack else n-stack[-1]-1
        ans=max(ans,y*w)
print(ans)
```

#### 求逆序对数

```python
from bisect import *
a=[]
rev=0
for _ in range(n):
    num=int(input())
    rev+=bisect_left(a,num)
    insort_left(a,num)
ans=n*(n-1)//2-rev
```

```python
def merge_sort(a):
    if len(a)<=1:
        return a,0
    mid=len(a)//2
    l,l_cnt=merge_sort(a[:mid])
    r,r_cnt=merge_sort(a[mid:])
    merged,merge_cnt=merge(l,r)
    return merged,l_cnt+r_cnt+merge_cnt
def merge(l,r):
    merged=[]
    l_idx,r_idx=0,0
    inverse_cnt=0
    while l_idx<len(l) and r_idx<len(r):
        if l[l_idx]<=r[r_idx]:
            merged.append(l[l_idx])
            l_idx+=1
        else:
            merged.append(r[r_idx])
            r_idx+=1
            inverse_cnt+=len(l)-l_idx
    merged.extend(l[l_idx:])
    merged.extend(r[r_idx:])
    return merged,inverse_cnt
```

## 三、树

#### 根据前中序得后序、根据中后序得前序

```python
def postorder(preorder,inorder):
    if not preorder:
        return ''
    root=preorder[0]
    idx=inorder.index(root)
    left=postorder(preorder[1:idx+1],inorder[:idx])
    right=postorder(preorder[idx+1:],inorder[idx+1:])
    return left+right+root
```

```python
def preorder(inorder,postorder):
    if not inorder:
        return ''
    root=postorder[-1]
    idx=inorder.index(root)
    left=preorder(inorder[:idx],postorder[:idx])
    right=preorder(inorder[idx+1:],postorder[idx:-1])
    return root+left+right
```

#### 层次遍历

```python
from collections import deque
def levelorder(root):
    if not root:
        return ""
    q=deque([root])  
    res=""
    while q:
        node=q.popleft()  
        res+=node.val  
        if node.left:
            q.append(node.left)
        if node.right:
            q.append(node.right)
    return res
```

#### 二叉搜索树的构建

```python
def insert(root,num):
    if not root:
        return Node(num)
    if num<root.val:
        root.left=insert(root.left,num)
    else:
        root.right=insert(root.right,num)
    return root
```

#### 解析括号嵌套表达式

```python
def parse(s):
    node=Node(s[0])
    if len(s)==1:
        return node
    s=s[2:-1]; t=0; last=-1
    for i in range(len(s)):
        if s[i]=='(': t+=1
        elif s[i]==')': t-=1
        elif s[i]==',' and t==0:
            node.children.append(parse(s[last+1:i]))
            last=i
    node.children.append(parse(s[last+1:]))
    return node
```

#### 并查集

```python
class UnionFind:
    def __init__(self,n):
        self.p=list(range(n))
        self.h=[0]*n
    def find(self,x):
        if self.p[x]!=x:
            self.p[x]=self.find(self.p[x])
        return self.p[x]
    def union(self,x,y):
        rootx=self.find(x)
        rooty=self.find(y)
        if rootx!=rooty:
            if self.h[rootx]<self.h[rooty]:
                self.p[rootx]=rooty
            elif self.h[rootx]>self.h[rooty]:
                self.p[rooty]=rootx
            else:
                self.p[rooty]=rootx
                self.h[rootx]+=1
```

#### 字典树的构建

```python
def insert(root,num):
    node=root
    for digit in num:
        if digit not in node.children:
            node.children[digit]=TrieNode()
        node=node.children[digit]
        node.cnt+=1
```

## 四、图

#### bfs

```python
from collections import deque
def bfs(graph, start_node):
    queue = deque([start_node])
    visited = set()
    visited.add(start_node)
    while queue:
        current_node = queue.popleft()
        for neighbor in graph[current_node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

#### 棋盘问题（回溯法）

```python
def dfs(row, k):
    if k == 0:
        return 1
    if row == n:
        return 0
    count = 0
    for col in range(n):
        if board[row][col] == '#' and not col_occupied[col]:
            col_occupied[col] = True
            count += dfs(row + 1, k - 1)
            col_occupied[col] = False
    count += dfs(row + 1, k)
    return count
col_occupied = [False] * n
print(dfs(0, k))
```

#### dijkstra

```python
# 1.使用vis集合
def dijkstra(start,end):
    heap=[(0,start,[start])]
    vis=set()
    while heap:
        (cost,u,path)=heappop(heap)
        if u in vis: continue
        vis.add(u)
        if u==end: return (cost,path)
        for v in graph[u]:
            if v not in vis:
                heappush(heap,(cost+graph[u][v],v,path+[v]))
# 2.使用dist数组
import heapq
def dijkstra(graph, start):
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    priority_queue = [(0, start)]
    while priority_queue:
        current_distance, current_node = heapq.heappop(priority_queue)
        if current_distance > distances[current_node]:
            continue
        for neighbor, weight in graph[current_node].items():
            distance = current_distance + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(priority_queue, (distance, neighbor))
    return distances
```

#### kruskal

```python
uf=UnionFind(n)
edges.sort()
ans=0
for w,u,v in edges:
    if uf.union(u,v):
        ans+=w
print(ans)
```

#### prim

```python
vis=[0]*n
q=[(0,0)]
ans=0
while q:
    w,u=heappop(q)
    if vis[u]:
        continue
    ans+=w
    vis[u]=1
    for v in range(n):
        if not vis[v] and graph[u][v]!=-1:
            heappush(q,(graph[u][v],v))
print(ans)
```

#### 拓扑排序

```python
from collections import deque
def topo_sort(graph):
    in_degree={u:0 for u in graph}
    for u in graph:
        for v in graph[u]:
            in_degree[v]+=1
    q=deque([u for u in in_degree if in_degree[u]==0])
    topo_order=[]
    while q:
        u=q.popleft()
        topo_order.append(u)
        for v in graph[u]:
            in_degree[v]-=1
            if in_degree[v]==0:
                q.append(v)
    if len(topo_order)!=len(graph):
        return []  
    return topo_order
```

## 五、其他

#### lrucache

```py
from functools import lru_cache
@lru_cache(maxsize=None)
```

#### bisect

```python
import bisect
# 创建一个有序列表
sorted_list = [1, 3, 4, 4, 5, 7]
# 使用bisect_left查找插入点
position = bisect.bisect_left(sorted_list, 4)
print(position)  # 输出: 2
# 使用bisect_right查找插入点
position = bisect.bisect_right(sorted_list, 4)
print(position)  # 输出: 4
# 使用insort_left插入元素
bisect.insort_left(sorted_list, 4)
print(sorted_list)  # 输出: [1, 3, 4, 4, 4, 5, 7]
# 使用insort_right插入元素
bisect.insort_right(sorted_list, 4)
print(sorted_list)  # 输出: [1, 3, 4, 4, 4, 4, 5, 7]
```

#### permutations：全排列

```python
from itertools import permutations
# 创建一个可迭代对象的排列
perm = permutations([1, 2, 3])
# 打印所有排列
for p in perm:
    print(p)
# 输出: (1, 2, 3)，(1, 3, 2)，(2, 1, 3)，(2, 3, 1)，(3, 1, 2)，(3, 2, 1)
```

#### combinations：组合

```python
from itertools import combinations
# 创建一个可迭代对象的组合
comb = combinations([1, 2, 3], 2)
# 打印所有组合
for c in comb:
    print(c)
# 输出: (1, 2)，(1, 3)，(2, 3)
```

#### reduce：累次运算

```python
from functools import reduce
# 使用reduce计算列表元素的乘积
product = reduce(lambda x, y: x * y, [1, 2, 3, 4])
print(product)  # 输出: 24
```

#### product：笛卡尔积

```python
from itertools import product
# 创建两个可迭代对象的笛卡尔积
prod = product([1, 2], ['a', 'b'])
# 打印所有笛卡尔积对
for p in prod:
    print(p)
# 输出: (1, 'a')，(1, 'b')，(2, 'a')，(2, 'b')
```

