---
title: Bash的if使用和参数介绍
layout: post
categories:
  - communication
tags:
  - bash
---

Bash的If基本使用语法

**if 与 [ 之间有空格， [ 和 conditiong 和 ]之间有空格**

<div class="wp_codebox">
  <table>
    <tr id="p1052124">
      <td class="code" id="p1052code124">
        <pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> condition <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span>
&nbsp;
    operate <span style="color: #000000;">1</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">elif</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> condition <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span>
&nbsp;
    operate <span style="color: #000000;">2</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">else</span>
&nbsp;
    operate <span style="color: #000000;">3</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">fi</span></pre>
      </td>
    </tr>
  </table>
</div>

<div class="wp_codebox">
  <table>
    <tr id="p1052125">
      <td class="code" id="p1052code125">
        <pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">test</span> condition; <span style="color: #000000; font-weight: bold;">then</span>
&nbsp;
    operate <span style="color: #000000;">1</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">elif</span> <span style="color: #7a0874; font-weight: bold;">test</span> condition; <span style="color: #000000; font-weight: bold;">then</span>
&nbsp;
    operate <span style="color: #000000;">2</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">else</span>
&nbsp;
    operate <span style="color: #000000;">3</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">fi</span></pre>
      </td>
    </tr>
  </table>
</div>

&nbsp;

&nbsp;

<table border="0" cellspacing="0" cellpadding="3">
  <tr valign="top" bgcolor="#0033cc">
    <td>
      <strong>运算符</strong>
    </td>
    
    <td>
      <strong>描述</strong>
    </td>
    
    <td>
      <strong>示例</strong>
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#888888">
    <td colspan="3">
      <strong>文件比较运算符 </strong>
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -e <em>filename</em>
    </td>
    
    <td>
      如果 <em>filename</em>存在，则为真
    </td>
    
    <td>
      [ -e /var/log/syslog ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -d <em>filename</em>
    </td>
    
    <td>
      如果 <em>filename</em>为目录，则为真
    </td>
    
    <td>
      [ -d /tmp/mydir ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -f <em>filename</em>
    </td>
    
    <td>
      如果 <em>filename</em>为常规文件，则为真
    </td>
    
    <td>
      [ -f /usr/bin/grep ]
    </td>
  </tr>
  
  <p>
    /tr>
  </p>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -s <em>filename</em>
    </td>
    
    <td>
      如果 <em>filename</em>存在且不为空，则为真
    </td>
    
    <td>
      [ -s /usr/bin/grep ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -L <em>filename</em>
    </td>
    
    <td>
      如果 <em>filename</em>为符号链接，则为真
    </td>
    
    <td>
      [ -L /usr/bin/grep ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -r <em>filename</em>
    </td>
    
    <td>
      如果 <em>filename</em>可读，则为真
    </td>
    
    <td>
      [ -r /var/log/syslog ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -w <em>filename</em>
    </td>
    
    <td>
      如果 <em>filename</em>可写，则为真
    </td>
    
    <td>
      [ -w /var/mytmp.txt ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -x <em>filename</em>
    </td>
    
    <td>
      如果 <em>filename</em>可执行，则为真
    </td>
    
    <td>
      [ -L /usr/bin/grep ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>filename1</em>-nt <em>filename2</em>
    </td>
    
    <td>
      如果 <em>filename1</em>比 <em>filename2</em>新，则为真
    </td>
    
    <td>
      [ /tmp/install/etc/services -nt /etc/services ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>filename1</em>-ot <em>filename2</em>
    </td>
    
    <td>
      如果 <em>filename1</em>比 <em>filename2</em>旧，则为真
    </td>
    
    <td>
      [ /boot/bzImage -ot arch/i386/boot/bzImage ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#888888">
    <td colspan="3">
      <strong>字符串比较运算符 </strong>（请注意引号的使用，这是防止空格扰乱代码的好方法）
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -z <em>string</em>
    </td>
    
    <td>
      如果 <em>string</em>长度为零，则为真
    </td>
    
    <td>
      [ -z "$myvar" ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      -n <em>string</em>
    </td>
    
    <td>
      如果 <em>string</em>长度非零，则为真
    </td>
    
    <td>
      [ -n "$myvar" ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>string1</em>= <em>string2</em>
    </td>
    
    <td>
      如果 <em>string1</em>与 <em>string2</em>相同，则为真
    </td>
    
    <td>
      [ "$myvar" = "one two three" ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>string1</em>!= <em>string2</em>
    </td>
    
    <td>
      如果 <em>string1</em>与 <em>string2</em>不同，则为真
    </td>
    
    <td>
      [ "$myvar" != "one two three" ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#888888">
    <td colspan="3">
      <strong>算术比较运算符 </strong>
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>num1</em>-eq <em>num2</em>
    </td>
    
    <td>
      等于
    </td>
    
    <td>
      [ 3 -eq $mynum ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>num1</em>-ne <em>num2</em>
    </td>
    
    <td>
      不等于
    </td>
    
    <td>
      [ 3 -ne $mynum ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>num1</em>-lt <em>num2</em>
    </td>
    
    <td>
      小于
    </td>
    
    <td>
      [ 3 -lt $mynum ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>num1</em>-le <em>num2</em>
    </td>
    
    <td>
      小于或等于
    </td>
    
    <td>
      [ 3 -le $mynum ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>num1</em>-gt <em>num2</em>
    </td>
    
    <td>
      大于
    </td>
    
    <td>
      [ 3 -gt $mynum ]
    </td>
  </tr>
  
  <tr valign="top" bgcolor="#eeeeee">
    <td>
      <em>num1</em>-ge <em>num2</em>
    </td>
    
    <td>
      大于或等于
    </td>
    
    <td>
      [ 3 -ge $mynum ]
    </td>
  </tr>
</table>

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

转直：http://blog.csdn.net/yuanchao3333/archive/2009/07/24/4376816.aspx
