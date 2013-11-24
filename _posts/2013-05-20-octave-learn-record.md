---
title: Octave学习记录
author: 悟道
layout: post
categories:
  - octave
tags:
  - octave
---

1.Basic operations

<pre class="brush: bash; title: ; notranslate" title="">%generate a matrix
a = [1,2,3;4,5,6]
a =

   1   2   3
   4   5   6

a = [1,2,3;4,5,6]; % The end ';' will inhibit the output of assignment operation

%generate a vaector

a = [1 2 3];

a = [1:3];

%specific matrix or vectors

ones(3,1)
zeros(0,1)

a = ones(3,1);
a(1) = 0;
a 

%change or add one row or one column of a matrix

octave:33&gt; a = [1 2 3];
octave:34&gt; a = [a;a]
a =

   1   2   3
   1   2   3

octave:35&gt; a = [a a]
a =

   1   2   3   1   2   3
   1   2   3   1   2   3

octave:36&gt; a = [a a ones(2,1)]
a =

   1   2   3   1   2   3   1   2   3   1   2   3   1
   1   2   3   1   2   3   1   2   3   1   2   3   1

octave:37&gt; a = [a ; ones(1,size(a,2))]
a =

   1   2   3   1   2   3   1   2   3   1   2   3   1
   1   2   3   1   2   3   1   2   3   1   2   3   1
   1   1   1   1   1   1   1   1   1   1   1   1   1

octave:38&gt; a[1,]
parse error:

  syntax error

&gt;&gt;&gt; a[1,]
     ^

octave:38&gt; a[1,:] = zeros(1,size(a,2))
parse error:

  syntax error

&gt;&gt;&gt; a[1,:] = zeros(1,size(a,2))
     ^

octave:38&gt; a(1,:) = zeros(1,size(a,2))
a =

   0   0   0   0   0   0   0   0   0   0   0   0   0
   1   2   3   1   2   3   1   2   3   1   2   3   1
   1   1   1   1   1   1   1   1   1   1   1   1   1

octave:39&gt; a(:,1) = ones(size(a,1),1)
a =

   1   0   0   0   0   0   0   0   0   0   0   0   0
   1   2   3   1   2   3   1   2   3   1   2   3   1
   1   1   1   1   1   1   1   1   1   1   1   1   1


</pre>

2.Get the maximum value from a matrix

<pre class="brush: bash; title: ; notranslate" title="">octave:12&gt; a = [1,2,3;4,5,6;7,8,9]
a =

   1   2   3
   4   5   6
   7   8   9

octave:13&gt; max(a) #default by columns
ans =

   7   8   9

octave:14&gt; [value, index] = max(a) #return the largest value of each column and their rows
value =

   7   8   9

index =

   3   3   3

</pre>

3.Get unique values of a vector

<pre class="brush: bash; title: ; notranslate" title="">octave:23&gt; a = [1 2 3 4 5 1 2 3 4 5 1 2 3 4 5]
a =

   1   2   3   4   5   1   2   3   4   5   1   2   3   4   5

octave:24&gt; unique(a)
ans =

   1   2   3   4   5

</pre>

4.Get the number of rows and columns of a mtrix

<pre class="brush: bash; title: ; notranslate" title="">octave:27&gt; a = [1 2 3 4 5; 1 2 3 4 5 ;1 2 3 4 5]
a =

   1   2   3   4   5
   1   2   3   4   5
   1   2   3   4   5

octave:28&gt; size(a)
ans =

   3   5

octave:29&gt; size(a,1) % number of rows
ans =  3
octave:30&gt; size(a,2) % number of columns
ans =  5
octave:31&gt; a = [1 2 3 4 5 1 2 3 4 5 1 2 3 4 5]
a =

   1   2   3   4   5   1   2   3   4   5   1   2   3   4   5

octave:32&gt; size(a)
ans =

    1   15

</pre>

5.Get the position of one special value or change one special value to 0

<pre class="brush: bash; title: ; notranslate" title="">octave:48&gt; a = [ones(5,1);zeros(5,1)];
octave:49&gt; pos_a = find(a==1)
pos_a =

   1
   2
   3
   4
   5

octave:50&gt; a(pos_a,:)
ans =

   1
   1
   1
   1
   1

octave:51&gt; zero_a = find(a==0)
zero_a =

    6
    7
    8
    9
   10

octave:52&gt; a(zero_a,:)
ans =

   0
   0
   0
   0
   0

%------------------------------------------
octave:53&gt; a = [1,2,3,4,5,1,2,3,4,5]
a =

   1   2   3   4   5   1   2   3   4   5

octave:54&gt; a == 1
ans =

   1   0   0   0   0   1   0   0   0   0

octave:55&gt; a == 5
ans =

   0   0   0   0   1   0   0   0   0   1

</pre>

6.repmat &#8212; repeat a given matrix by given number of times in row and column

<pre class="brush: bash; title: ; notranslate" title="">octave:24&gt; a = ones(3,4)
a =

   1   1   1   1
   1   1   1   1
   1   1   1   1

octave:25&gt; repmat(a,1,2)
ans =

   1   1   1   1   1   1   1   1
   1   1   1   1   1   1   1   1
   1   1   1   1   1   1   1   1

octave:26&gt; repmat(a,2,2)
ans =

   1   1   1   1   1   1   1   1
   1   1   1   1   1   1   1   1
   1   1   1   1   1   1   1   1
   1   1   1   1   1   1   1   1
   1   1   1   1   1   1   1   1
   1   1   1   1   1   1   1   1
</pre>

7.

8.  
9.
