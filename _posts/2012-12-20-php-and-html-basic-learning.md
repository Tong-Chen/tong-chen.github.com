---
title: php and html
author: 悟道
layout: post
categories:
  - php
tags:
  - php
---

<pre class="brush: xml; title: ; notranslate" title="">&lt;html&gt;

&lt;head&gt;
&lt;title&gt;
Homework
&lt;/title&gt;
&lt;/head&gt;

&lt;body&gt;

Please give us a sequence in fasta format:&lt;br/&gt;

&lt;form method="post" action="b.php"&gt;

&lt;textarea name="texttext1" rows="10" cols="80" &gt;&lt;/textarea&gt;

&lt;p&gt;Length(k):
&lt;input type="text" name="len_k" value="6" /&gt;
&lt;/p&gt;
&lt;input type="submit" value="Submit" &gt;
&lt;/input&gt;

&lt;/form&gt;

&lt;/body&gt;

&lt;/html&gt;



</pre>

<pre class="brush: php; title: ; notranslate" title="">&lt;?php
$my_input=$_POST["texttext1"];
$k=$_POST["len_k"];
// Parse fasta
$lines=split("\n", $my_input);
$description=array();
$linked_seq=array();
for($i=0,$j=-1;$i&lt;sizeof($lines);$i++){
 if ($lines[$i][0]=="&gt;"){
  $locus = str_replace('&gt;','',trim($lines[$i]));
  $description[]=$locus;
  $j++;
 }else {
  $linked_seq[$j]=$linked_seq[$j].trim($lines[$i]);
 }
}
//-coonnect to database----------------------------------------
@ $db=new mysqli('localhost', 'hw', '123456', 'HW');
if( mysqli_connect_errno()){
 echo 'Error: Could not connect to database. Please try again later.';
 exit;
}
//-----table-----------------------------------------------------
$query = "DROP TABLE IF EXISTS query;";
$result=$db-&gt;query($query);
$query = "create table query ( id int unsigned not null auto_increment primary key, `desc` text, seq text);";
$result=$db-&gt;query($query);
//-----table-----------------------------------------------------
$tables=array('query','dbseq');
for ($i=0;$i&lt;sizeof($description);$i++){  
  $segs=str_split($linked_seq[$i],$k);
  for ($j=0;$j&lt;sizeof($segs);$j++){
    $query = "INSERT INTO " . $tables[$i] . " (`desc`, seq) values ('$description[$i]', '$segs[$j]');";
    $result=$db-&gt;query($query);
  }
}
//--------select and display-------------------------------------------------
echo "&lt;hr&gt;";
$query="select * from query";
$result=$db-&gt;query($query);
echo "Sequences in table query&lt;br/&gt;&lt;br/&gt;";
while ($row=$result-&gt;fetch_row()){
    echo $row[0].' | '.$row[1].' | '.$row[2].'&lt;/br&gt;';
}
$db-&gt;close();
?&gt;

</pre>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;  
1.修改完html之后，先刷新再调用。  
2.
