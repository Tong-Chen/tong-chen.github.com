---
title: ANSI C使用getline和getdelim读取一行
author: 悟道
layout: post
permalink: /?p=860
categories:
  - C
tags:
  - C
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<div class="wp_codebox">
  <table>
    <tr id="p86069">
      <td class="code" id="p860code69">
        <pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include &lt;stdio.h&gt;</span>
ssize_t getline<span style="color: #009900;">&#40;</span><span style="color: #993333;">char</span> <span style="color: #339933;">**</span>lineptr<span style="color: #339933;">,</span> size_t <span style="color: #339933;">*</span>n<span style="color: #339933;">,</span> FILE <span style="color: #339933;">*</span>stream<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
ssize_t getdelim<span style="color: #009900;">&#40;</span><span style="color: #993333;">char</span> <span style="color: #339933;">**</span>lineptr<span style="color: #339933;">,</span> size_t <span style="color: #339933;">*</span>n<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> delim<span style="color: #339933;">,</span> FILE <span style="color: #339933;">*</span>stream<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

**getline**

**The getline function is the preferred method for reading lines of text from a stream, including standard input.** The other standard functions, including **gets**, **fgets**, and **scanf**, are too unreliable. (Doubtless, in some programs you will see code that uses these unreliable functions, and at times you will come across compilers that cannot handle the safer getline function. As a professional, you should avoid unreliable functions and any compiler that requires you to be unsafe.)

The *getline* function reads **an entire line from a stream, up to and including the next newline character. **It takes three parameters. The first is a **pointer to a block allocated with malloc or calloc**. (These two functions allocate computer memory for the program when it is run. See Memory allocation, for more information.) This parameter is of type **char ****; it will contain the line read by *getline* when it returns. The second parameter is **a pointer to a variable of type size_t**; this parameter specifies the size in bytes of the block of memory pointed to by the first parameter. The third parameter is simply the stream from which to read the line.

The pointer to the block of memory allocated for *getline* is merely a suggestion. The *getline* function will automatically enlarge the block of memory as needed, via the *realloc* function, so there is never a shortage of space &#8212; one reason why *getline* is so safe. Not only that, but *getline* will also tell you the new size of the block by the value returned in the second parameter.

If an error occurs, such as end of file being reached without reading any bytes, *getline* returns **-1**. Otherwise, the first parameter will contain a pointer to the string containing the line that was read, and *getline* returns the number of characters read (up to and including the newline, but not the final null character). The return value is of type **ssize_t**.

**Although the second parameter is of type pointer to string (char **), you cannot treat it as an ordinary string, since it may contain null characters before the final null character marking the end of the line**. The return value enables you to distinguish null characters that *getline* read as part of the line, by specifying the size of the line. Any characters in the block up to the number of bytes specified by the return value are part of the line; any characters after that number of bytes are not.

Here is a short code example that demonstrates how to use* getline* to read a line of text from the keyboard safely. Try typing more than 100 characters. Notice that *getline* can safely handle your line of input, no matter how long it is. Also note that the puts command used to display the line of text read will be inadequate if the line contains any null characters, since it will stop displaying text at the first null, but that since it is difficult to enter null characters from the keyboard, this is generally not a consideration. 

**getdelim**

The getdelim function is a more general form of the getline function; whereas getline stops reading input at the first newline character it encounters, the getdelim function enables you to specify other delimiter characters than newline. In fact, getline simply calls getdelim and specifies that the delimiter character is a newline.

The syntax for getdelim is nearly the same as that of getline, except that the third parameter specifies the delimiter character, and the fourth parameter is the stream from which to read. You can exactly duplicate the getline example in the last section with getdelim, by replacing the line

<div class="wp_codebox">
  <table>
    <tr id="p86070">
      <td class="code" id="p860code70">
        <pre class="c" style="font-family:monospace;">bytes_read <span style="color: #339933;">=</span> getline <span style="color: #009900;">&#40;</span><span style="color: #339933;">&</span>my_string<span style="color: #339933;">,</span> <span style="color: #339933;">&</span>nbytes<span style="color: #339933;">,</span> stdin<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

