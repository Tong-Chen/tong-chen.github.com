---
title: Tips for BASH usage
layout: post
categories:
  - bash
  - letter
tags:
  - awk
  - bash
  - perl
  - sed
---

#############################################################################  
由于高开始使用的高亮工具wp-code在“可视化”和“文本”两个模式下切换操作时会发生字符的转移问。  
现在更换了新的语法高亮工具，因此可能存在部分html字符或引号使用不当的地方，正在着力修改，也请读者发现后指出。  
#############################################################################  
这篇日志记录使用到的快捷bash，sed，awk脚本。

Bash篇

1.输出指定行(第k行，包括k行)及其后面所有行，用于去除文件头

{% highlight vim %}
tail -n +k filename
{% endhighlight %}

2.

3.拷贝一个文件到当前目录的所有子目录(可以使用-maxdepth指定子文件级数)

{% highlight vim %}
find . -type d -exec cp ./file {}/ \;

for dir in $(find . -type d); do rm -f "$dir/file" ; done
{% endhighlight %}

4.修改多个目录下的同一个文件

{% highlight vim %}
find . -name README -exec sed -i 's/pat/sub/g {} \;
{% endhighlight %}

5.bash script中使用$符号，需加反斜线(\)转义

6.求文件所有数值的最小值（两条语句细微的差别，第二个更保险）

{% highlight vim %}
cat file | tr -s  ''[:blank:]" "\n" | sort -n | sed -n '1p;$p'

tr -s "[:blank:]" "\n" <file | sort -n | sed '/^$/d' | sed -n '1p;$p'
{% endhighlight %}

7.从文件中取出随机行或文件夹中取出随机文件

{% highlight vim %}
shuf -n num filename   #取出num行

ls dir | shuf -n num #取出num个随机文件

ls dir | shuf #随机重拍所有文件
{% endhighlight %}

8.删除指定大小的文件

{% highlight vim %}
find . -size 28c -exec /bin/rm -f {} \;

find . -size +28k -delete  删除大于28k的文件
{% endhighlight %}

9.查看当前目录下文件的个数（包含隐藏文件）

{% highlight vim %}
ls -al | grep -c '^-'

find . -maxdepth 1 -type f -print | wc -l
{% endhighlight %}

10.大小写转换

{% highlight vim %}
cat file.txt | tr 'a-z' 'A-Z'

tr 'a-z' 'A-Z'  'small'

declare -l m="HELLO"

echo $m   (output>:hello)

declare -u m

echo $m  (output>:hello)

m='cde'

echo $m  (output>:CDE)
{% endhighlight %}

11.bash一行行读取文件

{% highlight vim %}
#!/bin/bash

OLDIFS=$IFS

IFS=$'\n'

SOURCE-sth.txt

LINES=$(ca $SOURCE)

for LINE in $LINES; do

echo $LINE

done

IFS=$OLDIFS
{% endhighlight %}

12.sort多列排序

{% highlight vim %}
sort -k1,1 -k2,2n testsort （特殊的第二列为数字）
{% endhighlight %}

13.bash数组操作，索引版

{% highlight vim %}
declare -a a;

#a=`ls`; #not work very well

#first choice

j=0;

for i in `ls | grep 'DE$' | grep '-'`; do

a[$j]=$i; j=`expr $j + 1`; done

#expr $j + 1  not expr $j+1, pay attention to the space

#second choice

ls | grep 'DE$' | grep '-' >tmp

read -a a <tmp

/bin/rm -f tmp

##################

echo $a # only shows the first element

echo ${a[@]} #show all elements, so does ${a[*]}

##################3

