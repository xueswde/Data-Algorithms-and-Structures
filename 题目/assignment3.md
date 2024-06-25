# Assignment #3: March月考

Updated 1537 GMT+8 March 6, 2024

2024 spring, Complied by 2300012105 刘乐天，生命科学学院

**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:
- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11 家庭中文版22621.2283

Python编程环境： PyCharm 2023.1.4 (Professional Edition)

## 1. 题目

**02945: 拦截导弹**

http://cs101.openjudge.cn/practice/02945/



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
k=int(input())
x=list(map(int,input().split()))
kk=[0]*(k-1)+[1]
for i in range(k-2,-1,-1):
    m=[0]*(k-i)
    for j in range(i,k):
        if x[i]>=x[j]:
            m[j-i]=kk[j]+1
    kk[i]=max(m)
print(max(kk))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240308193735316](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403081937546.png)



**04147:汉诺塔问题(Tower of Hanoi)**

http://cs101.openjudge.cn/practice/04147



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
def moveOne(numDisk: int, init: str, desti: str):
    print("{}:{}->{}".format(numDisk, init, desti))
def move(numDisks: int, init: str, temp: str, desti: str):
    if numDisks == 1:
        moveOne(1, init, desti)
    else:
        move(numDisks - 1, init, desti, temp)
        moveOne(numDisks, init, desti)
        move(numDisks - 1, temp, init, desti)
n, a, b, c = input().split()
move(int(n), a, b, c)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240312175949751](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403121759908.png)



**03253: 约瑟夫问题No.2**

http://cs101.openjudge.cn/practice/03253



思路：

​	

##### 代码

```python
#刘乐天 2300012105 生命科学学院
while True:
    n, p, m = map(int, input().split())
    if {n,p,m} == {0}:
        break
    monkey = [i for i in range(1, n+1)]
    for _ in range(p-1):
        tmp = monkey.pop(0)
        monkey.append(tmp)
    # print(monkey)

    index = 0
    ans = []
    while len(monkey) != 1:
        temp = monkey.pop(0)
        index += 1
        if index == m:
            index = 0
            ans.append(temp)
            continue
        monkey.append(temp)

    ans.extend(monkey)

    print(','.join(map(str, ans)))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240312174358271](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403121744454.png)



**21554:排队做实验 (greedy)v0.2**

http://cs101.openjudge.cn/practice/21554



思路：



##### 代码

```python

#刘乐天 2300012105 生命科学学院
n = int(input())
t = [(i, int(j)) for i, j in enumerate(input().split(), 1)]
tt = t.copy()
tt.sort(key=lambda x: x[1])

ans = []
for i in tt:
    ans.append(i[0])

print(*ans)

dp = [0] * n
dp[0] = 0
for i in range(1, n):
    dp[i] = dp[i - 1] + tt[i - 1][1]

print('{:.2f}'.format(sum(dp) / n))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240312174752464](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403121747513.png)



**19963:买学区房**

http://cs101.openjudge.cn/practice/19963



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
n = int(input())
dis = [eval(x)[0]+eval(x)[1] for x in input().split()]
pri = [int(x) for x in input().split()]
vau = [dis[x]/pri[x] for x in range(n)]
def mid(n,lis):
    lis = sorted(lis)
    if n%2==1:
        return lis[n//2]
    else:
        return (lis[n//2-1]+lis[n//2])/2
prim = mid(n, pri)
vaum = mid(n, vau)
sum = 0
for i in range(n):
    if vau[i]>vaum and pri[i]<prim:
        sum +=1
print(sum)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240312175143662](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403121751714.png)



**27300: 模型整理**

http://cs101.openjudge.cn/practice/27300



思路：



##### 代码

```python
#刘乐天 2300012105 生命科学学院
from collections import defaultdict

n = int(input())
d = defaultdict(list)
for _ in range(n):
    #name, para = input().strip().split('-')
    name, para = input().split('-')
    if para[-1]=='M':
        d[name].append((para, float(para[:-1])/1000) )
    else:
        d[name].append((para, float(para[:-1])))


sd = sorted(d)
#print(d)
for k in sd:
    paras = sorted(d[k],key=lambda x: x[1])
    #print(paras)
    value = ', '.join([i[0] for i in paras])
    print(f'{k}: {value}')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240312175604349](https://cdn.jsdelivr.net/gh/xueswde/picture@main/img/202403121756400.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

​	练习了队列相关的方法，学习了defaultdict（）、eval（）等函数。



