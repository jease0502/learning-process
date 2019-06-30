# magic mirror專題
---
## 前置作業

[magic mirror安裝](https://github.com/MichMich/MagicMirror)

[遠端連線網址](http://140.134.32.39:2139/cgi-bin/)



## 功能需求


### magicmirro設定

- [x] 1.更換背景
> 檔案已修改成功
- [x] 2.更換問候語
>如果要更改問候語則要去 /home/pi/MagicMirror/modules/default/compliments 
>中打開compliments.js 
>更改裡面有中文的地方
- [x] 3.使螢幕反轉
>如果螢幕要轉90度將
>sudo nano /boot/config.txt   
>最後一行的#刪掉變成display_rotate=1

### 刷卡整理

#### 需求分析
將刷卡的資料傳到mysql上面，然後把它載下來整理，最後把缺到達日期給記錄下來，並自動寄信
![](https://i.imgur.com/R2d8bqO.jpg)



#### 第一部分

- [x] 1.rc522-python測試
- [x] 2.撰寫資料寫入與上傳mysql
- [x] 3.製作掃描感應機制，當感應到磁卡時，將資料回傳資料庫，並去記錄當前登入時間。
- [ ] 4.將每個人的RFID建檔並存入MySQL-----以做一個示範

#### 第二部分

- [x] 1.利用migicmirror進行刷卡並將數據上傳伺服器
- [x] 2.上傳伺服器並將資料抓下來
- [x] 3.更改檔案內容，加上uid、datatime欄位
- [x] 4.整理數據，將不同時間數據進行整理
- [x] 5.可視化完成
- [ ] 6.再刷卡時，同時顯示出是否刷卡成功

>如果有出現就是1，沒出現就是0，這樣去判斷每日出席人數

![](https://i.imgur.com/EOoA3bn.jpg)


### 即時訊息回傳

- [x] 1.撰寫to do list頁面
- [x] 2.撰寫rss頁面
- [x] 3.進行to do list與rss串聯
- [x] 4.rss中文使顯示正常
- [ ] 5.將rss網址輸入至migicmirror上

[rss連結](http://140.134.32.39/mirror/reports.xml)

---
## 程式檔案

### 及時回傳訊息

[todo.php](http://140.134.32.39/mirror/todo.php)
[style.css](http://140.134.32.39/mirror/style.css)

- todo.php
```php=
<?php
	$errors = "";

	$db = mysqli_connect("140.134.32.39:3306", "root2", "admin", "todo");
	mysql_query("set character set utf8",$db);
	mysqli_query($db,"SET CHARACTER SET UTF8");
	mysql_query("SET CHARACTER_SET_database= utf8",$db);
	mysql_query("SET CHARACTER_SET_CLIENT= utf8",$db);
	mysql_query("SET CHARACTER_SET_RESULTS= utf8",$db);
 	mysql_query("SET NAMES UTF8");
	if (isset($_POST['submit'])) {
		$task = $_POST['task'];
		if (empty($task)) {
			$errors = "You must fill in the task";
		}
		else{
			mysqli_query($db,"INSERT INTO tasks (task) VALUES ('$task')");
			header('location: todo.php');
		}

	}

	if (isset($_GET['del_task'])) {
		$id = $_GET['del_task'];
		mysqli_query($db,"DELETE FROM tasks WHERE id=$id");
		header('location: todo.php');
	}

	$tasks = mysqli_query($db,"SELECT * FROM tasks");
	$xml=new DOMDocument('1.0','UTF-8');
	  $xml->formatOutput=true;
	  $todolist=$xml ->createElement("channel");
	  $xml->appendChild($todolist);

	  while ($row=mysqli_fetch_array($tasks)) {
	  	$todo=$xml->createElement("title");
	  	$todolist->appendChild($todo);
	  	 $task=$xml->createElement("task",$row['task']);
	  	 mb_convert_encoding($task, "UTF-8"); //編碼轉換為utf-8
	  	 $todo->appendChild($task);
	  }
		  $xml ->save("reports.xml");
	$tasks = mysqli_query($db,"SELECT * FROM tasks");

?>

<!DOCTYPE html>
<html lang="ch">
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" >
	<title>Todo list </title>
	<link rel="stylesheet" type="text/css" href="style.css">
</head>
<body>
	<div class="heading">
		<h2>To do list </h2>
	</div>

	<form method="POST" action="todo.php">
	<?php if (isset($errors)) { ?>
		<p><?php echo $errors ?></p>
	<?php } ?>
		<input type="text" name="task" class="task_input">
		<button type="submit" class="add_btn" name="submit">Add Task</button>
	</form>

	<table>
		<thead>
			<tr>
				<th>N</th>
				<th>Task</th>
				<th>Action</th>
			</tr>
		</thead>

		<tbody>
		<?php $i = 1; while ($row = mysqli_fetch_array($tasks)) {?>
			<tr>
				<td><?php echo $i; ?></td>
				<td class="task"><?php echo $row['task']; ?></td>
				<td class="delete"><a href="todo.php?del_task=<?php echo $row['id']; ?>">x</a></td>
			</tr>
		<?php } ?>

		</tbody>
	</table>
</body>
</html>
```

style.css
```css=
body{
	font-size: 20px;
	text-align: center;
	background-image: url('http://scdn.file1.gk99.com/photo/2012-12/2012-12-27/135659006021886.jpg');
            background-repeat: no-repeat;
            background-attachment: fixed;
            background-position: center;
            background-size: cover;
}


.heading{
	width:50%;
	margin: 30px auto;
	text-align: center;
	text-align: #238E88;
	background: #E7AFE6;
	
	border-radius: 20px;
	text-align: center;
}

form{
	width:50%;
	text-align: center;
	margin: 30px auto;
	
	border-radius: 3px;
	padding: 5px;
	background: #2C3F9F;
	border:1px solid #238E88;
}

form p{
	color:red;
	margin: 0px;
}

.task_input {
	width:73%;
	height: 15px;
	padding: 10px;
	border:2px solid #238E88;
}

.add_btn{
	height: 39px;
	background: #E7AFE6;
	color: #238E88;
	border:2px solid #238E88;
	border-radius: 5px;
	padding: 5px 20px;
}

table{
	width: 50%;
	margin: 31px auto;
	
}

tr{
	border-bottom: 1px solid #cbcbcb;
}

th{
	font-size: 19px;
	color: #238E88;
}

th,td{
	border: none;
	height: 30px;
	padding: 2px;
}


}

.task{
	
	text-align: left;
}

.$i{
	text-align: right;	
}

.delete{
	
	text-align: center;
}

.delete a{
	color: white;
	background: #a52a2a;
	padding: 1px 6px;
	border-radius: 3px;
	text-decoration: none;
}
```

---
## 功能演示



---

