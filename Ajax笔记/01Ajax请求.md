#Ajax？made by lois

##不刷新页面的情况下自己发请求
----
```
...
html代码
...
<script>
    document.querySelector('input').onclick = function(){
    var xhr = new XMLHttpRequest();//创建异步对象

    xhr.open('get','xxx.php');//请求行 包括请求方式和url

    xhr.onload = function(){
        console.log('hhhh');
        document.querySelector('h3').innerHTML = xhr.responseText;//将服务端返回的数据写入h3
    }//请求响应回来之后会触发的回调函数

    xhr.setRequestHeader('name','jack')//请求头 参数1：键名 参数2：值 在get请求中可以省略。

    xhr.send(null)//请求主体
}
</script>
```
---
###例子
####验证用户名是否存在，后端以php为例
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
    <h2>用户注册</h2>
    <h3>状态</h3>
    <input type="text" name="" placeholder="请输入用户名">
</body>
<script type="text/javascript">
	document.querySelector('input').onblur= function(){ //失去焦点时触发
    document.querySelector('h3').innerHTML = '验证中'；
	var xhr = new XMLHttpRequest();//创建异步对象

    xhr.open('get','checkName.php?name='+this.value);

    xhr.onload = function(){
        console.lod(xhr.respondeText);
        document.querySelector('h3').innerHTML = '验证完毕' //修改验证状态
        document.querySelector('h2').innerHTML = xhr.responseText;//收到响应后修改h2
    }

    <!-- xhr.setRequestHeader('name','jack') -->

    xhr.send(null)//请求主体
	}
</script>
</html>
```
-后端部分
```
<?php
    $name = $_GET[name];

    $nameArr = array('jack','rose','ice');//假数据

    $result = in_arry($name,$namrArr);//判断新用户名是否存在

    if($result === true){
        echo '用户名已经存在。'
    }else{
        echo '该用户名可用。'
    }
?>
```
