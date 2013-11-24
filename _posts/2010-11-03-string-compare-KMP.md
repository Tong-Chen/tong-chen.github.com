---
title: 字符串比对KMP算法
author: 悟道
layout: post
categories:
  - algorithm
  - C
  - python
tags:
  - algorithm
  - C
  - python
---

KMP算法

一种字符串比对算法，寻找存在于长字符串中的子串，由Knuth、Morris、Pratt三个同时提出来。

算法的基本思路是：

假设有序列seq(长度为m)和子序列subseq(长度为n)，  
首先遍历序列seq，找到subseq[0]第一次出现在seq中的位置k；

然后顺次比较subseq\[j\](0<j<n)与seq\[i\](k<i<m), 即比较以subseq\[0]开头长度为j的序列subseq[0,j]和以seq[i-1]结尾长度为j的序列seq[i-j,i\](此处之所以选择用i而不是k来描述seq的片段，是想通过序列片段而不是单个字符进行移动，继而减少移动次数)：

若在j==n-1时，每个元素都相等，则定位了一个子序列，重复上面的过程即可找到所有子序列的分布位置，若对某一特定的j(0<j<n)使得subseq[j] <> seq[i]， 这时则宣告最初找到的k不合意（应该后移），无法继续延伸，这时需要调整j的值， 继而影响到k的值。为了调整后，依然满足subseq[0,j'] == subseq[i-j',i]，就要求j&#8217;应该满足subseq[0,j']==subseq[j-j',j]，同时最佳j&#8217;应该是满足这个条件的最大值且j&#8217; <> j， 使得能继续参与匹配的序列最长。当然也存在不能找到合适的j&#8217;的情况，这时另j&#8217;等于0， 而增加i的值直到再次碰到subseq[0]。同时，我们可以看到j&#8217;的取值只取决于subseq，因此我们可以提前构建出这样一个索引数组来指导错误匹配之后的移动。

