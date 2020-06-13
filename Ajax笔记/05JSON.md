# JSON made by lois
- 是一种数据的格式
- 载体是字符串
- 基本上所有编程语言都支持（都提供对应方法来解析）
---
### 格式 
- 属性名 必须用"" (双引号)包裹
- 属性值 必须用"" (双引号)包裹 但是数值可不用
##### json表示对象
```
<script>
    var jsonobj = '{"name":"jack","skill":"singing"}' ;//json字符串
    console.log(jsonobj);//打印的是 {"name":"jack","skill":"singing"}
    var obj = JSON.parse(jsonobj);//将字符串转为js对象
    console.log(obj);//打印的是 Object
    console.log(obj.name+'|'+obj.skill);//打印的是 jack|singing
</script>
```

##### json表示数组
```
<script>
    var jsonArr = '["苹果","香蕉","橙子","西瓜"]';
    console.log(jsonArr);//["苹果","香蕉","橙子","西瓜"]
    var arr = JSON.parse(jsonArr);
    console.log(arr);//Array(4)
    console.log(arr[1]);//香蕉
</script>
```

##### 对象数组
```
 var jsonObjArr = '{"name":"rose","skill":"swimming","friends":["jenny","tony","lisa"]}';
    console.log(jsonObjArr);//{"name":"rose","skill":"swimming","friends":["jenny","tony","lisa"]}
    var objArr = JSON.parse(jsonObjArr);
    console.log(objArr);//{name: "rose", skill: "swimming", friends: Array(3)}
    console.log(objArr.name);//rose
    console.log(objArr.friends[2]);//lisa
```

##### 接收响应
```
var obj = JSON.parse(xhr.responseText);
//因为载体为字符串 所以用responseText接收
```