length=${#a[@]};

for((i=0;i<$[${length}-1]; i++)); do

for((j=$[$i+1];j<${length};j++)); do

if [ $i -eq 0 ]; then pre=`echo ${a[i]} | cut -d ' ' -f 1`;

echo -n $pre; echo -n ' '; echo ${a[j]};

else echo -n ${a[i]}; echo -n ' '; echo ${a[j]};fi;

done; done
{% endhighlight %}

14.bash数据同步

{% highlight vim %}
rsync -vazuL –delete /project user@server:/project/

#-L treat symbolic link as the dir/file linked
{% endhighlight %}

15.时间函数

{% highlight vim %}
date

date '+%Y-%m-%d %H:%M:%S'


{% endhighlight %}

16.显示自己的进程

{% highlight vim %}
ps u  #返回当前终端运行的程序及其所有登录终端(-bash)

ps ux #返回所有终端的程序

ps uxr #只返回运行中的程序

ps aux | grep 'user' #让程序描述折行显示
{% endhighlight %}

17.杀掉一个用户的进程

{% highlight vim %}
killall -u user
{% endhighlight %}

18.bash下diff比较标准输入的重定向

{% highlight vim %}
diff <(sort file1)  <(sort file2)

bash -c 'diff <(sort file1)  <(sort file2)'

#To specify using bash command if you meets an error
#when working on other types of term.
{% endhighlight %}

19.paste, cut, join, split

{% highlight vim %}
paste 把多个文件的列粘帖在一起构成一个新文件

join 按指定的列作为key来粘帖

split -l 200 file  #把文件分为2000行的小文件
{% endhighlight %}

20.expand, unexpand

{% highlight vim %}
expand把tab转换为空格

unexpand把空格转换为tab
{% endhighlight %}

21.计算文件中最长行的长度

{% highlight vim %}
wc -L file
{% endhighlight %}

22.join使用，[参考][1] **使用join前确保已按第一列排好序sort -k1,1,而不是sort. 第一行如果有标题，应去掉。**

{% highlight vim %}
join file1 file2  #内连接，关键字不匹配的行不输出

join -a1 file1 file2 #左连接，显示左边文件中所有记录，右边文件中没有匹配的显示空白

join -a2 file1 file2 #右连接，显示右边文件中所有记录，左边文件中没有匹配的显示空白

join -a1 -a2 file1 file2 #全连接，显示所有未匹配的项

join -o 1.1 file1 file2 #只输出第一个文件的第一个字段

join -o 1.1,2.2 file2 file2 #只输出第一个文件第一字段和第二个文件的第二个字段

join -o 1.1,2.2,1.2 file1 file2
{% endhighlight %}

23.bash从标准输入读取信息

{% highlight vim %}
read -p "how old r u? " age

echo $age

read -p ”some words? “ -a words

echo ${words[*]}

read -p “Password: ” -s passwd

echo $passwd

read -t 5 auth

echo $auth

read -n 1 key

read -dq -p “input something end with q: ” menu

read -e file #在这试试命令历史和补齐功能
{% endhighlight %}

24.删除一个用户的全部进程

{% highlight vim %}
killall -u username
{% endhighlight %}

24.删除包含某一特定的程序的所有进程

{% highlight vim %}
killall -e progNamw
{% endhighlight %}

25.bash中while循环

{% highlight vim %}
while [ condition ]

do

command1 command2 command3

done
{% endhighlight %}

26.window文件^M转换为linux格式

{% highlight vim %}
sed -i 's/^M//' file.ok
perl -p -i -e "s/^M//g" `find .`

^M的输入时ctrl+v+M  ctrl+v;ctrl+m


{% endhighlight %}

27.wc -l的误差

{% highlight vim %}
wc -l只能给出文件中换行符的个数，而不一定是行数，特例是最后一行没有换行符时。

wc -L返回最长行的字符数
{% endhighlight %}

28.touch修改时间戳

{% highlight vim %}
touch -t [[CC]YY]MMDDhhmm[.ss]
{% endhighlight %}

29.bash数学运算<http://blog.chinaunix.net/space.php?uid=20609878&do=blog&id=1915813>

{% highlight vim %}
echo $[1+3]

echo "10/3" | bc -l

echo $(( 1+3 ))

用于脚本时declare -i
{% endhighlight %}

30.uniq指定忽略的列或字符，配合awk使用，把不需要比较的列放到前面

{% highlight vim %}
uniq -f 1   #跳过第一列

uniq -s 10  #跳过前十个字符
{% endhighlight %}

31.统计字符出现个数

{% highlight vim %}
grep -o 'h' file | wc -l
{% endhighlight %}

32.在终端向其它用户发送信息<http://blog.csdn.net/knock/article/details/4801360> 发送的信息会插入你正在编辑的文本，造成混乱。

{% highlight vim %}
1.用w命令查看都有哪些中断用户

[]#w

jeff     pts/5    192.168.96.128   16:47   10:44   0.03s  0.03s -bash

2.发送消息

[]#write jeff pts/5

hello!

接下来每写一行，按回车后就会发送到对方相应的终端。

广播消息

echo "hello,This is a message" | wall
33.paste用法，-s表示每个文件一行行处理，其实是做了一个转置。
1     $ cat num2

1

2

$ cat let3

a

b

c

$ paste num2 let3

1       a

2       b

c

$ paste -s num2 let3

1       2

a       b       c

bash下文件转置，假设有一个文件内容是

$cat a  [tab分割]

1 a

2 b

3 c

$paste -s <(cut -f 1 a) <(cut -f 2 a)

1 2 3

a b c
{% endhighlight %}

34.sort排序，保留标题行http://forums.devshed.com/unix-help-35/sort-excluding-first-line-heading-line-183574.html

{% highlight vim %}
(  head -1 ${in:=dummy.txt} ; tail +2 $in | sort -u  ) >  sort_$in
在vi中使用
:2,$!sort -u

{% endhighlight %}

35.grep匹配tab

{% highlight vim %}
grep -P '\t'

grep [[:space:]] // 所有空白字符

直接grep tab字符 // 命令行下用"ESC TAB"输入

grep $'\t'

</div>
{% endhighlight %}

36.for循环中使用后台运行【Both & and ; are line terminators, only one is enough.】

<http://ubuntuforums.org/showthread.php?t=504030>

{% highlight vim %}
for i in *.data; do nohup \
    awk 'BEGIN{OFS="\t"}{if(match($0, /^fixed/)) {split($0,  array,  " "); \
    chr=substr(array[2],7); start=substr(array[3], 7); step=substr(array[4],6); } \
    else {end=start+step; print chr, start, end, $0; start=end} }' $i >$i.bed & done
{% endhighlight %}

37.输出当前运行的bash文件所在目录

{% highlight vim %}
`dirname $0`
{% endhighlight %}

38.得到linux下命令的地址和判断某个命令是否存在

{% highlight vim %}
type cmd  ----------python is /home/username/soft/Python-2.6.7/bin/python

which cmd---------~/soft/Python-2.6.7/bin/python

if ! which python; then

echo "Could not find python"

fi

if [ ! -x dir/python ]; then

echo "Could not find python"

fi

if ! python --version >/dev/null 2>&1; then

echo "Could not find python"

fi
{% endhighlight %}

39.排序大文件，先拆分再排序

{% highlight vim %}
split -l 300 bigfile

sort bigfile.aa > bigfile.aa.sort

sort -m *.sort

#使用大内存
sort -S 5G bifile  #K,M,G,P 1%

{% endhighlight %}

40.bash中输出从1到n的数

{% highlight vim %}
seq 1 n

$(echo `seq 0 0.05 1` | sed 's/ /,/g') #产生一些列的数值作为传入参数
{% endhighlight %}

41.bash中统计所有文件的大小

{% highlight vim %}
find folder -type f -printf "%s+" | sed 's/+$/\n/' | bc

{% endhighlight %}

42.wait的使用

{% highlight vim %}
#!/bin/bash

for i in `seq 1 5`; do

sleep $i && echo $i &

done

wait

echo "Finish"

-------------Output---------------------

1

2

3

4

5

Finish

{% endhighlight %}

管道（|）会开启一个新的shell，在同时使用wait时要格外注意（把wait和想wait的东西括在一起）。【http://stackoverflow.com/questions/6041708/bash-subshells-and-waiting-for-subprocesses-to-finish 】【http://stackoverflow.com/questions/2259867/bash-threading-wait-for-all-job-threads-to-finish-doesnt-work】

&#8212;&#8212;&#8212;&#8212;&#8212;-wrong&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

{% highlight vim %}
find /home/some/path -type f | while read filename ; do
     echo "Creating archive of $filename"
     func $somevariable & done
wait
-------------------right-----------------------------------
find /home/some/path -type f | (while read filename ; do
     echo "Creating archive of $filename"
     func $somevariable &   done
wait )

{% endhighlight %}

43.找更新的文件

{% highlight vim %}
find -anewer file
{% endhighlight %}

44.批量修改软链接

{% highlight vim %}
ls -l | grep -P '^l' | awk 'BEGIN{OFS="\t"}{if($11~/^\/home\/CT/) \
    {gsub("/home","/oldhome",$11)}; if($11~/^\/media\//){gsub("/media","\~",$11)}; print "ln -sf ",$11,$9}' \
    >updateSOftLink.sh bash updateSOftLink.sh
{% endhighlight %}

45.批量删除断了的软连接 (search for and remove dead symbolic link)

{% highlight vim %}
find . -type l -print | xargs -r file | grep 'broken symbolic' | cut -d ":“ -f 1
{% endhighlight %}

46.配置登录终端类型 [不添加--login不回读取.bash_profile]

{% highlight vim %}
如果当前是csh or tcsh

cat <<END >~/.login

exec bash --login

END

如果当前是sh或ksh

cat<<END >~/.profile

exec bash --login
#[ -f /usr/gnu/bin/bash ] && exec /usr/gnu/bin/bash --login
END

echo $SHELL

相关参考见：

http://www.unixguide.net/unix/bash/A7.shtml
{% endhighlight %}

47.在bash 脚本中，subshells (写在圆括号里的) 是一个很方便的方式来组合一些命令。一个常用的例子是临时地到另一个目录中，例如：

{% highlight vim %}
# do something in current dir
(cd /some/other/dir; other-command)
# continue in original dir

{% endhighlight %}

在 bash 中，注意那里有很多的变量展开。如：检查一个变量是否存在: ${name:?error message}。  
如果一个bash的脚本需要一个参数，也许就是这样一个表达式 input\_file=${1:?usage: $0 input\_file}。  
一个计算表达式： i=$(( (i + 1) % 5 ))。一个序列： {1..10}。  
截断一个字符串： ${var%suffix} 和 ${var#prefix}。  
示例： if var=foo.pdf, then echo ${var%.pdf}.txt prints “foo.txt”.

48.find使用

{% highlight vim %}
#-exec is the same as -ok, except that -ok needs you type yes to make sure

#{} represents the things you find by given conditions

#\; is mandatory

find . -name *.tdf -exec ln -s {} . \;

find . -name *.tdf -ok ln -s {} \;

#fast delete files
find . -type f -delete -print
find . -type d -delete -print

{% endhighlight %}

49.bash命令的重用

{% highlight vim %}
1.!$是一个特殊的环境变量，它代表了上一个命令的最后一个字符串。
2.!!表示上一个命令
3.！vim 表示最近一条以vim开头的命令
4.!!:gs/old_name/new_name   #把上一条命令中的old_name全部替换为new_name
!cd:gs/old_name/new_name    #把最近一条以cd开头的命令中的old_name全部替换为new_name
5.^old^new  #把上一条命令中的第一个old替换为new
6.在 bash 里，使用 Ctrl-R 而不是上下光标键来查找历史命令。
7.在 bash里，使用 Ctrl-W 来删除最后一个单词，使用 Ctrl-U 来删除一行
8.Alt-. 把上一次命令的最后一个参数打出来，而Alt-* 则列出你可以输入的命令
9.man bash后查找Readline Key Bindings一节来看看bash的默认热键
10.CTRL+R 快速查找包含特定字符的命令

{% endhighlight %}

50.delete files with hypen or dash or search dash(-) in a file

{% highlight vim %}
# -file
rm ./-file
rm -- -file
# --testings.html
rm -- --testings.html
grep -- '-[a-zA-Z]' file

{% endhighlight %}

51.Promot a hint, when * appears in command line

{% highlight vim %}
shopt -s extdebug
check_for_rm_star() {
  case $1 in
    (rm*[\ /]"* "* | rm*[\ /]\*)  #you can change rm to other commands
      read -p "check_for_rm_star: Are you sure this is the right directory? " -n1 answer < /dev/tty > /dev/tty
      echo > /dev/tty
      [[ $answer == [yY] ]]
  esac
}
trap 'check_for_rm_star "$BASH_COMMAND"' DEBUG

{% endhighlight %}

52.Getting colored results when using a pipe from grep or ls to less

{% highlight vim %}
grep --color=always 'sth' file | less -R
ls --color=always | less -R

{% endhighlight %}

53.bash for loop

{% highlight vim %}
#------------------------------------------
for ((i=0;i<10;i++)); do
    echo $i
done

#------------------------------------------
for i in {0..9}
  do
    echo $i
done

#------------------------------------------
for i in `seq 10`
do
    echo "the i is $i"
done

#------------------------------------------
i=1
for day in Mon Tue Wed Thu Fri
#<"Mon Tue Wed Thu Fri"> and <Mon, Tue, Wed, Thu, Fri> are unsuitable

do
 echo "Weekday $((i++)) : $day"
done

#------------------------------------------
i=1
weekdays="Mon Tue Wed Thu Fri"
for day in $weekdays
#Do not double quote <$weekdays> like "$weekdays" here
do
 echo "Weekday $((i++)) : $day"
done

#------------------------------------------
i=1
for username in `awk -F: '{print $1}' /etc/passwd`
do
 echo "Username $((i++)) : $username"
done
#------------------------------------------
i=1
cd ~
for item in *
do
 echo "Item $((i++)) : $item"
done
#------------------------------------------
i=1
for file in /etc/[abcd]*.conf
do
 echo "File $((i++)) : $file"
done
#------------------------------------------
for ((i=1, j=10; i <= 5 ; i++, j=j+5))
do
 echo "Number $i: $j"
done
#------------------------------------------
for num in {1..10..2}
do
 echo "Number: $num"
done
#------------------------------------------

{% endhighlight %}

54.bash中的算术元算

{% highlight vim %}
#自加
((num++))


{% endhighlight %}

55. bash中把行倒叙 tac， 把列倒叙 rev

#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

Sed篇 1.取出文件中特定的一行或几行

{% highlight vim %}
sed -n '1,20'p TAIR10_cds_20101214
{% endhighlight %}

2.列出文件夹的目录结构，可以用tree命令实现

{% highlight vim %}
ls -R | grep ":$" | sed -e 's/:$//' -e 's/[^-][^\/]*\//--/g' -e 's/^/   /' -e 's/-/|/'
{% endhighlight %}

3.去除文件中的空行

{% highlight vim %}
sed -i '/^$/d' filename
{% endhighlight %}

4.sed记忆匹配

{% highlight vim %}
sed 's/\(pat\)/ok \1 ok/'
{% endhighlight %}

5.sed给每行增加行号

{% highlight vim %}
sed = file(增加行号，并行号单独放在一行)
sed = file | sed 'N;s/\n/\t/'（编号和行在同一行）
sed = file | sed 's/^/>locus/;N' （把文件转换为fasta格式,添加locus是为了避免fasta的序列标号以数字开头，这不被tcoffee识别）
{% endhighlight %}

6.sed在特定位置插入行 [\ 可能不需要]

{% highlight vim %}
a.在第n行前面插入内容"content"（假设n为1）[i为前面插入，\表示i结束]
sed '1 i\context' -i file
b.在第n行后面插入内容"content"（假设n为1）[a为前面插入，a表示i结束]
sed '1 a\context' -i file
c.在特定匹配位置出插入(假设要匹配pattern)
sed '/pattern/a\context' -i file

{% endhighlight %}

7.sed奇数偶数行处理

{% highlight vim %}
a.偶数行合并到奇数行
echo -e '1\n2\n3\n4\n' | sed -n 'N;s/\n//;p'
解释：N表示先读入第一行到patternspace，然后执行N命令，读入第二行追加近patternspace，这时patternspace里有1\n2，然后执行s/\n//去掉中间的换行符，打印出来
b.取出偶数行
echo -e '1\n2\n3\n4\n' | sed -n 'n;s/\n//;p'
echo -e '1\n2\n3\n4\n' | sed -n 'n;p'
解释：先读入第一行到patternspace，然后执行n命令，用第二行去覆盖当前patternspace，由于未读入\n，不执行任何替换。
c.取出奇数行
echo -e '1\n2\n3\n4\n' | sed -n 'N;s/\n.*//;p'
d.如果用awk处理，可能会更方便和易于理解些。

{% endhighlight %}

8.删除一个用户的全部进程

{% highlight vim %}
killall -u username
{% endhighlight %}

9.删除包含某一特定的程序的所有进程

{% highlight vim %}
killall -e progNamw
{% endhighlight %}

10.sed使用bash的变量

{% highlight vim %}
J=‘OK’
sed -i "s/yes/$j/" file

{% endhighlight %}

11.sed删除行 (删除不需要-n，去除行需要-n)

{% highlight vim %}
sed '2d' text  #删除第二行
sed '/match/d' test  #删除匹配上match的行
sed '3,$ {/match/d}' test  #输出从第三行到最后匹配上match的行
sed '1, /match/d' test #删除从第一到匹配上match的行
sed '/match1/,/match2/d' test #删除匹配上match1行到match2行之间的行
#取得行号
sed -n '/match_regx/=' file
#output
sed '/match/p' file
# -n repress outputting original matched line
sed -n '/match/p' file
sed -n '/pre/,/post/p' file
sed -n '1,/match/p' file


{% endhighlight %}

12. sed对特定行进行操作

{% highlight vim %}
#特定行替换［最初用于保证R的write.table能输出正确的列数］

sed '1 s/^\t/label\t/' r.output


{% endhighlight %}

13.  
14.  
15. http://sed.sourceforge.net/sed1line_zh-CN.html

Awk篇(默认用空格分割)  
0.Awk representing script

{% highlight vim %}
awk 'BEGIN{OFS="\t";FS="\t"}{file="";
    if(FNR==1) {print $0 >"DhMR.high.2"; print $0 >"DhMR.low.2";} \
    else { if(($2+1)/($3+1) > 2 && ($4+1)/($3+1) > 2) {file="DhMR.high.2"; print $0 >>file;} \
    else if (($2+1)/($3+1) < 0.5 && ($4+1)/($3+1) < 0.5) {file="DhMR.low.2"; print $0 >>file;}}}'

{% endhighlight %}

1.做两列的四则运算

{% highlight vim %}
awk -F ' ' '{print $1 "\t" $2 "\t" $3 "\t" $3/$2}' result.ori
{% endhighlight %}

2.交换两列

{% highlight vim %}
awk '{ss=$1;$1=$2;$2=ss; print $0}' awk 'BEGIN{FS="\t";OFS="\t"}{ss=$1;$1=$2;$2=ss;print $0}'
{% endhighlight %}

3.求文件一行的最小值

{% highlight vim %}
awk 'a=$1{for(i=2;i<=NF;i++)if($i<a)a=$1;print a}' file
{% endhighlight %}

4.求文件所有数值的最小值

{% highlight vim %}
awk 'NR==1{a=$1}{for(i=2;i<=NF;i++)if($i<a)a=$i}END{print a}' file
{% endhighlight %}

5.求文件每一列的平均值

{% highlight vim %}
awk '{for(i=1;i<=NF;i++)a[i]+=$i}END{for(i=1;i<=NF;i++)print a[i]/NR}' file
{% endhighlight %}

6.awk if else if else

{% highlight vim %}
cat <<END >grade.awk
f ( avg >= 90 ) grade="A";
else if ( avg >= 80) grade ="B";
else if (avg >= 70) grade ="C";
else grade="D";
END

awk -f grade.awk grade

{% endhighlight %}

7.awk中计算相关的函数

{% highlight vim %}
+ （加），- （减）， * （乘）， / （除）， ^ 或 **（乘方）， % 取模） 等等。

awk 也提供了一些常用的数学函数, 比如 sin(x), cos(x), exp(x), log(x)[自然对数], sqrt(x), rand()。
{% endhighlight %}

8.awk字符串连接

{% highlight vim %}
awk '{a=$1 $2 $3 "\t" $4;print a}' file
{% endhighlight %}

9.awk替换操作，支持正则表达式

{% highlight vim %}
awk '{gsub(/ori/, "sub", $2}' file
{% endhighlight %}

10.awk转换大小写

{% highlight vim %}
awk 'BEGIn{OFS="\t"}{print $1, toupper($2)}' file
{% endhighlight %}

11.awk if else <http://www.thegeekstuff.com/2010/02/awk-conditional-statements/>

{% highlight vim %}
conditional-expression ? action1 : action2 ;
if(conditional-expression1)
	action1;
else if(conditional-expression2)
	action2;
else if(conditional-expression3)
	action3;
	.
	.
else
	action n;

{% endhighlight %}

12.awk的split函数

{% highlight vim %}
split(fullstr,a,"-")

#the first parameter is the full string you want to split,
the second is an array contains the splitted part, 1-indexed,
the third parameter is the separtor. I
t return the length of the array. One can get the first part by using a[1].
{% endhighlight %}

13. awk 按第一列合并<http://blog.163.com/qingfeng_0105@126/blog/static/750627382011315112338716/>

{% highlight vim %}
A     88

B     78

B     89

C     44

A     98

C     433

要求输出：A：88；98

B：78；89

C：44；433

awk '{a[$1]=a[$1]" "$2}END{for(i in a)print i,a[i]}' test.txt |awk '{print $1":",$2";",$3}'

awk 'BEGIN{OFS="\t";FS="\t"}{key=$1"\t"$2"\t"$3; if (! a[key]) a[key]=$4; \
    else if ($4>a[key]) a[key]=$4; }END{for (i in a ) print i,a[i]}'
{% endhighlight %}

14.按行统计字符出现次数

{% highlight vim %}
awk -F'[XY]' 'NF>1{t+=NF-1}END{print t}' input

{% endhighlight %}

15.awk给每行增加行号，使其变为唯一

{% highlight vim %}
awk 'BEGIN{OFS="\t";FS="\t"}NR!=1{$4=$4"_"NR;print $0}' file
{% endhighlight %}

16.awk round

{% highlight vim %}
awk  'BEGIN { rounded = sprintf("%.0f", 3/2); print rounded }'

{% endhighlight %}

17.awk统计文件中一行某字符的比例

{% highlight vim %}
awk 'BEGIN{OFS="\t";FS="\t"}{a=length; gsub(/[^A]/,""); print length/a}' txtfile
{% endhighlight %}

18.Pass Shell Variables To awk [http://www.cyberciti.biz/faq/linux-unix-appleosx-bsd-bash-passing-variables-to-awk/]

{% highlight vim %}
root="/webroot"
echo | awk -v r=$root '{ print "shell root value - " r}'
awk -v v1=$v1 -v v2=$V2 '{ print "shell root value - " v1, v2}'

{% endhighlight %}

19.awk匹配含有特定字符串的列

{% highlight vim %}
awk 'BEGIN{OFS="\t";FS="\t"}{for(i=1;i<=NF;i++) if ($i ~ /MIR/) print $i}'

awk 'BEGIN{OFS="\t";FS="\t"}{for(i=1;i<=NF;i++) if ($i ~ "MIR") print $i}'
{% endhighlight %}

20.awk计算对数

{% highlight vim %}
awk 'BEGIN{OFS="\t";FS="\t"}{print log($0)/log(2)}'
{% endhighlight %}

21.awk读两个文件

{% highlight vim %}
awk 'BEGIN{OFS="\t";FS="\t"}NR==FNR{a[$4]=a[$4]"\n"$0}NR!=FNR{$0=a[$1];print}' file1 file2

awk 'BEGIN{OFS="\t";FS="\t"}ARGIND==1{a[$4]=a[$4]"\n"$0}ARGIND==2{$0=a[$1];print}' file1 file2

#Use '-' represents standard input when reading multiple files
cat file2 | awk 'BEGIN{OFS="\t";FS="\t"}ARGIND==1{a[$4]=a[$4]"\n"$0}ARGIND==2{$0=a[$1];print}' file1 -


{% endhighlight %}

22.awk同时读两个文件，每次各读一行 (文件名 file1,file2) [也可用paste完成]

{% highlight vim %}
awk 'BEGIN {OFS="\t";FS="\t"}
{
    getline f2line < "file2"
    f2line_len = split(f2line,f2line_L,FS)
    print $1,f2line[1]
} '  file1
#The getline command returns 1 on success, 0 on end of file, and -1 on an #error.
#Upon an error, ERRNO contains a string describing the problem.


{% endhighlight %}

&nbsp;

{% highlight vim %}
while ((getline line < "file") > 0)
    print line
close("file")

{% endhighlight %}

23.awk写入多个文件，根据文件内部条件写入不同文件

{% highlight vim %}
awk 'BEGIN{OFS="\t";FS="\t"}{print $2 >$1}' file
{% endhighlight %}

24.awk去除数字小数位

{% highlight vim %}
awk 'BEGIN{OFS="\t";FS="\t"}{print $1，int($2+0.5)}' file
{% endhighlight %}

25.awk在作字符串比较时可能使用位与操作，因此对于很小的数比较可恩那个会发生溢出的现象。推荐使用算数操作，可以避免这个问题。

26.awk强制退出用some_cmd;exit;

27.awk不能识别Linux下的家目录符号(~)

28.awk输出到标准错误并退出 [错误的用法]

{% highlight vim %}
awk 'BEGIN{OFS="\t";FS="\t"}{print $0 >"&2"; exit;}' file

{% endhighlight %}

29.awk格式化输出

{% highlight vim %}
>echo "12345 0.618" | awk '{printf("%s\t%f\n", $1,$2)}'
12345	0.618000
>echo "12345 0.618" | awk '{printf("%s\t%.2f\n", $1,$2)}'
12345	0.62
>echo "12345 0.618" | awk '{printf("%s\t%.1f\n", $1,$2)}'
12345	0.6
>echo "12345 0.618" | awk '{printf("%s\t%.0f\n", $1,$2)}'
12345	1

{% endhighlight %}

30.awk中自定义函数

{% highlight vim %}
awk 'function abs(x){return ((x < 0.0) ? -x : x)}BEGIN{OFS="\t";FS="\t"}{pos[1]=$1;pos[2]=$2;pos[3]=$3;pos[4]=$4; len=asort(pos);for(i=len;i>1;i--) print abs(pos[i]-pos[i-1]);}'

{% endhighlight %}

31.

32.

33.

34.

Perl篇

1.一个字符串重复多次输出

{% highlight vim %}
echo `perl -e "print '-' x 10"`
{% endhighlight %}

2.统计一个字符的出现次数

{% highlight vim %}
perl -e 'while (<>){$count+=s/char//g;} print "$count\n"' filename

perl -en '$count += s/char//g; print "$count\n"' filename | tail -n 1

echo '12,21,23,' | perl -nle '$t +=tr/,//;print ++$t if eof'
{% endhighlight %}

3.匹配并且利用

{% highlight vim %}
perl -ne 'print if /AS:i:(\d+)/&&$1>=400' in.sam
{% endhighlight %}

4.

5.

6.

7.

8.

9.

10.

11.

12.

13.

14.

15.

16.

Convert篇

1.eps图形转换为png

{% highlight vim %}
mogrify -format png logo*.eps    #批量转换

convert -density 200 -flatten myPlot.eps myPlot.png #-density指定像素


{% endhighlight %}

Printer

system-config-printer

参考资料：

http://www.tsnc.edu.cn/default/tsnc\_wgrj/doc/abs-3.9.1\_cn/html/index.html

 [1]: http://codingstandards.iteye.com/blog/796299
