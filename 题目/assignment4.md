# Assignment #4: 排序、栈、队列和树

Updated 0005 GMT+8 March 11, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院

**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:

Learn about Time complexities, learn the basics of individual Data Structures, learn the basics of Algorithms, and practice Problems.

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)

## 1. 题目

### 05902: 双端队列

http://cs101.openjudge.cn/practice/05902/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
t=int(input())
for i in range(t):
    n=int(input())
    l=[]
    for j in range(n):
        type,x=map(int,input().split())
        if type==1:
            l.append(x)
        else:
            if x==1:
                l=l[0:-1]
            else:
                l=l[1:]
    if len(l)==0:
        print("NULL")
    else:
        l1 = ' '.join(str(i) for i in l)
        print(l1)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240318200142144](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403182001357.png)



### 02694: 波兰表达式

http://cs101.openjudge.cn/practice/02694/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
a=input().split()
c=[1,1]
while len(a) > 1 and len(c)>1:
    c=[]
    for i in range(len(a)-1):
        if len(a[i])>1 and len(a[i+1])>1:
            b=eval(a[i]+a[i-1]+a[i+1])
            c[i-1]=(str(b))
            c+=a[i+2:]
            break
        else:
            c.append(a[i])
    if len(c)>1:
        a=[]
        for i in range(len(c) - 1):
            if len(c[i]) > 1 and len(c[i + 1]) > 1:
                b = eval(c[i] + c[i - 1] + c[i + 1])
                a[i - 1] = (str(b))
                a += c[i + 2:]
                break
            else:
                a.append(c[i])
        if len(a)==1:
            q=float(a[0])
    else:
        q=float(c[0])
print("{:.6f}".format(q))


```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240318200204115](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403182002260.png)



### 24591: 中序表达式转后序表达式

http://cs101.openjudge.cn/practice/24591/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
import re

def expProcessor(fpexp):
    temp = re.findall('[0-9.a-zA-Z]+|[**]+|[//]+|[+\-*/()]?|[not]?|[and]?|[or]?|[True]?|[False]?|.',\
    fpexp)
    fplist = [i for i in temp if i not in ["", " "]]

    i = 1
    while i < len(fplist):
        if (fplist[i] == "-") and (fplist[i - 1] in ["(", "+", "-", "*", "/", "**", "//", "not", "and", "or"]):
            fplist[i + 1] = "-" + fplist[i + 1]
            fplist.pop(i)
        else:
            i += 1

    return fplist

def priority(x):
    if x == '*' or x == '/':
        return 2
    if x == '+' or x == '-':
        return 1
    return 0

def is_numeric(string):
    try:
        int(string)
        return True
    except ValueError:
        try:
            float(string)
            return True
        except ValueError:
            return False

def infix_trans(infix):
    postfix = []
    op_stack = []
    for char in infix:
        if is_numeric(char):
            postfix.append(char)
        else:
            if char == '(':
                op_stack.append(char)
            elif char == ')':
                while op_stack and op_stack[-1] != '(':
                    postfix.append(op_stack.pop())
                op_stack.pop()
            else:
                while op_stack and priority(op_stack[-1]) >= priority(char) and op_stack[-1] != '(':
                    postfix.append(op_stack.pop())
                op_stack.append(char)
    while op_stack:
        postfix.append(op_stack.pop())
    return postfix

n = int(input())
for _ in range(n):
    s = input()
    fp = expProcessor(s)
    pp = infix_trans(fp)
    print(' '.join(pp))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240319180118925](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403191801044.png)



### 22068: 合法出栈序列

http://cs101.openjudge.cn/practice/22068/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def is_valid_pop_sequence(origin, output):
    if len(origin) != len(output):
        return False

    stack = []
    bank = list(origin)

    for char in output:
        while (not stack or stack[-1] != char) and bank:
            stack.append(bank.pop(0))

        if not stack or stack[-1] != char:
            return False

        stack.pop()

    return True

origin = input().strip()

while True:
    try:
        output = input().strip()
        if is_valid_pop_sequence(origin, output):
            print('YES')
        else:
            print('NO')
    except EOFError:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240319180442210](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403191804300.png)



### 06646: 二叉树的深度

http://cs101.openjudge.cn/practice/06646/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
ans, l, r = 1, [-1], [-1]
def dfs(n, count):
    global ans, l, r
    if l[n] != -1:
        dfs(l[n], count + 1)
    if r[n] != -1:
        dfs(r[n], count + 1)
    ans = max(ans, count)


n = int(input())
for i in range(n):
    a, b = map(int, input().split())
    l.append(a)
    r.append(b)
dfs(1, 1)
print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240319180651954](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403191806193.png)



### 02299: Ultra-QuickSort

http://cs101.openjudge.cn/practice/02299/



思路：



代码

```python
#刘乐天 2300012105 生命科学学院
def merge_sort(lst):
    if len(lst) <= 1:
        return lst, 0

    middle = len(lst) // 2
    left, inv_left = merge_sort(lst[:middle])
    right, inv_right = merge_sort(lst[middle:])

    merged, inv_merge = merge(left, right)

    return merged, inv_left + inv_right + inv_merge

def merge(left, right):
    merged = []
    inv_count = 0
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1
            inv_count += len(left) - i

    merged += left[i:]
    merged += right[j:]

    return merged, inv_count

while True:
    n = int(input())
    if n == 0:
        break

    lst = []
    for _ in range(n):
        lst.append(int(input()))

    _, inversions = merge_sort(lst)
    print(inversions)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240319180942112](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403191809331.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

​	这次作业比较困难，后面几道题看了题解，学习了findall（）等函数，加深了对队列和栈的理解。



