---
title: C中计算数组的长度
author: 悟道
layout: post
categories:
  - C
  - 转载
tags:
  - C
---

C<span>、C++中没有提供直接获取数组长度的函数，对于存放字符串的字符数组提供了一个strlen函数获取长度，那么对于其他类型的数组如何获取他们的长度呢？其中一种方法是使用sizeof(array) / sizeof(array[0]),</span> <span>在C语言中习惯上在</span> <span>使用时都把它定义成一个宏，比如#define GET_ARRAY_LEN(array,len) {len = (sizeof(array) / sizeof(array[0]));}</span> <span>。而在C++中则可以使用模板技术定义一个函数，比如：</span>

template <class T>

int getArrayLen(T& array)

{

return (sizeof(array) / sizeof(array[0]));

}

<span>这样对于不同类型的数组都可以使用这个宏或者这个函数来获取数组的长度了。以下是两个Demo程序，一个C语言的，一个C++的：</span>

P.S<span>：若数组为存储字符串的字符数组，则所求得的长度还需要减一，即对于宏定义：</span> #define GET\_ARRAY\_LEN(array,len) {len = (sizeof(array) / sizeof(array[0]) &#8211; 1 );} <span>，对于函数定义：</span>

template <class T>

int getArrayLen(T& array)

{

return (sizeof(array) / sizeof(array[0]) &#8211; 1);

}

<span>原因为存储字符串的字符数组末尾有一个&#8217;\0&#8242;字符，需要去掉它。</span>

<span>【C语言】</span>

#include <stdio.h>

#include <stdlib.h>

#define GET\_ARRAY\_LEN(array,len){len = (sizeof(array) / sizeof(array[0]));}

//<span>定义一个带参数的宏，将数组长度存储在变量len中</span>

int main()

{

char a[] = {&#8217;1&#8242;,&#8217;2&#8242;,&#8217;3&#8242;,&#8217;4&#8242;};

int len;

GET\_ARRAY\_LEN(a,len)

//<span>调用预定义的宏，取得数组a的长度，并将其存储在变量len中</span>

printf(&#8220;%d\n&#8221;,len);

system(&#8220;pause&#8221;);

return 0;

}

<span>【C++】</span>

#include <iostream>

using namespace std;

template <class T>

int getArrayLen(T& array)

{//<span>使用模板定义一个函数getArrayLen,该函数将返回数组array的长度</span>

return (sizeof(array) / sizeof(array[0]));

}

int main()

{

char a[] = {&#8217;1&#8242;,&#8217;2&#8242;,&#8217;3&#8242;};

cout << getArrayLen(a) << endl;

return 0;

}

引用地址：http://hi.baidu.com/aleczhou/blog/item/4addd1881df0b691a5c27209.html
