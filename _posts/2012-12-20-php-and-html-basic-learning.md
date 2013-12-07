---
title: php and html
author: 悟道
layout: post
categories:
  - php
  - letter
tags:
  - php
---
<pre>
<html>

<head>
<title>
Homework
</title>
</head>

<body>

Please give us a sequence in fasta format:<br/>

<form method="post" action="b.php">

<textarea name="texttext1" rows="10" cols="80" ></textarea>

<p>Length(k):
<input type="text" name="len_k" value="6" />
</p>
<input type="submit" value="Submit" >
</input>

</form>

</body>

</html>

</pre>

<pre>
<?php
$my_input=$_POST["texttext1"];
$k=$_POST["len_k"];
// Parse fasta
$lines=split("\n", $my_input);
$description=array();
$linked_seq=array();
for($i=0,$j=-1;$i<sizeof($lines);$i++){
 if ($lines[$i][0]==">"){
  $locus = str_replace('>','',trim($lines[$i]));
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
$result=$db->query($query);
$query = "create table query ( id int unsigned not null auto_increment primary key, `desc` text, seq text);";
$result=$db->query($query);
//-----table-----------------------------------------------------
$tables=array('query','dbseq');
for ($i=0;$i<sizeof($description);$i++){  
  $segs=str_split($linked_seq[$i],$k);
  for ($j=0;$j<sizeof($segs);$j++){
    $query = "INSERT INTO " . $tables[$i] . " (`desc`, seq) values ('$description[$i]', '$segs[$j]');";
    $result=$db->query($query);
  }
}
//--------select and display-------------------------------------------------
echo "<hr>";
$query="select * from query";
$result=$db->query($query);
echo "Sequences in table query<br/><br/>";
while ($row=$result->fetch_row()){
    echo $row[0].' | '.$row[1].' | '.$row[2].'</br>';
}
$db->close();
?>

</pre>
1.修改完html之后，先刷新再调用。  
2.
