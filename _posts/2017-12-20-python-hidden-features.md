---
title: Python学习之路和隐藏特征
author: ct
layout: post
categories:
  - Python
tags:
  - Python
  - Bioinfo
---

针对生信领域的零基础爱好者及生信分析中遇到的种种问题,生信领域知名公众号“生信宝典”团队组织了中科院系统项目经验丰富的一线科研人员开展系列培训活动。

在[小学生都学Python了，你还不知道怎么开始](http://mp.weixin.qq.com/s/1JlAROpOCBwaG574EwvkVw)文中介绍了Python的应用广泛，功能强大，提供了Python的在线学习视频和资料等。

学习程序语言不是一件难事，也不是一件简单事。[为什么编程这么难](http://mp.weixin.qq.com/s/dD37HygYagxIlxEi1JwnKw)中翻译了一篇编程学习的心路历程。

（图例“编程信心与能力”：纵轴为信心值，横轴为能力水平，虚线从左至右依次分割出手牵手蜜月期、混沌悬崖、绝望沙漠、令人兴奋的上升期四个阶段，第5条虚线标志着工作准备就绪）

在我看来，学习编程是**学以致用**，学习方式是**硬着头皮**去写。

**读文档**是蜜月期，读读就过去，谁都会。

**写程序**是混沌悬崖，知道是这么回事，就是写不出来；

**调程序**是绝望沙漠，怎么看自己写的都对，就是编译器不开眼；

**程序正确了**就是兴奋期，万里长征迈出又一步。

这些过程没有捷径，但可以加速，就是我们的**[零基础Python编程班，应用Python处理生物信息数据和作图](www.ehbio.com/Training)**。

![](http://www.ehbio.com/Training/Public/images/mapython.png)

广告做完了，来点Python的特性。

Python编程有其特有的方式 **phyonic**，下面是python编程一些有意思的用法和技巧，总结出来，以飨大家。

1.原位替换


```python
a = 5
b = 6
c = 7
a, b = b,a
print("a is",a)
print("b is",b)
```

    a is 6
    b is 5



```python
a, (b,c) = c, (a,b)
print("a is",a)
print("b is",b)
print("c is",c)
```

    a is 7
    b is 6
    c is 5



```python
first, *middle_all, last = (1,2,3,4,5,6)
middle_all
```




    [2, 3, 4, 5]

2.链似比较


```python
x = 5
print("1 < x < 10 is", 1 < x < 10)
print("10 > x <= 9", 10 > x <= 9)
```

    1 < x < 10 is True
    10 > x <= 9 True


3.列表索引，反序


```python
a = [1,2,3,4,5]
a[::2]
```

    [1, 3, 5]

```python
a[::-1]
```

    [5, 4, 3, 2, 1]


4.列表解析、字典解析、元组解析


```python
# 获得系列坐标点
a = ((i,j) for i in range(3) for j in range(2))
a
```
    <generator object <genexpr> at 0x7fa8d04d7fc0>


```python
for i in a:
    print(i)
```

    (0, 0)
    (0, 1)
    (1, 0)
    (1, 1)
    (2, 0)
    (2, 1)

```python
str1 = "I love sheng xin bao dian"
print([i for i in str1.split() if i.endswith('n')])
```

    ['xin', 'dian']

```python
a = {i:i*2 for i in range(5)}
a
```

    {0: 0, 1: 2, 2: 4, 3: 6, 4: 8}

```python
[(x, y) for x in range(4) if x % 2 == 1 for y in range(4)]
```

    [(1, 0), (1, 1), (1, 2), (1, 3), (3, 0), (3, 1), (3, 2), (3, 3)]

5.集合操作


```python
a = set(["sheng", "xin", "bao","dian","best","tutotials"])
b = set(["hong", "ji", "yin","zu","best","tutotials"])
a | b  # union
```

    {'bao', 'best', 'dian', 'hong', 'ji', 'sheng', 'tutotials', 'xin', 'yin', 'zu'}

```python
a & b # intersection
```

    {'best', 'tutotials'}

```python
a ^ b # Symmetric Difference
```

    {'bao', 'dian', 'hong', 'ji', 'sheng', 'xin', 'yin', 'zu'}

6.Negative round


```python
print("round整数:",str(round(1234.5678, -2)))

print("round小数:",str(round(1234.5678, 2)))
```

    round整数: 1200.0
    round小数: 1234.57


7.多行字符串的优雅嵌套


```python
# \可以，但是第二行需要起头
system_command = "s-plot pheatmap -f matrix \
-t heatmap -a TRUE"
print(system_command)
```

    s-plot pheatmap -f matrix -t heatmap -a TRUE


```python
# 字符串中包含换行符
# 切第二行要起头，不然会有较多空格
system_command = """s-plot pheatmap -f matrix
-t heatmap -a TRUE""" 
print(system_command)
print(system_command.replace('\n', ' '))
```

    s-plot pheatmap -f matrix 
    -t heatmap -a TRUE
    s-plot pheatmap -f matrix  -t heatmap -a TRUE


```python
# 类元组的写法，既可以跨行，又可以自由格式
# 需要注意2点
   # 类元组，无逗号
   # 字符串连接时不会自动加空格，空格需要保存在字符串里面 
system_command = ("s-plot pheatmap -f matrix "
                  "-t heatmap -a TRUE")
print(system_command)
```

    s-plot pheatmap -f matrix -t heatmap -a TRUE


```python
# 多一步join；
system_command = ["s-plot pheatmap -f matrix",
                  "-t heatmap -a TRUE"]
print(' '.join(system_command))
```

    s-plot pheatmap -f matrix -t heatmap -a TRUE


8.zip转换两个列表为字典


```python
keyL = [1,2,3]
valueL = ['a','b','v']
for i ,j in zip(keyL, valueL):
    print(i,j)
```

    1 a
    2 b
    3 v

```python
import pprint
pprint.pprint(dict(zip(keyL, valueL)))
```

    {1: 'a', 2: 'b', 3: 'v'}

```python
dict([(i,j) for i ,j in zip(keyL, valueL)])
```

    {1: 'a', 2: 'b', 3: 'v'}

9.enumerate索引列表 (不再使用len)


```python
a = ['s','x','b','d']

# Preferred way
for index, item in enumerate(a):
    print(index,item)

print("\n")

# Old way
for i in range(len(a)):
    print(i,a[i])
    
```

    0 s
    1 x
    2 b
    3 d
    
    
    0 s
    1 x
    2 b
    3 d
	
10.矩阵转置


```python
a = [(1,2), (3,4), (5,6)]
b = zip(*a)
for i in b:
    print(i)
```

    (1, 3, 5)
    (2, 4, 6)


11.sum的另一用法，二维数组秒变1维


```python
aList = [[1, 2, 3], [4, 5], [6], [7, 8, 9]]
sum(aList, [])
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9]



12.解释正则表达式


```python
import re
re.compile("^[a-z]*$", re.DEBUG)
```

    AT AT_BEGINNING
    MAX_REPEAT 0 MAXREPEAT
      IN
        RANGE (97, 122)
    AT AT_END


```python
re.compile("^[a-z][0-9]+$", re.DEBUG)
```

    AT AT_BEGINNING
    IN
      RANGE (97, 122)
    MAX_REPEAT 1 MAXREPEAT
      IN
        RANGE (48, 57)
    AT AT_END


```python
re.compile("^[a-z]([0-9]+)$", re.DEBUG)
```

    AT AT_BEGINNING
    IN
      RANGE (97, 122)
    SUBPATTERN 1 0 0
      MAX_REPEAT 1 MAXREPEAT
        IN
          RANGE (48, 57)
    AT AT_END


13.for..else;若`for`循环中未执行`break`,则`else`会被执行


```python
found = False
for i in range(2,5):
    if i == 1:
        found = True
        break
if not found: 
    print("i was never 1")
```

    i was never 1



```python
for i in range(2,5):
    if i == 1:
        break
else:
    print("i was never 1")
```

    i was never 1


14.启动网络服务器，用于文件预览或传输


```python
# run in commang line
# python -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

15.python打印九九乘法表 (列表解析)


```python
print('\n'.join([' '.join(['%s*%s=%-2s' % (y,x,x*y) for y in range(1,x+1)]) for x in range(1,10)]))
```

    1*1=1 
    1*2=2  2*2=4 
    1*3=3  2*3=6  3*3=9 
    1*4=4  2*4=8  3*4=12 4*4=16
    1*5=5  2*5=10 3*5=15 4*5=20 5*5=25
    1*6=6  2*6=12 3*6=18 4*6=24 5*6=30 6*6=36
    1*7=7  2*7=14 3*7=21 4*7=28 5*7=35 6*7=42 7*7=49
    1*8=8  2*8=16 3*8=24 4*8=32 5*8=40 6*8=48 7*8=56 8*8=64
    1*9=9  2*9=18 3*9=27 4*9=36 5*9=45 6*9=54 7*9=63 8*9=72 9*9=81


16.`map`, `filter`


```python
# 过滤大于4的元素
a = [3,4,5]
[i for i in a if i<4]
```

    [3]

```python
list(filter(lambda x: x<4, a))
```

    [5]

```python
# 每个元素加2
[i+2 for i in a]
```

    [5, 6, 7]


```python
map(lambda x: x+2, a)
```

    <map at 0x7fa8d0502358>


```python
list(map(lambda x: x+2, a))
```

    [5, 6, 7]

算2的1000次方的各位数之和

```python
sum(map(int, str(2**1000)))
```

    1366



17.python打印心型

```python
print('\n'.join([''.join([('Love'[(x-y) % len('Love')] if ((x*0.05)**2+(y*0.1)**2-1)**3-(x*0.05)**2*(y*0.1)**3 <= 0 else ' ') for x in range(-30, 30)]) for y in range(30, -30, -1)]))
```
  
                                                                
                    veLoveLov           veLoveLov               
                eLoveLoveLoveLove   eLoveLoveLoveLove           
              veLoveLoveLoveLoveLoveLoveLoveLoveLoveLov         
             veLoveLoveLoveLoveLoveLoveLoveLoveLoveLoveL        
            veLoveLoveLoveLoveLoveLoveLoveLoveLoveLoveLov       
            eLoveLoveLoveLoveLoveLoveLoveLoveLoveLoveLove       
            LoveLoveLoveLoveLoveLoveLoveLoveLoveLoveLoveL       
            oveLoveLoveLoveLoveLoveLoveLoveLoveLoveLoveLo       
            veLoveLoveLoveLoveLoveLoveLoveLoveLoveLoveLov       
            eLoveLoveLoveLoveLoveLoveLoveLoveLoveLoveLove       
             oveLoveLoveLoveLoveLoveLoveLoveLoveLoveLove        
              eLoveLoveLoveLoveLoveLoveLoveLoveLoveLove         
              LoveLoveLoveLoveLoveLoveLoveLoveLoveLoveL         
                eLoveLoveLoveLoveLoveLoveLoveLoveLove           
                 oveLoveLoveLoveLoveLoveLoveLoveLove            
                  eLoveLoveLoveLoveLoveLoveLoveLove             
                    veLoveLoveLoveLoveLoveLoveLov               
                      oveLoveLoveLoveLoveLoveLo                 
                        LoveLoveLoveLoveLoveL                   
                           LoveLoveLoveLov                      
                              LoveLoveL                         
                                 Lov                            
                                  v                             
                                                                
   


18. python打印曼德勃罗集合


```python
print('\n'.join([''.join(['*'if abs((lambda a:lambda z,c,n:a(a,z,c,n))(lambda s,z,c,n:z if n==0else s(s,z*z+c,c,n-1))(0,0.02*x+0.05j*y,40))<2 else' 'for x in range(-80,20)])for y in range(-20,20)]))
```

                                                                                    *                   
                                                                                                        
                                                                                                        
                                                                              **                        
                                                                         ***********                    
                                                                        ************                    
                                                                          *********                     
                                                                *    * ************  * *                
                                                        ****** * *************************** *          
                                                        *************************************** *****   
                                                         *******************************************    
                                                   *** ******************************************** *   
                                                    **************************************************  
                                                 *******************************************************
                          *        *              ***************************************************** 
                         **** ******* *          *******************************************************
                          *****************     ******************************************************* 
                       *********************** *********************************************************
                       *********************** ******************************************************** 
                 **** ********************************************************************************  
    *********************************************************************************************       
                 **** ********************************************************************************  
                       *********************** ******************************************************** 
                       *********************** *********************************************************
                          *****************     ******************************************************* 
                         **** ******* *          *******************************************************
                          *        *              ***************************************************** 
                                                 *******************************************************
                                                    **************************************************  
                                                   *** ******************************************** *   
                                                         *******************************************    
                                                        *************************************** *****   
                                                        ****** * *************************** *          
                                                                *    * ************  * *                
                                                                          *********                     
                                                                        ************                    
                                                                         ***********                    
                                                                              **                        
                                                                                                        
                                                                                                        




19.打开一个关于Python漫画的网站


```python
import antigravity
```
