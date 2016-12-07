---
title: Python tips
author: ct
layout: page
---


### 记录无法归类的小问题及解决方法

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

