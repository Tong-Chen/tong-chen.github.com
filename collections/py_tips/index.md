---
title: Python tips
author: ct
layout: page
---

1. UnicodeDecodeError: 'ascii' codec can not decode byte 0xe9 in position 0: ordinal not in range(128))

   ```python
   import sys
   reload(sys)
   sys.setdefaultencoding('utf8')
   ```

2. 启动HTTP服务

   ```python
   cd specific_dir_containing_an_index.html
   python -m SimpleHTTPServer 11521 # 11521 as port number
   ```

3. Generate a combination for all elements in a 2-d list.

   ```python
   def iterateLists(optL, resultL, recordL=[]):
       '''
       optL = [
               ["-p prot1", "-p prot2", "-p prot3"], 
               ["-l chem1", "-l chem2"], 
               ["-o result"]
              ]
       
       recordL: tmp record variable
   
       resultL = [
           ["-p prot1", "-l chem1",  "result"], 
           ["-p prot1", "-l chem2",  "result"]
       ]
   
       '''
       if debug:
           print >>sys.stderr, "New"
           print >>sys.stderr, optL
           print >>sys.stderr, recordL
       for opt in optL[0]:
           newOptL = optL[1:]
           if len(newOptL) > 1:
               tmpL = recordL[:]
               tmpL.append(opt)
               if debug:
                   print >>sys.stderr, "Next"
                   print >>sys.stderr, newOptL
                   print >>sys.stderr, tmpL
               iterateLists(newOptL, resultL, tmpL)
           else:
               for last_opt in newOptL[0]:
                   tmpL = recordL[:]
                   tmpL.append(opt)
                   tmpL.append(last_opt)
                   resultL.append(tmpL)
   #------------------------------------
   a = a = [[1],  [2,  3],  [4,  5],  [6]]
   resultL = []
   iterateLists(a, resultL)
   resultL
   [[1, 2, 4, 6], [1, 2, 5, 6], [1, 3, 4, 6], [1, 3, 5, 6]]
   ```

4. Check if system command runs successfully

   ```
   if os.system(cmd):
	   print >>sys.stderr, cmd + ' failed'
	   sys.exit(1)
   ```

5. 获取软连接的绝对路径

```
os.path.realpath("link_file")
```

6. 获得文件大小

```
os.path.exists(file)
os.stat(file).st_size
```

7. 调用系统命令，并指导timeout

```
from subprocess32 import call, TimeoutExpired
cmd = ['cmd', '-p1', 'p1value', '-p2', 'p2value']
try:
	call(cmd, timeout=5)
except TimeoutExpired:
	print >>sys.stderr, "Time out"
```

8. 调用系统指令并获得输出

```
from subprocess32 import check_output
output = check_output(' '.join(cmd), shell=True)
output
```

8. Python mail

```
msg = MIMEMultipart()  
msg['From'] = "%s<%s>" % (Header("易生信培训", "utf-8"), "train@ehbio.com")
msg['To'] = '1@ehbio.com, 2@ehbio.com'
msg['Cc'] = '3@ehbio.com'

mailServer.sendmail(gmailUser, ['1@ehbio.com', '2@ehbio.com', '3@ehbio.com'],  msg.as_string()) 

```

9. multiple thread

```
from multiprocessing.dummy import Pool
from functools import partial
from subprocess import call
pool = Pool(10) # 10 threads
# pool.map(func, iteratable)
pool.map(partial(call,  shell=True),  cmdL)
pool.close()
pool.join

```

10. 获取文件名和目录名

```
head,  tail = os.path.split(" /tmp/d/a.dat" )
print(tail)
a.dat
print(head)
/tmp/d
```

11. 列表死循环

```
for i in lineL:
	lineL.append(i)

for i in lineL[:]:
	lineL.append(i)
```

