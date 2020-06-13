# Ajax发送post请求 made by lois
---
### 例子
- 前端部分
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h2>ajax发送post请求</h2>
    <input type="button" value="post请求">
</body>
<script type="text/javascript">
	document.querySelector('input').onclick= function(){ //失去焦点时触发
    document.querySelector('h3').innerHTML = '验证中'；
	var xhr = new XMLHttpRequest();//创建异步对象

    xhr.open('post','postData.php);

    xhr.setRequestHeader('content-type','application/x-www-form-urlencoded');//把content-type改成默认值

    xhr.onload = function(){
        console.lod(xhr.respondeText);
    }
    xhr.send('name=jack&friend=rose');//post请求发送数据写在这
	}
</script>
</html>
```
-后端部分
```
<?php
echo '你post过来啦';

print_r($_POST);
?>
```
---
## 聊天机器人练习
1.浏览器端
- 输入框
- 发送按钮
   
   - 点击发送按钮时发请求 -ajax
   - 创建一个聊天框

2.服务器端(我们不用关心其实)
- 返回信息
- 当数据回来后渲染到页面上（创建一个聊天框）
   
   - 回调函数里面

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body{
            background-color:pink;
        }
        ul{
            width: 400px;
            border:1px solid black;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <h2>聊天机器人简单版</h2>
    <input type="text">
    <input type="button" value="发送">
    <h3>聊天框</h3>
    <ul>

    </ul>
</body>
<script type="text/javascript">
	document.querySelector('input[type=button]').onclick= function(){ //失去焦点时触发
        //创建聊天框
        var myli = document.createElement('li');
        myli.innerHTML = document.querySelector('input[type=text]').value;
        myli.style.backgroundColor = 'yellow';
        document.querySelector('ul').appendChild(myli);
	}

    //ajax
    var xhr = new XMLHttpRequest();

    xhr.open('get','chat.php');//假设chat.php已经存在写好了 因为没有php运行的服务器只能假设。。

    xhr.onload = function(){
        console.log(xhr.responseText);
        //创建对方的聊天框
        var hisli =  document.createElement('li');
        hisli.innerHTML = xhr.responseText;
        hisli.style.backgroundColor = 'skyblue';
        document.querySelector('ul').appendChild(hisli);
    }

    xhr.send(null);
</script>
</html>
```