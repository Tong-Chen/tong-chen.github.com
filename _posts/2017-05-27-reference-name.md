---
title: 参考文献中杂志名字问题
author: ct
layout: post
categories:
  - Bioinformatics
tags:
  - Bioinformatics
---

Endnote在获取参考文献时由于来源不同，捕获的杂志名称格式也不同，有时为全称，有时为不加点的缩写，有时为加点的缩写，这在引用时会造成一些麻烦，使得论文中参考文献来源的杂志名字不统一。而这一点，不能单纯的通过修改`Endnote-output style`来解决。一个方法是论文定稿后，手工一个个修改，这个比较费力，而且浪费宝贵的时间；另一个方法是采用下述的文献名字替换方法，把不规范的名字都替换成整理好的规范的名字，这样就可以通过在`output style`中选择`全名`、`加点的缩写`、`不加点的缩写`来实现杂志名字的统一配置。

## 调整办法

1. 下载杂志的名字及其缩写表 （<https://www.library.uq.edu.au/faqs/endnote/medical_2010.txt>）

2. 将`medical_2010.txt`的文字复制称为两份，第二份中用第3列替换第一列，然后合并到原文件。Endnote会利用第一列的杂志名去跟其自动获取的杂志名字去匹配，从而关联上这些杂志名字的全名和缩写名（文件的2,3,4列）。因为前面提到Endnote获取杂志名时有时是全名，有时是缩写，因此索引列要包含的不同类型的名字足够多，这也就是这一步操作的目的。

3. 或者跳过前两步使用我整理的名字和缩写表 (下载地址 <http://pan.baidu.com/s/1i5637tr>)

3. 若`medical_2010.txt`没收录你关注的杂志，可自行添加。（杂志缩写加点的原则是：缩写词后加点，非缩写词不加点）

4. 打开`endnote` - `tools` - `open term lists`  - `journal term list`，在打开的对话框中选择`journals`并且点击`Delete List`。

5. 然后点击`create list`，在弹出框中输入`Journals` (注意大小写)，勾选单选框(`Journal list`)，点击`OK`。

6. 点击`Import List`--选择刚才修改过的`medial_2010.txt`--导入

7. 防止自动更新：菜单`edit` - `Preferences` - `Term Lists`- 不选择`Update list when importing or pasting references`.

8. 更新文献

## 自行添加文献的方法：

假如在Endnote中你收录了一个文献没有包含在我们之前导入的文件中，它的`Journal`项名字为 `Hootie and the Blowfish`，它对应的缩写为`Hoo and the Blow`。那么你需要在
`medical_2010.txt`中添加如下行，然后再次重复上述导入操作：

```
Hootie and the Blowfish         Hoo. and the Blow.        Hoo and the Blow        Hootie and the Blowfish
```

这四列分别表示 `索引列`，`杂志带点缩写列`，`杂志无点缩写列`，`杂志全称列`。Endnote会拿其收录文献的`Journal`项的名字去我们导入的这个文件
的第一列去匹配，这也是为什么我们使用`Journal`项的名字作为第一列，然后去提取对应的杂志缩写列和全称列。


