---
title: Python解析psiBlast输出的JSON文件结果
author: ct
layout: post
categories:
  - Python
tags:
  - Python
  - Bioinfo
---

### 什么是JSON文件

JSON文件是一种轻量级的数据存储和交换格式，其实质是字典和列表的组合。这在定义生信分析流程的参数文件中具有很好的应用。

```
{
	"公众号": {
		"名字": "生信宝典", 
		"宗旨": "为生信服务", 
		"正确地打开方式": [
			"阅读", 
			"置顶", 
			"转发"
		]	
	} 
}
```

在Python中解析JSON是通过如下代码完成的

```
import json
file_fh = open("test2.json")
ajsonD = json.load(file_fh)
ajsonD
{'公众号': {'宗旨': '为生信服务',  '正确地打开方式': ['阅读',  '置顶',  '转发'],  '名字': '生信宝典'}}
ajsonD['公众号']['名字']
'生信宝典'
```

### 什么是PSIBLAST

PSI-BLAST位置特异的迭代搜索工具，输入为位置得分矩阵或多序列比对图谱，搜索匹配到的序列会更新到搜索信息中进行进一步搜索，直到没有新的序列搜索到，常用于发现远同源基因。 (Position-Specific Iterative Basic Local Alignment Search Tool) derives a position-specific scoring matrix (PSSM) or profile from the multiple sequence alignment of sequences detected above a given score threshold using protein–protein BLAST. This PSSM is used to further search the database for new matches, and is updated for subsequent iterations with these newly detected sequences. Thus, PSI-BLAST provides a means of detecting distant relationships between proteins.

著名的`TET`家族蛋白(哺乳动物主动去甲基化酶, 美国科学院院士Anjana Rao), `NgAgo`(具体功能存疑，韩主席的工作)，`Cas`家族蛋白(序列分析大牛Eugene V. Koonin的工作)都是通过`PSI-BLAST`搜索出来的, 可见其强大。

### Python解析PSIBLAST的JSON输出结果

BLAST的输出结果可以有多种，在线的配对比较结果，线下常用的表格输出，这次尝试的是JSON的输出，运行命令如下

```
psiblast -db nr -out Known_CPS.CUI.mfa.psiblast -evalue 0.0001 -outfmt 13 -num_threads 10 -num_iterations 0 -in_msa Known_CPS.CUI.mfa
```

这次编程的目的是通过解析输出的JSON结果获取匹配的蛋白的名字和序列，JSON文件解析的关键是知道关注的信息在哪个关键字下可以找到，然后需要怎么操作进入到关键字所在数据层，具体操作见如下视频，视频中一步步尝试如何不断试错，解析JSON文件，获得想要的Python脚本和解析结果。

{::nomarkdown}
<embed src="https://imgcache.qq.com/tencentvideo_v1/playerv3/TPout.swf?max_age=86400&v=20161117&vid=p0542g1puwt&auto=0" allowFullScreen="true" quality="high" width="480" height="400" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed>
{:/nomarkdown}


