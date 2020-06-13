# XML 一种数据的格式 made by lois
---
### 书写格式

```
<?xml version="1.0" encoding="UTF-8"?> 
<!-- 不是必须的 -->
<root>
<!-- 标签名可用随便取，但都是双标签，即成对出现。 -->
    <name>jack</name>
    <age>18</age>
    <skill>singing</skill>
</root>

```

### ajax请求xml
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h2>请求xml文件啊</h2>
    <input type="button" value-"点击获取xml文件">
</body>
</html>
<script>
    document.querySelector('input').onclick = funciton(){
        var xhr = new XMLHttpRequest();

        xhr.open('post','backXML.php');//假设存在后端

        // xhr.setRequestHeader();//不发数据可用省略

        xhr.onreadystatechange = function(){
            if(xhr.readystate === 4 && xhr.status === 200){
                // console.log(xhr.responseText);//此时接收的是字符串，不好解析
                console.log(xhr.responseXML);//返回了一个document对象
            }
        }

        xhr.send(null);
    }
</script>
```
### 解析发回来的xml
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h2>请求xml文件啊</h2>
    <input type="button" value-"点击获取xml文件">
    <h3></h3>
</body>
</html>
<script>
    document.querySelector('input').onclick = funciton(){
        var xhr = new XMLHttpRequest();

        xhr.open('post','backXML.php');//假设存在后端

        // xhr.setRequestHeader();//不发数据可用省略

        xhr.onreadystatechange = function(){
            if(xhr.readystate === 4 && xhr.status === 200){
                // console.log(xhr.responseText);//此时接收的是字符串，不好解析
                console.log(xhr.responseXML);//返回了一个document对象

                var name = xhr.responseXML.querySelector('name').innerHTML;//拿到note.xml里面的name标签里面的值
                var age = xhr.responseXML.querySelector('age').innerHTML;
                var skill = xhr.responseXML.querySelector('skill').innerHTML;

                //把数据放进h3标签里
                document.querySelector('h3').innerHTML = name + '--' + age + '--' + skill; 
            }
        }

        xhr.send(null);
    }
</script>
```
### 例子 查询天气
- 使用外部接口（虽然说接口已经失效了orz。。）
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h2>天气预报</h2>

    <input type="text" value="请输入要查询的城市">

    <input type="button" value="查询">
</body>
</html>
<script>
    // 点击按钮获取所要查询的的城市
    document.querySelector('input[type=button]').onclick = function(){
        //ajax
        var xhr = new XMLHttpRequest();

        xhr.open('get','http://wthrcdn.etouch.cn/WeatherApi ?city=' + document.querySelector('input[type=text]').value);
        //api已经失效了。。

        xhr.onreadystatechange() = function(){
            if(xhr.readyState === 4 &&  xhr.status === 200){
                console.log(xhr.responseXML)//根据响应回来的xml的标签名进行解析
                //类似这样：var skill = xhr.responseXML.querySelector('skill').innerHTML;
            }
        }
        xhr.senf(null);
    }
</script>
```

### xml的缺点
- 传输的数据量略大
- 解析有点复杂（document然后一串...）
- 于是json就出现辣！