索引数组index的构建：  
索引数组的构建就是对字符串进行自我扫描的过程，每个值都可以递归的由其前一个位的值得出。  
假设index[j-1] = k, 只要index[k] == index[j]，index[j] = index[j-1]+1, 因为index[0,k] = index[j-k,j]， 所以index[0,k+1] == index[j-k, j+1]。若index[k] != index[j]，这时可以回溯到index[index[j-1]，若依然不满足则递归index[index[index[j-1]]，直到满足或取 值为0， 由此得到index数组。

假设seq = &#8216;abaebacddebacdbace&#8217;, subseq = &#8216;bace&#8217;.  
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17  
a b a e b a c d d e b  a  c  d  b  a  c  e

b a c e  
0 1 2 3

当k=1时，subseq[0] == seq[k],  
然后subseq[1] == seq[2], subseq[2] != seq[3], 这时需要调整j的值，使得subseq[0,j']依然等同于  
seq[i-j'+1,i], 这就使得j&#8217;要满足使得subseq[0,j]的前j&#8217;的字母和后j&#8217;个字母完全相同， 由于没有合适的,  
j&#8217;取值0，此时继续增大i的值直到再次在seq里遇到subseq[0]， 重复以上过程。这个例子比较特殊没有利用到算法的优势。  
若子序列不存在重复，用KMP算法和用下面的一个bruteforce程序效果应该相差不大, 另外python的find和index在处理字符串时速度也很可观。

另一个例子是matrix67上的， 大家可过去参考下。

参考：http://www.matrix67.com/blog/archives/115

http://stackoverflow.com/questions/425604/best-way-to-determine-if-a-sequence-is-in-another-sequence-in-python

<div class="wp_codebox">
  <table>
    <tr id="p3148">
      <td class="code" id="p314code8">
        <pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
&nbsp;
<span style="color: #808080; font-style: italic;">#Last Change:  2010-11-03 13:38:36</span>
<span style="color: #ff7700;font-weight:bold;">def</span> compute_prefix_function<span style="color: black;">&#40;</span>p<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
    compute_prefix_function(p) --&gt; a list
&nbsp;
    [p] is a pattern sequence to be searched in a longer sequence.
    '</span><span style="color: #483d8b;">''</span>
    m = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>p<span style="color: black;">&#41;</span>
    pi = <span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">*</span> m
    k = <span style="color: #ff4500;"></span>
    <span style="color: #ff7700;font-weight:bold;">for</span> q <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span>, m<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">while</span> k <span style="color: #66cc66;">&</span>gt<span style="color: #66cc66;">;</span> <span style="color: #ff4500;"></span> <span style="color: #ff7700;font-weight:bold;">and</span> p<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!</span>= p<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span>:
            k = pi<span style="color: black;">&#91;</span>k - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> p<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> == p<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span>:
            k = k + <span style="color: #ff4500;">1</span>
        pi<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span> = k
    <span style="color: #ff7700;font-weight:bold;">return</span> pi
&nbsp;
<span style="color: #ff7700;font-weight:bold;">def</span> kmp_matcher<span style="color: black;">&#40;</span>t, p<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
    kmp_matcher(t, p) --&gt; a list
&nbsp;
    [t, p] is two sequences, which '</span>p<span style="color: #483d8b;">' maybe partof '</span>t<span style="color: #483d8b;">'.
    '</span><span style="color: #483d8b;">''</span>
    n = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>t<span style="color: black;">&#41;</span>
    m = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>p<span style="color: black;">&#41;</span>
    pi = compute_prefix_function<span style="color: black;">&#40;</span>p<span style="color: black;">&#41;</span>
    q = <span style="color: #ff4500;"></span>
    index = <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">while</span> q <span style="color: #66cc66;">&</span>gt<span style="color: #66cc66;">;</span> <span style="color: #ff4500;"></span> <span style="color: #ff7700;font-weight:bold;">and</span> p<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!</span>= t<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>:
            q = pi<span style="color: black;">&#91;</span>q - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> p<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span> == t<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>:
            q = q + <span style="color: #ff4500;">1</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> q == m:
            q = <span style="color: #ff4500;"></span>
            index.<span style="color: black;">append</span><span style="color: black;">&#40;</span>i-m+<span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">#-----end of for---------------------------</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> -<span style="color: #ff4500;">1</span> <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>index<span style="color: black;">&#41;</span> == <span style="color: #ff4500;"></span> <span style="color: #ff7700;font-weight:bold;">else</span> index
&nbsp;
<span style="color: #ff7700;font-weight:bold;">if</span> __name__ == <span style="color: #483d8b;">'__main__'</span>:
    <span style="color: #008000;">str</span> = <span style="color: #483d8b;">"1230012123211212213012300121232112122130123001212321121221312300121232112122130"</span>
    substr = <span style="color: #483d8b;">"1212"</span>
    <span style="color: #808080; font-style: italic;">#for i in range(10000000):</span>
    <span style="color: #808080; font-style: italic;">#    kmp_matcher(str, substr)</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> kmp_matcher<span style="color: black;">&#40;</span><span style="color: #008000;">str</span>, substr<span style="color: black;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

* * *

<div class="wp_codebox">
  <table>
    <tr id="p3149">
      <td class="code" id="p314code9">
        <pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> index<span style="color: black;">&#40;</span>subseq, seq<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">''</span><span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
    index(subseq, seq) --&gt;a list of numbers or -1
    Return an index of [subseq] in the [seq].
    Or -1 if [subseq] is not a subsequence of [seq].
    The time complexity of the algorithm is O(n*m), where
    n, m = len(seq), len(subseq).
    &gt;&gt;&gt;index('</span><span style="color: #ff4500;">12</span><span style="color: #483d8b;">', '</span>0112<span style="color: #483d8b;">')
    [2]
    &gt;&gt;&gt;index([1,2], [011212])
    [2, 4]
    &gt;&gt;&gt;index('</span><span style="color: #ff4500;">13</span><span style="color: #483d8b;">', '</span>0112<span style="color: #483d8b;">')
    -1
    '</span><span style="color: #483d8b;">''</span>
    i, n, m = -<span style="color: #ff4500;">1</span>, <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>seq<span style="color: black;">&#41;</span>, <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>subseq<span style="color: black;">&#41;</span>
    index = <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">try</span>:
        <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #008000;">True</span>:
            i = seq.<span style="color: black;">index</span><span style="color: black;">&#40;</span>subseq<span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span>, i+<span style="color: #ff4500;">1</span>, n - m + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">if</span> subseq == seq<span style="color: black;">&#91;</span>i:i+m<span style="color: black;">&#93;</span>:
                index.<span style="color: black;">append</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">except</span> <span style="color: #008000;">ValueError</span>:
        <span style="color: #ff7700;font-weight:bold;">return</span> index <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>index<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&</span>gt<span style="color: #66cc66;">;</span> <span style="color: #ff4500;"></span> <span style="color: #ff7700;font-weight:bold;">else</span> -<span style="color: #ff4500;">1</span>
<span style="color: #ff7700;font-weight:bold;">def</span> subseqInSeq<span style="color: black;">&#40;</span>subseq, seq<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">''</span><span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
    subseqInSeq(subseq, seq) ---&gt; list or -1
    The same as index.
    '</span><span style="color: #483d8b;">''</span>
    indexList = <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    m = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>subseq<span style="color: black;">&#41;</span>
    subseqRepla = <span style="color: #483d8b;">'*'</span> <span style="color: #66cc66;">*</span> m
    <span style="color: #ff7700;font-weight:bold;">while</span> subseq<span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">in</span> seq:
        index = seq.<span style="color: black;">index</span><span style="color: black;">&#40;</span>subseq<span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> subseq == seq<span style="color: black;">&#91;</span>index:index+m<span style="color: black;">&#93;</span>:
            indexList.<span style="color: black;">append</span><span style="color: black;">&#40;</span>index<span style="color: black;">&#41;</span>
            seq = seq.<span style="color: black;">replace</span><span style="color: black;">&#40;</span>subseq, subseqRepla, <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">else</span>:
            seq = seq.<span style="color: black;">replace</span><span style="color: black;">&#40;</span>subseq<span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span>, <span style="color: #483d8b;">'*'</span>, <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>indexList <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>indexList<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&</span>gt<span style="color: #66cc66;">;</span> <span style="color: #ff4500;"></span> <span style="color: #ff7700;font-weight:bold;">else</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
<span style="color: #ff7700;font-weight:bold;">def</span> main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> index<span style="color: black;">&#40;</span><span style="color: #483d8b;">'ab'</span>, <span style="color: #483d8b;">'abcdab'</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> subseqInSeq<span style="color: black;">&#40;</span><span style="color: #483d8b;">'ab'</span>, <span style="color: #483d8b;">'abcdab'</span><span style="color: black;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

* * *

<div class="wp_codebox">
  <table>
    <tr id="p31410">
      <td class="code" id="p314code10">
        <pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include</span>
<span style="color: #339933;">#include</span>
<span style="color: #339933;">#include </span>
&nbsp;
<span style="color: #993333;">int</span> kmp<span style="color: #009900;">&#40;</span><span style="color: #993333;">char</span> <span style="color: #339933;">*</span>substr<span style="color: #339933;">,</span> <span style="color: #993333;">char</span> <span style="color: #339933;">*</span>str<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> <span style="color: #339933;">*</span>index<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #993333;">int</span> prefix<span style="color: #009900;">&#40;</span><span style="color: #993333;">char</span> <span style="color: #339933;">*</span>substr<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> lensub<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> <span style="color: #339933;">*</span>subIndex<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
<span style="color: #808080; font-style: italic;">/* this is a string compare function using KMP */</span>
<span style="color: #993333;">int</span> kmp<span style="color: #009900;">&#40;</span><span style="color: #993333;">char</span> <span style="color: #339933;">*</span>substr<span style="color: #339933;">,</span> <span style="color: #993333;">char</span> <span style="color: #339933;">*</span>str<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> <span style="color: #339933;">*</span>index<span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
	<span style="color: #993333;">int</span> lensub<span style="color: #339933;">,</span> lenstr<span style="color: #339933;">;</span>
	<span style="color: #993333;">int</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
	<span style="color: #993333;">int</span> q <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
	<span style="color: #993333;">int</span> k <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//a index of array-index</span>
	lensub <span style="color: #339933;">=</span> strlen<span style="color: #009900;">&#40;</span>substr<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	lenstr <span style="color: #339933;">=</span> strlen<span style="color: #009900;">&#40;</span>str<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #993333;">int</span> subIndex<span style="color: #009900;">&#91;</span>lensub<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
&nbsp;
	prefix<span style="color: #009900;">&#40;</span>substr<span style="color: #339933;">,</span> lensub<span style="color: #339933;">,</span> subIndex<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">;</span> i <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lenstr <span style="color: #339933;">;</span> i<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		<span style="color: #b1b100;">while</span><span style="color: #009900;">&#40;</span> <span style="color: #009900;">&#40;</span>q <span style="color: #339933;">&</span>gt<span style="color: #339933;">;</span> <span style="color: #0000dd;"></span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&</span>amp<span style="color: #339933;">;&</span>amp<span style="color: #339933;">;</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>substr<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #339933;">!=</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>str<span style="color: #339933;">+</span>i<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
		<span style="color: #009900;">&#123;</span>
			q <span style="color: #339933;">=</span> subIndex<span style="color: #009900;">&#91;</span>q<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
		<span style="color: #009900;">&#125;</span>
		<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>substr<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>str<span style="color: #339933;">+</span>i<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span>
		<span style="color: #009900;">&#123;</span>
			q<span style="color: #339933;">++;</span>
		<span style="color: #009900;">&#125;</span>
		<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> q <span style="color: #339933;">==</span> lensub <span style="color: #009900;">&#41;</span>
		<span style="color: #009900;">&#123;</span>
			q <span style="color: #339933;">=</span> subIndex<span style="color: #009900;">&#91;</span>q<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
			<span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>index<span style="color: #339933;">+</span>k<span style="color: #009900;">&#41;</span> <span style="color: #339933;">=</span> i<span style="color: #339933;">-</span>lensub<span style="color: #339933;">+</span><span style="color: #0000dd;">2</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//1 or 2</span>
			k<span style="color: #339933;">++;</span>
		<span style="color: #009900;">&#125;</span>
	<span style="color: #009900;">&#125;</span>
	<span style="color: #b1b100;">return</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #808080; font-style: italic;">/* this does a self kmp of short string to get the prefix function */</span>
<span style="color: #993333;">int</span> prefix<span style="color: #009900;">&#40;</span><span style="color: #993333;">char</span> <span style="color: #339933;">*</span>substr<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> lensub<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> <span style="color: #339933;">*</span>subIndex<span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
	<span style="color: #993333;">int</span> k <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
	<span style="color: #993333;">int</span> q <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> q <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">;</span> q <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lensub <span style="color: #339933;">;</span> q<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		<span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>subIndex<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
&nbsp;
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> q <span style="color: #339933;">=</span> <span style="color: #0000dd;">1</span> <span style="color: #339933;">;</span> q <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lensub <span style="color: #339933;">;</span> q<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		<span style="color: #b1b100;">while</span><span style="color: #009900;">&#40;</span> k <span style="color: #339933;">&</span>gt<span style="color: #339933;">;</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">&</span>amp<span style="color: #339933;">;&</span>amp<span style="color: #339933;">;</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>substr<span style="color: #339933;">+</span>k<span style="color: #009900;">&#41;</span> <span style="color: #339933;">!=</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>substr<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span>
		<span style="color: #009900;">&#123;</span>
			k <span style="color: #339933;">=</span> subIndex<span style="color: #009900;">&#91;</span>k<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
		<span style="color: #009900;">&#125;</span>
		<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>substr<span style="color: #339933;">+</span>k<span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>substr<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span>
		<span style="color: #009900;">&#123;</span>
			k<span style="color: #339933;">++;</span>
		<span style="color: #009900;">&#125;</span>
		<span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>subIndex<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #339933;">=</span> k<span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
	<span style="color: #b1b100;">return</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #993333;">int</span> main<span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span> argc<span style="color: #339933;">,</span> <span style="color: #993333;">char</span> <span style="color: #339933;">*</span>argv<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
	clock_t start<span style="color: #339933;">,</span> finish<span style="color: #339933;">;</span>
	start <span style="color: #339933;">=</span> clock<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #993333;">double</span> duration<span style="color: #339933;">;</span>
	<span style="color: #993333;">char</span> <span style="color: #339933;">*</span>str <span style="color: #339933;">=</span> <span style="color: #ff0000;">"CGTAACGCGTGCCGCGGCTACGTAACGCGGCTA"</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #993333;">char</span> <span style="color: #339933;">*</span>substr <span style="color: #339933;">=</span> <span style="color: #ff0000;">"CGCG"</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #993333;">int</span> lenindex<span style="color: #339933;">;</span>
	lenindex <span style="color: #339933;">=</span> strlen<span style="color: #009900;">&#40;</span>str<span style="color: #009900;">&#41;</span><span style="color: #339933;">/</span>strlen<span style="color: #009900;">&#40;</span>substr<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #993333;">int</span> index<span style="color: #009900;">&#91;</span>lenindex<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
	<span style="color: #993333;">int</span> i<span style="color: #339933;">;</span>
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">;</span> i <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lenindex <span style="color: #339933;">;</span> i<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		index<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
&nbsp;
	kmp<span style="color: #009900;">&#40;</span>substr<span style="color: #339933;">,</span> str<span style="color: #339933;">,</span> <span style="color: #339933;">&</span>amp<span style="color: #339933;">;</span>index<span style="color: #009900;">&#91;</span><span style="color: #0000dd;"></span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">;</span> i <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lenindex <span style="color: #339933;">;</span> i<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> index<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">==</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span> <span style="color: #009900;">&#41;</span>
		<span style="color: #009900;">&#123;</span>
			<span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
		<span style="color: #009900;">&#125;</span>
		<a href="http://www.opengroup.org/onlinepubs/009695399/functions/printf.html"><span style="color: #000066;">printf</span></a><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"%d<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">,</span> index<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
	finish <span style="color: #339933;">=</span> clock<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	duration <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">double</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#40;</span>finish<span style="color: #339933;">-</span>start<span style="color: #009900;">&#41;</span> <span style="color: #339933;">/</span> CLOCKS_PER_SEC<span style="color: #339933;">;</span>
	<a href="http://www.opengroup.org/onlinepubs/009695399/functions/printf.html"><span style="color: #000066;">printf</span></a><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"Done, %f seconds<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">,</span> duration<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #b1b100;">return</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

* * *

<div class="wp_codebox">
  <table>
    <tr id="p31411">
      <td class="code" id="p314code11">
        <pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include</span>
<span style="color: #339933;">#include</span>
<span style="color: #339933;">#include</span>
<span style="color: #339933;">#include </span>
&nbsp;
<span style="color: #993333;">typedef</span> <span style="color: #993333;">unsigned</span> <span style="color: #993333;">char</span> byte<span style="color: #339933;">;</span>
&nbsp;
<span style="color: #993333;">int</span> kmp<span style="color: #009900;">&#40;</span>byte <span style="color: #339933;">*</span>bitsub<span style="color: #339933;">,</span> byte <span style="color: #339933;">*</span>bit<span style="color: #339933;">,</span> <span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> lensub<span style="color: #339933;">,</span>
		<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> lenbit<span style="color: #339933;">,</span> <span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> <span style="color: #339933;">*</span>index<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #993333;">int</span> prefix<span style="color: #009900;">&#40;</span>byte <span style="color: #339933;">*</span>bitsub<span style="color: #339933;">,</span> <span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> lensub<span style="color: #339933;">,</span> <span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> <span style="color: #339933;">*</span>subIndex<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
<span style="color: #808080; font-style: italic;">/* this is a string compare function using KMP */</span>
<span style="color: #993333;">int</span> kmp<span style="color: #009900;">&#40;</span>byte <span style="color: #339933;">*</span>bitsub<span style="color: #339933;">,</span> byte <span style="color: #339933;">*</span>bit<span style="color: #339933;">,</span> <span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> lensub<span style="color: #339933;">,</span>
		<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> lenbit<span style="color: #339933;">,</span> <span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> <span style="color: #339933;">*</span>index<span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> q <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> k <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//a index of array-index</span>
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> subIndex<span style="color: #009900;">&#91;</span>lensub<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
&nbsp;
	prefix<span style="color: #009900;">&#40;</span>bitsub<span style="color: #339933;">,</span> lensub<span style="color: #339933;">,</span> subIndex<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">;</span> i <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lenbit <span style="color: #339933;">;</span> i<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		<span style="color: #b1b100;">while</span><span style="color: #009900;">&#40;</span> <span style="color: #009900;">&#40;</span>q <span style="color: #339933;">&</span>gt<span style="color: #339933;">;</span> <span style="color: #0000dd;"></span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&</span>amp<span style="color: #339933;">;&</span>amp<span style="color: #339933;">;</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>bitsub<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #339933;">^</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>bit<span style="color: #339933;">+</span>i<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//*(bitsub+q) != *(bit+i))</span>
		<span style="color: #009900;">&#123;</span>
			q <span style="color: #339933;">=</span> subIndex<span style="color: #009900;">&#91;</span>q<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
		<span style="color: #009900;">&#125;</span>
		<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> <span style="color: #339933;">!</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>bitsub<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #339933;">^</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>bit<span style="color: #339933;">+</span>i<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//*(bitsub+q) == *(bit+i))</span>
		<span style="color: #009900;">&#123;</span>
			q<span style="color: #339933;">++;</span>
		<span style="color: #009900;">&#125;</span>
		<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> <span style="color: #339933;">!</span><span style="color: #009900;">&#40;</span>q <span style="color: #339933;">^</span> lensub<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span> <span style="color: #666666; font-style: italic;">//q == lensub</span>
		<span style="color: #009900;">&#123;</span>
			q <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
			<span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>index<span style="color: #339933;">+</span>k<span style="color: #009900;">&#41;</span> <span style="color: #339933;">=</span> i<span style="color: #339933;">-</span>lensub<span style="color: #339933;">+</span><span style="color: #0000dd;">2</span><span style="color: #339933;">;</span>
			k<span style="color: #339933;">++;</span>
		<span style="color: #009900;">&#125;</span>
	<span style="color: #009900;">&#125;</span>
&nbsp;
	<span style="color: #b1b100;">return</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #808080; font-style: italic;">/* this does a self kmp of short string to get the prefix function */</span>
<span style="color: #993333;">int</span> prefix<span style="color: #009900;">&#40;</span>byte <span style="color: #339933;">*</span>bitsub<span style="color: #339933;">,</span> <span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> lensub<span style="color: #339933;">,</span> <span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> <span style="color: #339933;">*</span>subIndex<span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> k <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> q <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> q <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">;</span> q <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lensub <span style="color: #339933;">;</span> q<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		<span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>subIndex<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
&nbsp;
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> q <span style="color: #339933;">=</span> <span style="color: #0000dd;">1</span> <span style="color: #339933;">;</span> q <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lensub <span style="color: #339933;">;</span> q<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		<span style="color: #b1b100;">while</span><span style="color: #009900;">&#40;</span> k <span style="color: #339933;">&</span>gt<span style="color: #339933;">;</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">&</span>amp<span style="color: #339933;">;&</span>amp<span style="color: #339933;">;</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>bitsub<span style="color: #339933;">+</span>k<span style="color: #009900;">&#41;</span> <span style="color: #339933;">^</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>bitsub<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//*(bitsub+k) != *(bitsub+q)</span>
		<span style="color: #009900;">&#123;</span>
			k <span style="color: #339933;">=</span> subIndex<span style="color: #009900;">&#91;</span>k<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
		<span style="color: #009900;">&#125;</span>
		<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>bitsub<span style="color: #339933;">+</span>k<span style="color: #009900;">&#41;</span> <span style="color: #339933;">^</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>bitsub<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//*(bitsub+k) == *(bitsub+q) )</span>
		<span style="color: #009900;">&#123;</span>
			k<span style="color: #339933;">++;</span>
		<span style="color: #009900;">&#125;</span>
		<span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>subIndex<span style="color: #339933;">+</span>q<span style="color: #009900;">&#41;</span> <span style="color: #339933;">=</span> k<span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
	<span style="color: #b1b100;">return</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #993333;">int</span> main<span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span> argc<span style="color: #339933;">,</span> <span style="color: #993333;">char</span> <span style="color: #339933;">*</span>argv<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
&nbsp;
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> i<span style="color: #339933;">;</span>
	<span style="color: #993333;">struct</span> timeval start<span style="color: #339933;">;</span>
	<span style="color: #993333;">struct</span> timeval finish<span style="color: #339933;">;</span>
	gettimeofday<span style="color: #009900;">&#40;</span><span style="color: #339933;">&</span>amp<span style="color: #339933;">;</span>start<span style="color: #339933;">,</span> NULL<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #993333;">double</span> duration<span style="color: #339933;">;</span>
	byte bit<span style="color: #009900;">&#91;</span><span style="color: #0000dd;">79</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span>
		<span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span>
		<span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;"></span><span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
	byte bitsub<span style="color: #009900;">&#91;</span><span style="color: #0000dd;">4</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #339933;">,</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> lenindex<span style="color: #339933;">;</span>
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> lenbit <span style="color: #339933;">=</span> <span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>bit<span style="color: #009900;">&#41;</span><span style="color: #339933;">/</span><span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>byte<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> lensub <span style="color: #339933;">=</span> <span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>bitsub<span style="color: #009900;">&#41;</span><span style="color: #339933;">/</span><span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>byte<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	lenindex <span style="color: #339933;">=</span> lenbit<span style="color: #339933;">/</span>lensub<span style="color: #339933;">;</span>
	<span style="color: #993333;">unsigned</span> <span style="color: #993333;">int</span> index<span style="color: #009900;">&#91;</span>lenindex<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">;</span> i <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lenindex <span style="color: #339933;">;</span> i<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		index<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">;</span> i <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> <span style="color: #0000dd;">1000000</span> <span style="color: #339933;">;</span> i<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		kmp<span style="color: #009900;">&#40;</span>bitsub<span style="color: #339933;">,</span> bit<span style="color: #339933;">,</span> lensub<span style="color: #339933;">,</span> lenbit<span style="color: #339933;">,</span> <span style="color: #339933;">&</span>amp<span style="color: #339933;">;</span>index<span style="color: #009900;">&#91;</span><span style="color: #0000dd;"></span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
&nbsp;
	kmp<span style="color: #009900;">&#40;</span>bitsub<span style="color: #339933;">,</span> bit<span style="color: #339933;">,</span> lensub<span style="color: #339933;">,</span> lenbit<span style="color: #339933;">,</span> <span style="color: #339933;">&</span>amp<span style="color: #339933;">;</span>index<span style="color: #009900;">&#91;</span><span style="color: #0000dd;"></span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;"></span> <span style="color: #339933;">;</span> i <span style="color: #339933;">&</span>lt<span style="color: #339933;">;</span> lenindex <span style="color: #339933;">;</span> i<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> index<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">==</span> <span style="color: #0000dd;"></span> <span style="color: #009900;">&#41;</span>
		<span style="color: #009900;">&#123;</span>
			<span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
		<span style="color: #009900;">&#125;</span>
		<a href="http://www.opengroup.org/onlinepubs/009695399/functions/printf.html"><span style="color: #000066;">printf</span></a><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"%d<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">,</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span>index<span style="color: #339933;">+</span>i<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
&nbsp;
	gettimeofday<span style="color: #009900;">&#40;</span><span style="color: #339933;">&</span>amp<span style="color: #339933;">;</span>finish<span style="color: #339933;">,</span> NULL<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
	duration <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>finish.<span style="color: #202020;">tv_sec</span><span style="color: #339933;">-</span>start.<span style="color: #202020;">tv_sec</span><span style="color: #009900;">&#41;</span>
		<span style="color: #339933;">+</span> <span style="color: #009900;">&#40;</span>finish.<span style="color: #202020;">tv_usec</span> <span style="color: #339933;">-</span> start.<span style="color: #202020;">tv_usec</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">/</span> <span style="color: #009900;">&#40;</span><span style="color:#800080;">1000000.1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<a href="http://www.opengroup.org/onlinepubs/009695399/functions/printf.html"><span style="color: #000066;">printf</span></a><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"Done, %f seconds<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">,</span> duration<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #b1b100;">return</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>
