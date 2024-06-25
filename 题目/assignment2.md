# Assignment #2: 编程练习

Updated 0953 GMT+8 Feb 24, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:
- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知3月1日导入选课名单后启用。**作业写好后，保留在自己手中，待3月1日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)

### 27653: Fraction类

http://cs101.openjudge.cn/2024sp_routine/27653/



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
a,b,c,d=map(int,input().split())
y=b*d
x=a*d+b*c
xx,yy=x,y
while y>0:
    x,y=y,x%y
xx=int(xx/x)
yy=int(yy/x)
print(str(xx)+'/'+str(yy))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240302175527162](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403021755400.png)



### 04110: 圣诞老人的礼物-Santa Clau’s Gifts

greedy/dp, http://cs101.openjudge.cn/practice/04110



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
n, w = map(int, input().split())
a = []

for i in range(n):
    b, c = map(int, input().split())
    a.append((b, c))  
a.sort(key=lambda x: x[0] / x[1], reverse=True)

ww = 0
v = 0

for k, j in a:
    if ww + j >= w:
        v += (w - ww) * (k / j)
        break
    else:
        v += k
        ww += j

print(f"{v:.1f}")

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240308183451807](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403081834133.png)



### 18182: 打怪兽

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
nc=int(input())
for _ in range(nc):
    n,m,b=map(int,input().split())
    tx={}
    for _ in range(n):
        t,x=map(int,input().split())
        if t in tx:
            tx[t].append(x)
        else:
            tx[t]=[x]
    tx0=sorted(tx)
    for i in tx0:
        if m>=len(tx[i]):
            b-=sum(tx[i])
        else:
            b-=sum(sorted(tx[i])[-m:])
        if b<=0:
            print(i)
            break
    if b>0:
        print("alive")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240308183607987](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403081836139.png)



### 230B. T-primes

binary search/implementation/math/number theory, 1300, http://codeforces.com/problemset/problem/230/B



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
import math
 
MAXN = 10**6
isprime = [0, 0] + [1]*MAXN
for i in range(2, int(math.sqrt(MAXN))+1):
    if isprime[i]:
        for j in range(i*i, MAXN+1, i):
            isprime[j] = 0
 
n = int(input().strip())
a = list(map(int, input().strip().split()))
 
for i in a:
    t = math.sqrt(i)
    if t == int(t) and isprime[int(t)]:
        print('YES')
    else:
        print('NO')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240308185445503](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403081854553.png)



### 1364A. XXXXX

brute force/data structures/number theory/two pointers, 1200, https://codeforces.com/problemset/problem/1364/A



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
for t in range(int(input())):
    n, m = map(int, input().split())
    s, k = 0, -1
    for i, x in enumerate(map(int, input().split())):
        s = s+x
        if x % m:
            k = max(k, max(n-1-i, i))
    print([n, k][s % m == 0])

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240308191249583](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403081912767.png)



### 18176: 2050年成绩计算

http://cs101.openjudge.cn/practice/18176/



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
from math import sqrt
N = 10005
s = [True] * N
p = 2
while p * p <= N:
    if s[p]:
        for i in range (p * 2, N, p):
            s[i] = False
    p += 1
m, n = [int(i) for i in input ().split ()]
for i in range (m):
    x= [int(i) for i in input().split()]
    sum = 0
    for num in x:
        root = int (sqrt (num))
        if num > 3 and s[root] and num == root * root:
            sum += num
    sum /= len (x)
    if sum ==0:
        print (0)
    else:
        print ('%.2f' % sum)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240308191617647](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403081916883.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==



​	除了第一题之前都做过了，但是发现自己以前的代码也不是一下就能看懂，复习了以前掌握的语法。

