##Ajax
**对Ajax的理解**
+ AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。

+ AJAX 是一种用于创建快速动态网页的技术。

+ AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。

+ AJAX 不需要任何浏览器插件，但需要用户允许JavaScript在浏览器上执行。

**Ajax的工作原理**
![avatar](/img/Ajax1.png)
**创建 XMLHttpRequest 对象用于Ajax请求**
+ 创建对象实例：
```
通用型
var xmlhtttp = new XMLHttpRequest();
老版本（IE.5 IE.6）
var xmlhttp = nwe ActiveXObject("Microsoft.XMLHTTP");
```
对像里面的两个方法：open（）和send（）
xmlhttp.open(method,url,asyns)
|方法|描述|
|---|---|
|open(method,url,async)	|规定请求的类型、URL 以及是否异步处理请求。method：求的类型；GET 或 POST url：文件在服务器上的位置 async：true（异步）或 false（同步）|
|send(string)|将请求发送到服务器。string：仅用于 POST 请求|

+ 向服务器发送请求有两种方式：get和post方法
<font style="color:red">get还是post：
get与post相比更快更简单，并且在大多数情况下都可以使用，在以下情况下：
1.在无法使用缓存文件（更新服务器的文件和数据库）
2.向服务器发送大量数据（post对发送的数据量没有限制）
3.发送用户的数据里含有未知字符，post比get更稳定</font>
get请求：
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script>
function loadXMLDoc()
{
	var xmlhttp;
	if (window.XMLHttpRequest)
	{
		// IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
		xmlhttp=new XMLHttpRequest();
	}
	else
	{
		// IE6, IE5 浏览器执行代码
		xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
	}
	xmlhttp.onreadystatechange=function()
	{
		if (xmlhttp.readyState==4 && xmlhttp.status==200)
		{
			document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
		}
	}
	xmlhttp.open("GET","/try/ajax/demo_get.php",true);
	xmlhttp.send();
}
</script>
</head>
<body>

<h2>AJAX</h2>
<button type="button" onclick="loadXMLDoc()">请求数据</button>
<div id="myDiv"></div>

</body>
</html>
```
在上面的例子中，您可能得到的是缓存的结果。为了避免这种情况，请向 URL 添加一个唯一的 ID：
```
xmlhttp.open("GET","/try/ajax/demo_get.php?t=" + Math.random(),true);
xmlhttp.send();
```
如果您希望通过 GET 方法发送信息，请向 URL 添加信息：
```
xmlhttp.open("GET","/try/ajax/demo_get2.php?fname=Henry&lname=Ford",true);
xmlhttp.send();
```
psot请求：
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script>
function loadXMLDoc()
{
  var xmlhttp;
  if (window.XMLHttpRequest)
  {
    // IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xmlhttp=new XMLHttpRequest();
  }
  else
  {
    // IE6, IE5 浏览器执行代码
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
  xmlhttp.onreadystatechange=function()
  {
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
      document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  }
  xmlhttp.open("POST","/try/ajax/demo_post.php",true);
  xmlhttp.send();
}
</script>
</head>
<body>

<h2>AJAX</h2>
<button type="button" onclick="loadXMLDoc()">请求数据</button>
<div id="myDiv"></div>
 
</body>
</html>
```
如果需要像 HTML 表单那样 POST 数据，请使用 setRequestHeader() 来添加 HTTP 头。然后在 send() 方法中规定您希望发送的数据：
```
xmlhttp.open("POST","/try/ajax/demo_post2.php",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Henry&lname=Ford");
```

+ Ajax的异步操作：
当async为true时，此次Ajax为异步操作。在没有Ajax之前，这将导致将程序挂起或停止；
通过Ajax请求程序无需等待：
 *1. 在等待服务器响应时执行其他脚本*
 *2. 当响应就绪时对该响应进行处理*

 + 服务器响应
 服务器响应会返回两种格式的数据对应着两种属性responseText和responseXMl
 	
|属性|描述|
|---|---|
|responseText|获得字符串形式的响应数据。|
|responseXML|获得 XML 形式的响应数据。|
responseText实列：
```
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```
responseXMl实列：
```
xmlDoc=xmlhttp.responseXML;
txt="";
x=xmlDoc.getElementsByTagName("ARTIST");
for (i=0;i<x.length;i++)
{
    txt=txt + x[i].childNodes[0].nodeValue + "<br>";
}
document.getElementById("myDiv").innerHTML=txt;
```
+ onreadystatechange 事件
当服务器响应Ajax请求时，就会改变readyState的值，并且当响应已就绪时，每次readyState值发生改变就会触发onreadystatechange事件，当满足条件时执行里面的代码。

下面是 XMLHttpRequest 对象的三个重要的属性：

|属性|描述|
|---|---|
|onreadystatechange|存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。|
|readyState|存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。0: 请求未初始化1: 服务器连接已建立2: 请求已接收3: 请求处理中4: 请求已完成，且响应已就绪|
|status	|200: "OK"  404: 未找到页面|


+ 使用回调函数来进行多次Ajax请求：
网站存在多个Ajax请求，我们不必为每一个Ajax请求都建立一个特有Ajax对象，我们只需要对XMLHttpRequest建立一个标准函数，在函数里对自己需要数据进行处理。该函数调用应该包含 URL 以及发生 onreadystatechange 事件时执行的任务（每次调用可能不尽相同）：
```
<!DOCTYPE html>
<html>
<head>
<script>
var xmlhttp;
function loadXMLDoc(url,cfunc)
{
if (window.XMLHttpRequest)
  {// IE7+, Firefox, Chrome, Opera, Safari 代码
  xmlhttp=new XMLHttpRequest();
  }
else
  {// IE6, IE5 代码
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
xmlhttp.onreadystatechange=cfunc;
xmlhttp.open("GET",url,true);
xmlhttp.send();
}
function myFunction()
{
	loadXMLDoc("/try/ajax/ajax_info.txt",function()
	{
		if (xmlhttp.readyState==4 && xmlhttp.status==200)
		{
			document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
		}
	});
}
</script>
</head>
<body>

<div id="myDiv"><h2>使用 AJAX 修改文本内容</h2></div>
<button type="button" onclick="myFunction()">修改内容</button>

</body>
</html>
```