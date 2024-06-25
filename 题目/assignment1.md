# Assignment #1: 拉齐大家Python水平

Updated 0940 GMT+8 Feb 19, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院



**说明：**

1）数算课程的先修课是计概，由于计概学习中可能使用了不同的编程语言，而数算课程要求Python语言，因此第一周作业练习Python编程。如果有同学坚持使用C/C++，也可以，但是建议也要会Python语言。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知3月1日导入选课名单后启用。**作业写好后，保留在自己手中，待3月1日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)



## 1. 题目

### 20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
a=int(input())
b=[0,1,1]
if a>=3:
    for i in range(2,a):
        x=b[i-2]+b[i-1]+b[i]
        b.append(x)
    print(x)
if a==0:
    print(0)
if a==1 or a==2:
    print(1)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240302155128021](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403021551241.png)



### 58A. Chat room

greedy/strings, 1000, http://codeforces.com/problemset/problem/58/A



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
x=input()
a=b=c=d=e=-1
for i in range(len(x)):
    if x[i]=="h":
        a=i
        break
if a>=0:
    for i in range(a+1,len(x)):
        if x[i]=="e":
            b=i
            break
if b>=0:
    for i in range(b+1,len(x)):
        if x[i]=="l":
            c=i
            break
if c>=0:
    for i in range(c+1,len(x)):
        if x[i]=="l":
            d=i
            break
if d>=0:
    for i in range(d+1,len(x)):
        if x[i]=="o":
            e=i
            break
if e>0:
    print('YES')
else:
    print('NO')

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240302160236619](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403021602670.png)



### 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
x=input()
x=x.lower()
xx=''
for i in x:
    if i=='a' or i=='u' or i=='o' or i=='i' or i=='e' or i=='y':
        a=1
    else:
        xx+='.'+i
print(xx)


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240302161026506](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403021610627.png)



### 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
p=[2]
for i in range(3,10000):
    a=1
    for j in p:
        if (i%j)==0:
            a=0
    if a==1:
        p.append(i)
x=int(input())
for a in p:
    b=x-a
    if b in p:
        break
print(a,b)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240302161922775](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403021619819.png)



### 23563: 多项式时间复杂度

http://cs101.openjudge.cn/practice/23563/



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
x=input().split("+")
a=0
for i in x:
    if i[0]>"0" :
        ii=i.split("n^")
        if int(ii[-1])>a:
            a=int(ii[-1])
print("n^"+str(a))


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240302163002892](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403021630036.png)



### 24684: 直播计票

http://cs101.openjudge.cn/practice/24684/



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
from collections import Counter
def most_voted_option(votes):
    counter = Counter(votes)
    max_votes = max(counter.values())
    most_voted = [option for option, count in counter.items() if count == max_votes]
    return sorted(most_voted)


votes = list(map(int, input().split()))
result = most_voted_option(votes)
print(*result)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240302165201508](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403021652673.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“数算pre每日选做”、CF、LeetCode、洛谷等网站题目。==

​	题目比较简单，但也复习了python的基本语法。