with the line

<div class="wp_codebox">
  <table>
    <tr id="p86071">
      <td class="code" id="p860code71">
        <pre class="c" style="font-family:monospace;">bytes_read <span style="color: #339933;">=</span> getdelim <span style="color: #009900;">&#40;</span><span style="color: #339933;">&</span>my_string<span style="color: #339933;">,</span> <span style="color: #339933;">&</span>nbytes<span style="color: #339933;">,</span> <span style="color: #ff0000;">'<span style="color: #000099; font-weight: bold;">\n</span>'</span><span style="color: #339933;">,</span> stdin<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

<div class="wp_codebox">
  <table>
    <tr id="p86072">
      <td class="line_numbers">
        <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
</pre>
      </td>
      
      <td class="code" id="p860code72">
        <pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include &lt;stdio.h&gt;</span>
<span style="color: #339933;">#include &lt;stdlib.h&gt;</span>
&nbsp;
<span style="color: #993333;">int</span> main<span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span> argc<span style="color: #339933;">,</span> <span style="color: #993333;">char</span> <span style="color: #339933;">*</span>argv<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
	<span style="color: #993333;">int</span> bytes_read<span style="color: #339933;">;</span>
	<span style="color: #993333;">int</span> nbytes <span style="color: #339933;">=</span> <span style="color: #0000dd;">10</span><span style="color: #339933;">;</span>
	<span style="color: #666666; font-style: italic;">//char *my_string;</span>
&nbsp;
&nbsp;
&nbsp;
	<span style="color: #666666; font-style: italic;">//my_string = (char *)malloc(nbytes+1);</span>
        <span style="color: #993333;">char</span> <span style="color: #339933;">*</span>my_string <span style="color: #339933;">=</span> NULL<span style="color: #339933;">;</span>
        puts<span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"Please enter a line of text."</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	bytes_read <span style="color: #339933;">=</span> getline<span style="color: #009900;">&#40;</span> <span style="color: #339933;">&</span>my_string<span style="color: #339933;">,</span> <span style="color: #339933;">&</span>nbytes<span style="color: #339933;">,</span> stdin<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
	<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> bytes_read <span style="color: #339933;">==</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		puts<span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"Error"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span><span style="color: #b1b100;">else</span>
	<span style="color: #009900;">&#123;</span>
		puts<span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"You typed:"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
		puts<span style="color: #009900;">&#40;</span>my_string<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
		<a href="http://www.opengroup.org/onlinepubs/009695399/functions/printf.html"><span style="color: #000066;">printf</span></a><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"%d<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">,</span>nbytes<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
	puts<span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"Please enter a line of text."</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	bytes_read <span style="color: #339933;">=</span> getdelim<span style="color: #009900;">&#40;</span><span style="color: #339933;">&</span>my_string<span style="color: #339933;">,</span> <span style="color: #339933;">&</span>nbytes<span style="color: #339933;">,</span> <span style="color: #ff0000;">':'</span><span style="color: #339933;">,</span> stdin<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> bytes_read <span style="color: #339933;">==</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span> <span style="color: #009900;">&#41;</span>
	<span style="color: #009900;">&#123;</span>
		puts<span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"Error"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span><span style="color: #b1b100;">else</span>
	<span style="color: #009900;">&#123;</span>
		puts<span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"You typed:"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
		puts<span style="color: #009900;">&#40;</span>my_string<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
		<a href="http://www.opengroup.org/onlinepubs/009695399/functions/printf.html"><span style="color: #000066;">printf</span></a><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"%d<span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #339933;">,</span>nbytes<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
	<span style="color: #009900;">&#125;</span>
&nbsp;
	<span style="color: #b1b100;">return</span> <span style="color: #0000dd;"></span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

原帖：<http://www.crasseux.com/books/ctutorial/getline.html>